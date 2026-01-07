# Example PowerShell Module

This is an example of how to structure a PowerShell module following the guidelines in the copilot instructions.

## Usage

1. Copy the powershell/ directory to your project
2. Customize the module manifest (.psd1) file
3. Add your functions to the Public/ directory
4. Import the module:

```powershell
Import-Module .\ExampleModule.psd1
```

## Files Included

- `ExampleModule.psd1` - Module manifest
- `ExampleModule.psm1` - Module file that loads functions
- `Public/` - Directory for public functions
- `Private/` - Directory for internal helper functions
- `Tests/` - Directory for Pester tests