@{
    ModuleVersion = '1.0'
    Author = 'Shawn Nichol'
    CompanyName = 'Shawn Nichol'
    Description = 'A custom module to enable WinRM on a remote computer.'
    PowerShellVersion = '5.1'
    FunctionsToExport = 'Enable-WinRM'
    PrivateData = @{
        PSData = @{
            Tags = @('WinRM', 'Remote')
        }
    }
}
