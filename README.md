# GitHub Copilot Configuration Template

This repository contains configuration files and instructions for optimizing GitHub Copilot for Terraform and PowerShell development.

## Structure Overview

```
.
├── .editorconfig                    # Universal formatting rules
├── .github/
│   ├── copilot-instructions.md      # Global GitHub Copilot instructions
│   └── copilot/                     # Specific instruction files
│       ├── terraform.md             # Terraform-specific guidelines
│       └── powershell.md            # PowerShell-specific guidelines
├── .vscode/
│   └── settings.json                # VS Code workspace settings
└── README.md                        # This file
```

## Files Explained

### `.editorconfig`

Defines consistent formatting rules across different editors and IDEs. Includes specific rules for:

- Terraform files (2-space indentation)
- PowerShell files (4-space indentation)
- JSON/YAML files (2-space indentation)
- Markdown files (preserves trailing whitespace)

### `.github/copilot-instructions.md`

Global instructions that apply to all files in your project. These guide GitHub Copilot on:

- Code quality standards
- Documentation requirements
- Security best practices
- Testing approaches

### `.github/copilot/terraform.md`

Terraform-specific instructions covering:

- HCL formatting and style
- Resource management patterns
- Module development best practices
- State management guidelines
- Security considerations

### `.github/copilot/powershell.md`

PowerShell-specific instructions covering:

- PowerShell style guide adherence
- Function structure and documentation
- Error handling patterns
- Module development practices
- Cross-platform compatibility

### `.vscode/settings.json`

VS Code workspace settings optimized for:

- Language-specific formatting
- GitHub Copilot configuration
- Recommended extensions

## How GitHub Copilot Uses These Files

GitHub Copilot automatically reads instruction files in the following order:

1. `.github/copilot-instructions.md` (global instructions)
2. Language-specific files in `.github/copilot/` folder
3. Context from your current file and project structure

## Quick Start

### Option 1: Clone and Copy (Recommended)

```bash
# Navigate to your project root
cd /path/to/your/project

# Clone the template repository
gh repo clone poorleno1/GitHub-copilot-template temp-copilot

# Copy the configuration files to your project
cp -r temp-copilot/.github ./
cp -r temp-copilot/.vscode ./
cp temp-copilot/.editorconfig ./

# Clean up the temporary folder
# macOS/Linux:
rm -rf temp-copilot

# Windows PowerShell:
# Remove-Item -Path "temp-copilot" -Recurse -Force -ErrorAction SilentlyContinue
```

### Option 2: Use as GitHub Template

1. Click **"Use this template"** on the GitHub repository page
2. Create a new repository from the template
3. Clone your new repository and start coding

### After Setup

1. Customize the instruction files in `.github/copilot/` based on your team's needs
2. Install the recommended VS Code extensions
3. Start coding with enhanced GitHub Copilot assistance!

## Recommended Extensions

- **GitHub Copilot** - AI pair programmer
- **GitHub Copilot Chat** - AI chat assistance
- **HashiCorp Terraform** - Terraform language support
- **PowerShell** - PowerShell language support
- **EditorConfig** - EditorConfig support

## Tips for Better Copilot Assistance

1. **Be Specific**: The more context you provide in comments, the better suggestions you'll get
2. **Use Descriptive Names**: Clear variable and function names help Copilot understand intent
3. **Follow Conventions**: Stick to the patterns defined in your instruction files
4. **Iterate**: Refine your instruction files based on the quality of suggestions you receive

## Customization

Feel free to modify these instruction files to match your organization's:

- Coding standards
- Security requirements
- Project structure preferences
- Tool choices and workflows
