<#
.SYNOPSIS
    Enables the WinRM service on a remote computer.
.DESCRIPTION
    The Enable-WinRM cmdlet starts the WinRM service on a remote computer specified by the ComputerName parameter.
    This allows remote management and PowerShell remoting on the target machine.
    
    Note: You need administrative privileges on the remote computer and SysInternals psservice.exe installed on your local computer for this script to execute this command successfully.

.PARAMETER ComputerName
    Specifies the name of the remote computer on which to enable WinRM.
    
    This parameter is mandatory.

.EXAMPLE
    Enable-WinRM -ComputerName "Remote-Computer"
    
    This example enables the WinRM service on the computer named "RemoteComputers."

.NOTES
    File Name      : Enable-WinRM.ps1
    Author         : Shawn Nichol
    Prerequisite   : Administrative privileges on the remote computer
    Prerequisite   : SysInternals psservice.exe installed on local computer
    
    Version History:
    - 1.0 (Initial release)
#>

function Enable-WinRM {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $true)]
        [string]$ComputerName
    )

    process {
        $processParams = @{
            FilePath = "psservice.exe"
            ArgumentList = "\\$ComputerName start WinRM"
            Wait = $true
        }

        Start-Process @processParams

        Write-Output "WinRM has been started on $ComputerName"
    }
}

Export-ModuleMember -Function Enable-WinRM
