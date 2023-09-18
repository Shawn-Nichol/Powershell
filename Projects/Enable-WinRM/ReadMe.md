# Enable-WinRM PowerShell Module

The **Enable-WinRM PowerShell Module** is a simple yet powerful tool for remotely enabling the Windows Remote Management (WinRM) service on remote computers. This module allows you to quickly and easily set up WinRM, enabling secure remote management and PowerShell remoting on target machines.

## Features

- Enables the WinRM service on remote computers.
- Streamlines the process of configuring WinRM for remote management.
- Requires administrative privileges on the remote computer.
- Utilizes the SysInternals psservice.exe utility (ensure it's installed on your local computer).

## Usage

To get started, follow these steps:

1. Create a directory to store the module.
2. Download or copy the Enable-WinRM.ps1 script into the module directory.
3. Import the module by using the Import-Module cmdlet.
4. Use the Enable-WinRM cmdlet with the -ComputerName parameter to specify the target remote computer."

```powershell
Import-Module Enable-WinRM
Enable-WinRM -ComputerName "Remote-Computer"
```

Ensure you have administrative access to the remote computer and that SysInternals psservice.exe is installed on your local machine for successful execution.

## Author

- **Author:** Shawn Nichol

