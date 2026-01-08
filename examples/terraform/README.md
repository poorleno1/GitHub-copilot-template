<!--
TEMPLATE: Copy this file to your Terraform project as README.md
Then replace placeholder text with your project-specific details.
Delete this comment block after copying.
-->

# Terraform Instructions

When working with Terraform files (.tf, .tfvars, .hcl), follow these specific guidelines:

## Code Style and Formatting

- Use 2 spaces for indentation (configured in .editorconfig)
- Run `terraform fmt` before committing
- Use snake_case for resource names and variables
- Group related resources together logically

## Resource Management

- Use descriptive resource names that indicate their purpose
- Include tags on all taggable resources with at minimum:
  - Name
  - Environment (dev/staging/prod)
  - Project/Application
  - Owner/Team
- Use data sources instead of hardcoded values when possible

## Variables and Outputs

- Define all variables with descriptions and types
- Use validation rules for variables when appropriate
- Set default values for optional variables
- Export useful information as outputs with descriptions

## State Management

- Always use remote state for team projects
- Configure state locking when using remote backends
- Never commit .tfstate files to version control
- Use separate state files for different environments

## Modules

- Create reusable modules for common patterns
- Follow module best practices:
  - README.md with usage examples
  - variables.tf with all input variables
  - outputs.tf with useful outputs
  - main.tf with primary resources
- Pin module versions in production

## Security

- Use terraform-docs to generate documentation
- Store sensitive variables in .tfvars files (not committed)
- Use data sources for existing resources instead of importing
- Implement resource-level security controls

## Validation and Testing

- Run `terraform validate` before applying
- Use `terraform plan` to review changes
- Consider using tools like tflint or checkov for security scanning
- Test modules with multiple scenarios

## File Organization

```
project/
├── main.tf                 # Primary resources
├── variables.tf            # Input variables
├── outputs.tf              # Output values
├── versions.tf             # Provider requirements
├── terraform.tfvars.example # Example variables
├── modules/
│   └── [module-name]/
└── environments/
    ├── dev/
    ├── staging/
    └── prod/
```

## Provider Configuration

- Always specify provider versions in versions.tf
- Use the latest stable provider versions
- Configure provider-specific settings appropriately
- Consider using provider aliases for multi-region deployments

## Task-Based Workflow

When working on this project, follow the task-based approach:

1. **Read SPEC.md first** - Understand the overall project requirements, architecture, and constraints
2. **Check the tasks/ folder** - Look for numbered task files (e.g., `01-networking.md`, `02-storage.md`)
3. **Complete tasks in order** - Tasks are numbered to indicate dependencies
4. **Follow task instructions** - Each task file contains specific requirements and acceptance criteria
5. **Validate after each task** - Run `terraform validate` and `terraform fmt` before marking complete

### Task File Structure

Each task file in `tasks/` should contain:

- **Objective**: What needs to be built
- **Requirements**: Specific resources and configurations
- **Acceptance Criteria**: How to verify completion
- **References**: Links to relevant SPEC.md sections

### When Completing a Task

- Reference SPEC.md for naming conventions, tags, and architecture
- Create files following the File Organization structure above
- Include all required outputs as specified in SPEC.md
- Test with `terraform validate` before reporting completion
