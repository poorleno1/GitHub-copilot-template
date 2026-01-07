# Example Terraform Project

This is an example of how to structure a Terraform project following the guidelines in the copilot instructions.

## Usage

1. Copy the terraform/ directory to your project
2. Customize variables.tf with your specific requirements
3. Create a terraform.tfvars file with your values (don't commit this!)
4. Run terraform commands:

```bash
terraform init
terraform plan
terraform apply
```

## Files Included

- `main.tf` - Primary resource definitions
- `variables.tf` - Input variable definitions
- `outputs.tf` - Output value definitions
- `versions.tf` - Provider version constraints
- `terraform.tfvars.example` - Example variable values