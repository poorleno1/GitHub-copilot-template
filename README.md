# GitHub Copilot Configuration Template

A template repository providing GitHub Copilot instruction files for **Terraform**, **PowerShell**, and **Azure DevOps Pipelines** development. Copy these files to your projects to get consistent, high-quality AI code suggestions aligned with your team's patterns.

## What's Included

| Category                 | Files                                | Purpose                                              |
| ------------------------ | ------------------------------------ | ---------------------------------------------------- |
| **Copilot Instructions** | `.github/copilot-instructions.md`    | Global coding principles (KISS, YAGNI, SRP, DRY)     |
|                          | `.github/copilot/terraform.md`       | Azure-focused Terraform patterns (1.5.7, westeurope) |
|                          | `.github/copilot/powershell.md`      | PowerShell style guide and module patterns           |
|                          | `.github/copilot/azure-pipelines.md` | YAML pipeline templates for Terraform deployments    |
| **Editor Config**        | `.editorconfig`                      | Consistent formatting (2-space TF, 4-space PS)       |
|                          | `.vscode/settings.json`              | VS Code settings and extension recommendations       |
| **Example READMEs**      | `examples/infrastructure-project/`   | Combined Terraform + Pipeline project template       |
|                          | `examples/terraform/`                | Terraform-only project template                      |
|                          | `examples/powershell/`               | PowerShell module template                           |
|                          | `examples/azure-pipelines/`          | Pipeline documentation template                      |

## Structure Overview

```
.
├── .editorconfig                       # Universal formatting rules
├── .github/
│   ├── copilot-instructions.md         # Global GitHub Copilot instructions
│   └── copilot/                        # Language-specific instruction files
│       ├── terraform.md                # Terraform guidelines (Azure, 1.5.7)
│       ├── powershell.md               # PowerShell guidelines
│       └── azure-pipelines.md          # Azure DevOps pipeline guidelines
├── .vscode/
│   └── settings.json                   # VS Code workspace settings
├── examples/                           # README templates for target projects
│   ├── infrastructure-project/         # ⭐ Terraform + Pipeline (recommended)
│   │   └── README.md
│   ├── terraform/
│   │   └── README.md                   # Terraform-only project
│   ├── powershell/
│   │   └── README.md                   # PowerShell module
│   └── azure-pipelines/
│       └── README.md                   # Pipeline documentation only
└── README.md                           # This file
```

### What Gets Copied vs What's Reference Material

| Folder/File     | Copy to Projects? | Purpose                                                 |
| --------------- | ----------------- | ------------------------------------------------------- |
| `.github/`      | ✅ **Yes**        | Copilot AI instructions - teaches Copilot your patterns |
| `.vscode/`      | ✅ **Yes**        | VS Code settings for consistent editing                 |
| `.editorconfig` | ✅ **Yes**        | Formatting rules for all editors                        |
| `examples/`     | ❌ **No**         | Reference templates - copy content, not the folder      |

## Files Explained

### `.editorconfig`

Defines consistent formatting rules across different editors and IDEs:

- Terraform/HCL files: 2-space indentation
- PowerShell files: 4-space indentation
- YAML/JSON files: 2-space indentation
- Markdown files: preserves trailing whitespace

### `.github/copilot-instructions.md`

Global instructions that apply to all files. Covers:

- Core principles: KISS, YAGNI, SRP, DRY (in priority order)
- Repository structure and file references
- Documentation requirements
- Security best practices

### `.github/copilot/terraform.md`

Terraform-specific instructions (~350 lines) covering:

- **Version**: Terraform 1.5.7 (last MPL-licensed version)
- **Azure regions**: westeurope (primary), northeurope (DR)
- **Environments**: dev, uat, prod with validation rules
- **Naming**: `<project>-<environment>-<resource>-<instance>`
- **State**: Azure Storage backend with partial configuration
- **Provider pinning**: Exact version constraints
- **Anti-patterns**: Common mistakes to avoid

### `.github/copilot/powershell.md`

PowerShell-specific instructions covering:

- `[CmdletBinding()]` for all advanced functions
- Comment-based help (.SYNOPSIS, .DESCRIPTION, .EXAMPLE)
- Public/Private folder structure for modules
- Pester testing patterns
- Cross-platform compatibility (5.1 and 7.x)

### `.github/copilot/azure-pipelines.md`

Azure DevOps pipeline instructions (~280 lines) covering:

- Template strategy: `extends` for security, `template` for reuse
- Terraform tasks: TerraformInstaller, TerraformTaskV4
- Multi-environment: dev → uat → prod progression
- Environment approvals configured in Azure DevOps UI
- Service connections: per-environment with OIDC
- Variable management with Key Vault integration
- Anti-patterns: hardcoded secrets, single connection for all envs

### `.vscode/settings.json`

VS Code workspace settings optimized for:

- Language-specific formatting (tab sizes, encoding)
- GitHub Copilot enabled for all relevant file types
- Recommended extensions list

## How GitHub Copilot Uses These Files

