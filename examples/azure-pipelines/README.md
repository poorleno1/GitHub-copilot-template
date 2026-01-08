<!--
TEMPLATE: Copy this file to your project as docs/pipelines.md or similar.
Then customize for your specific pipeline setup.
Delete this comment block after copying.
-->

# Azure Pipelines Instructions

When working with Azure DevOps pipeline files (`azure-pipelines.yml`), follow these specific guidelines for Terraform infrastructure deployments.

## Pipeline Structure

Organize pipelines using templates for reusability and security:

```
project/
├── azure-pipelines.yml           # Main pipeline (extends template)
├── .azure-pipelines/
│   ├── templates/
│   │   ├── stages/               # Stage templates
│   │   ├── jobs/                 # Job templates
│   │   └── steps/                # Step templates
│   └── variables/
│       ├── dev.yml               # Environment-specific variables
│       ├── uat.yml
│       └── prod.yml
└── terraform/
```

## Template Pattern

Use `extends` for security control and `template` includes for reusability:

```yaml
# azure-pipelines.yml
trigger:
  branches:
    include: [main]
  paths:
    include: [terraform/**]

extends:
  template: .azure-pipelines/templates/terraform-pipeline.yml
  parameters:
    terraformVersion: "1.5.7"
    environments: ["dev", "uat", "prod"]
```

## Terraform Deployment Pattern

```yaml
# Stage template for Terraform deployment
parameters:
  - name: environment
    type: string
    values: ["dev", "uat", "prod"]
  - name: azureSubscription
    type: string

stages:
  - stage: Deploy_${{ parameters.environment }}
    jobs:
      - deployment: TerraformApply
        environment: ${{ parameters.environment }} # Approval gates configured in UI
        strategy:
          runOnce:
            deploy:
              steps:
                - task: TerraformInstaller@1
                  inputs:
                    terraformVersion: "1.5.7"

                - task: TerraformTaskV4@4
                  displayName: "Terraform Init"
                  inputs:
                    provider: "azurerm"
                    command: "init"
                    backendServiceArm: "${{ parameters.azureSubscription }}"
                    backendAzureRmKey: "$(environment).tfstate"

                - task: TerraformTaskV4@4
                  displayName: "Terraform Plan"
                  inputs:
                    provider: "azurerm"
                    command: "plan"
                    commandOptions: "-out=tfplan -input=false"
                    environmentServiceNameAzureRM: "${{ parameters.azureSubscription }}"

                - task: TerraformTaskV4@4
                  displayName: "Terraform Apply"
                  inputs:
                    provider: "azurerm"
                    command: "apply"
                    commandOptions: "tfplan"
                    environmentServiceNameAzureRM: "${{ parameters.azureSubscription }}"
```

## Security Best Practices

- **Separate service connections** per environment: `Azure-Dev-Terraform`, `Azure-Prod-Terraform`
- **Use Workload Identity Federation** (OIDC) instead of client secrets
- **Link variable groups to Key Vault** for secrets
- **Configure approval gates** on `uat` and `prod` environments in Azure DevOps UI
- **Path-based triggers** - only run when terraform files change

## Variable Management

```yaml
# .azure-pipelines/variables/prod.yml
variables:
  environment: 'prod'
  location: 'westeurope'
  azureSubscription: 'Azure-Prod-Terraform'
  # No secrets here - use Key Vault linked variable groups

# In pipeline:
variables:
  - group: 'terraform-secrets'  # Linked to Key Vault
  - template: .azure-pipelines/variables/$(environment).yml
```

## Anti-Patterns to Avoid

- ❌ Hardcoding secrets in YAML
- ❌ Single service connection for all environments
- ❌ Deploying to prod without approval gates
- ❌ Skipping `terraform plan` artifact for review
- ❌ Using classic release pipelines instead of YAML
