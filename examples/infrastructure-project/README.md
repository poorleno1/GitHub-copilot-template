<!--
TEMPLATE: Copy this file to your infrastructure project as README.md
Replace all placeholder text (marked with <...>) with your project-specific details.
Delete this comment block after copying.
-->

# <Project Name> Infrastructure

Terraform infrastructure code and Azure DevOps pipeline for deploying <brief description of what this deploys>.

## Overview

| Component          | Description                            |
| ------------------ | -------------------------------------- |
| **Cloud Provider** | Azure                                  |
| **IaC Tool**       | Terraform 1.5.7                        |
| **CI/CD**          | Azure DevOps Pipelines                 |
| **Environments**   | dev, uat, prod                         |
| **Region**         | westeurope (primary), northeurope (DR) |

## Architecture

<!-- Add architecture diagram or description -->

```
<Describe or diagram the infrastructure being deployed>
```

## Prerequisites

### Tools

- [Terraform 1.5.7](https://releases.hashicorp.com/terraform/1.5.7/) - exact version required
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- [VS Code](https://code.visualstudio.com/) with recommended extensions

### Azure Resources (Pre-existing)

| Resource           | Purpose                  | How to Get Access          |
| ------------------ | ------------------------ | -------------------------- |
| Azure Subscription | Target for deployments   | Request via <process>      |
| Service Principal  | Terraform authentication | Created per environment    |
| Storage Account    | Terraform state backend  | `<tfstate-rg>/<tfstatesa>` |

### Azure DevOps

| Requirement         | Details                                                              |
| ------------------- | -------------------------------------------------------------------- |
| Project             | `<Azure DevOps Project Name>`                                        |
| Service Connections | `Azure-Dev-Terraform`, `Azure-UAT-Terraform`, `Azure-Prod-Terraform` |
| Environments        | `dev`, `uat` (approval required), `prod` (approval required)         |
| Variable Group      | `terraform-secrets` linked to Key Vault                              |

## Quick Start (Local Development)

### 1. Clone and Setup

```bash
git clone <repository-url>
cd <project-name>
```

### 2. Authenticate to Azure

```bash
az login
az account set --subscription "<subscription-name>"
```

### 3. Initialize Terraform (Dev Environment)

```bash
cd terraform

terraform init \
  -backend-config="resource_group_name=tfstate-rg" \
  -backend-config="storage_account_name=<tfstatesa>" \
  -backend-config="container_name=tfstate" \
  -backend-config="key=<project>/dev/terraform.tfstate"
```

### 4. Plan Changes

```bash
terraform plan -var-file="environments/dev/terraform.tfvars"
```

### 5. Apply (Dev Only)

```bash
terraform apply -var-file="environments/dev/terraform.tfvars"
```

> ⚠️ **UAT and Prod deployments must go through the pipeline** - do not apply locally.

## Project Structure

```
.
├── README.md                         # This file
├── azure-pipelines.yml               # Main pipeline definition
├── .azure-pipelines/
│   ├── templates/
│   │   ├── stages/
│   │   │   └── terraform-deploy.yml  # Reusable deployment stage
│   │   └── steps/
│   │       ├── terraform-init.yml
│   │       ├── terraform-plan.yml
│   │       └── terraform-apply.yml
│   └── variables/
│       ├── dev.yml                   # Dev environment variables
│       ├── uat.yml                   # UAT environment variables
│       └── prod.yml                  # Prod environment variables
└── terraform/
    ├── main.tf                       # Primary resources
    ├── variables.tf                  # Input variable definitions
    ├── outputs.tf                    # Output values
    ├── versions.tf                   # Terraform and provider versions
    ├── backend.tf                    # Backend configuration (partial)
    ├── locals.tf                     # Local values and naming
    ├── modules/                      # Custom modules (if any)
    └── environments/
        ├── dev/
        │   └── terraform.tfvars
        ├── uat/
        │   └── terraform.tfvars
        └── prod/
            └── terraform.tfvars
```

## Pipeline Workflow

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│     DEV     │────►│     UAT     │────►│    PROD     │
│  (auto)     │     │ (approval)  │     │ (approval)  │
└─────────────┘     └─────────────┘     └─────────────┘
     │                    │                    │
     ▼                    ▼                    ▼
  terraform            terraform            terraform
  init/plan/apply      init/plan/apply      init/plan/apply
```

### Pipeline Triggers

| Trigger                | Action                                      |
| ---------------------- | ------------------------------------------- |
| Push to `main`         | Deploy to all environments (with approvals) |
| Push to `feature/*`    | Validate only (no deployment)               |
| Pull Request to `main` | Plan and validate (no apply)                |

### Running the Pipeline

1. **Automatic**: Push to `main` branch triggers deployment
2. **Manual**: Navigate to Pipelines > `<pipeline-name>` > Run pipeline

## Configuration

### Environment Variables

| Variable       | Description        | Example              |
| -------------- | ------------------ | -------------------- |
| `environment`  | Target environment | `dev`, `uat`, `prod` |
| `location`     | Azure region       | `westeurope`         |
| `project_name` | Project identifier | `myproject`          |

### Secrets (from Key Vault)

| Secret               | Description               |
| -------------------- | ------------------------- |
| `sql-admin-password` | SQL Server admin password |
| `<other-secrets>`    | <description>             |

## Terraform Resources

### Resources Created

| Resource                 | Purpose                     |
| ------------------------ | --------------------------- |
| `azurerm_resource_group` | Container for all resources |
| `<other resources>`      | `<description>`             |

### Outputs

| Output                | Description                        |
| --------------------- | ---------------------------------- |
| `resource_group_name` | Name of the created resource group |
| `<other outputs>`     | `<description>`                    |

## Troubleshooting

### Common Issues

| Issue                     | Solution                                                                  |
| ------------------------- | ------------------------------------------------------------------------- |
| State lock error          | Check if another pipeline is running, or break the lease in Azure Storage |
| Permission denied         | Verify service connection has required RBAC roles                         |
| Provider version mismatch | Run `terraform init -upgrade`                                             |

### Useful Commands

```bash
# Validate configuration
terraform validate

# Format check
terraform fmt -check -recursive

# Show current state
terraform show

# Import existing resource
terraform import <resource_type>.<name> <azure_resource_id>
```

## Contributing

1. Create a feature branch: `git checkout -b feature/<feature-name>`
2. Make changes and test locally against `dev`
3. Run `terraform fmt` and `terraform validate`
4. Create a Pull Request to `main`
5. Pipeline will run plan - review the output
6. After merge, pipeline deploys through environments

## Related Documentation

- [Terraform AzureRM Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
- [Azure DevOps Pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/)
- [Project Architecture Document](link-to-architecture-doc)

## Contacts

| Role                | Name   | Contact |
| ------------------- | ------ | ------- |
| Project Owner       | <name> | <email> |
| Infrastructure Lead | <name> | <email> |
