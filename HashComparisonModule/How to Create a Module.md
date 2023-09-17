# PowerShell Module Management

This repository guides managing PowerShell modules, including their locations and how to create and import custom modules.

## Module Locations

PowerShell modules can be located in various directories. To view your current module path in PowerShell, you can use the following command:

```powershell
$env:PSModulePath -split ';'
```

### User-Specific Modules

Users can store modules in their own user profile, making them available only to their user account. These modules are typically stored in the following directory:

```
$env:USERPROFILE\Documents\WindowsPowerShell\Modules
```

### System-Wide Modules

Modules installed in system-wide locations are available to all user accounts. These modules are usually stored in the following directories:

```
C:\Program Files\WindowsPowerShell\Modules
C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules
```

## Creating a Custom Module

To create a custom PowerShell module, you'll need to create two files: a `.psm1` script module and a `.psd1` module manifest file.

### .psd1 File (Module Manifest)

```powershell
@{
    ModuleVersion = '1.0'
    Author = 'Your Name'
    Description = 'A custom module for hash comparison.'
    RootModule = 'Name of psm1 file'
    FunctionsToExport = 'function-name'
}
```

### .psm1 File (Script Module)

```powershell
<#
.SYNOPSIS
Provides a one-line description of what the module does.

.DESCRIPTION
Provides a detailed description of the module or cmdlet's purpose and functionality.

.PARAMETER P1
Describes the P1 parameter usage.

.PARAMETER P2
Describes the P2 parameter usage. 

.EXAMPLE
Provide an example of how to use the cmdlet. You can have more than one example.
#>

function Compare-Hash {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$true)]
        [string]$P1,

        [Parameter(Mandatory=$true)]
        [string]$P2
    )

    process {
        # Your code here
    }
}
```

## Importing Modules

You can import modules in various ways:

### Standard Import

```powershell
Import-Module MyCustomModule
```

### Import from a Custom Directory

```powershell
Import-Module C:\Path\To\Custom\Module\MyCustomModule
```

### Import a Specific Module Version

```powershell
Import-Module -Name MyCustomModule -RequiredVersion 1.0
```

### Import Module to Last Longer Than the Current Session

```powershell
Import-Module -Name MyCustomModule -Scope Global
```