GitHub Copilot automatically reads instruction files in the following order:

1. `.github/copilot-instructions.md` (global instructions)
2. Language-specific files in `.github/copilot/` folder
3. Context from your current file and project structure

## Quick Start

### For New Projects

```bash
# Navigate to your new project root
cd /path/to/your/new-project

# Clone the template repository
gh repo clone poorleno1/GitHub-copilot-template temp-copilot

# Copy the Copilot configuration files
cp -r temp-copilot/.github ./
cp -r temp-copilot/.vscode ./
cp temp-copilot/.editorconfig ./

# Clean up
rm -rf temp-copilot  # macOS/Linux
# Remove-Item -Path "temp-copilot" -Recurse -Force  # Windows PowerShell
```

### For Existing Projects

Same process - the copied files won't conflict with your existing code:

```bash
cd /path/to/existing-project

# Clone and copy (existing .github folder will be merged, not replaced)
gh repo clone poorleno1/GitHub-copilot-template temp-copilot
cp -r temp-copilot/.github ./
cp -r temp-copilot/.vscode ./
cp temp-copilot/.editorconfig ./
rm -rf temp-copilot
```

> **Note**: If you already have `.github/` or `.vscode/` folders, the copy will merge contents. Review for conflicts.

### Using the Example READMEs

The `examples/` folder contains **README templates** for your target projects. Use them as starting points:

| Your Project Type                 | Use This Template                           | Copy To                          |
| --------------------------------- | ------------------------------------------- | -------------------------------- |
| **Terraform + Pipeline** (common) | `examples/infrastructure-project/README.md` | `your-project/README.md`         |
| Terraform only (no pipeline)      | `examples/terraform/README.md`              | `your-project/README.md`         |
| PowerShell module                 | `examples/powershell/README.md`             | `your-module/README.md`          |
| Pipeline docs (separate file)     | `examples/azure-pipelines/README.md`        | `your-project/docs/pipelines.md` |

```bash
# Example: Starting a new Terraform project
mkdir my-terraform-project && cd my-terraform-project

# Copy Copilot config
cp -r ../GitHub-copilot-template/.github ./
cp -r ../GitHub-copilot-template/.vscode ./
cp ../GitHub-copilot-template/.editorconfig ./

# Use the example README as your project's README
cp ../GitHub-copilot-template/examples/terraform/README.md ./README.md

# Edit README.md to match your specific project
```

### Alternative: Use as GitHub Template

1. Click **"Use this template"** on the GitHub repository page
2. Create a new repository from the template
3. Delete the `examples/` folder (it's only for reference)
4. Rename/edit files as needed for your project

### After Setup

1. **Customize** the instruction files in `.github/copilot/` based on your team's needs
2. **Remove unused instruction files** - if not using PowerShell, delete `powershell.md`
3. **Install** the recommended VS Code extensions
4. **Start coding** with enhanced GitHub Copilot assistance!

## How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                     YOUR PROJECT                                │
├─────────────────────────────────────────────────────────────────┤
│  .github/                                                       │
│  ├── copilot-instructions.md  ←── Global rules for all files   │
│  └── copilot/                                                   │
│      ├── terraform.md         ←── Rules when editing .tf files │
│      ├── powershell.md        ←── Rules when editing .ps1 files│
│      └── azure-pipelines.md   ←── Rules when editing YAML pipes│
│                                                                 │
│  your-code/                                                     │
│  ├── main.tf        ←── Copilot uses terraform.md rules here   │
│  ├── Deploy.ps1     ←── Copilot uses powershell.md rules here  │
│  └── azure-pipelines.yml ←── Copilot uses azure-pipelines.md   │
└─────────────────────────────────────────────────────────────────┘
```

GitHub Copilot automatically reads these instruction files and applies them when generating code suggestions for matching file types.

## Recommended Extensions

- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) - AI pair programmer
- [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) - AI chat assistance
- [HashiCorp Terraform](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform) - Terraform language support
- [PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) - PowerShell language support
- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) - EditorConfig support
- [Azure Pipelines](https://marketplace.visualstudio.com/items?itemName=ms-azure-devops.azure-pipelines) - Pipeline YAML support

## Tips for Better Copilot Assistance

1. **Be Specific**: The more context you provide in comments, the better suggestions you'll get
2. **Use Descriptive Names**: Clear variable and function names help Copilot understand intent
3. **Follow Conventions**: Stick to the patterns defined in your instruction files
4. **Iterate**: Refine your instruction files based on the quality of suggestions you receive

## Customization

Modify the instruction files to match your organization's needs:

- **Azure regions**: Change `westeurope`/`northeurope` to your regions
- **Terraform version**: Update from 1.5.7 if using OpenTofu or have BSL license
- **Environments**: Modify `dev`/`uat`/`prod` to match your workflow
- **Naming conventions**: Adjust patterns to match your standards
- **Remove unused files**: Delete `powershell.md` if not using PowerShell

## License

This template is provided as-is for use in your projects.
