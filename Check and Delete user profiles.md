Get-volume
Get-WmiObject -Class Win32_UserProfile | Where-Object {$_.Special -ne 'Special'} | Select-Object LocalPath, Loaded
 (Get-WmiObject -Class Win32_UserProfile | Where {$_.localpath -eq "C:\Users\proesinger"}).Delete()

Used to display User profile size
```
$UserProfiles = Get-WmiObject -Class Win32_UserProfile | Where-Object { $_.Special -eq $false }

foreach ($Profile in $UserProfiles) {
    $ProfilePath = $Profile.LocalPath
    $ProfileSize = Get-ChildItem -Path $ProfilePath -Recurse -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum
    if ($ProfileSize -ne $null) {
        $ProfileSizeInGB = $ProfileSize.Sum / 1GB
        if ($ProfileSizeInGB -lt 1) {
            $ProfileSizeInMB = [math]::Round($ProfileSize.Sum / 1MB, 2)
            Write-Output "$ProfilePath - Size: $ProfileSizeInMB MB"
        } else {
            $ProfileSizeInGB = [math]::Round($ProfileSizeInGB, 2)
            Write-Output "$ProfilePath - Size: $ProfileSizeInGB GB"
        }
    } else {
        Write-Output "$ProfilePath - Size: Unable to determine size"
    }
}
```
Get directory size of directories in current directory
```
$UserDirectory = "C:\"  # Specify the user directory here

$Folders = Get-ChildItem -Path $UserDirectory -Directory -ErrorAction SilentlyContinue

if ($Folders.Count -gt 0) {
    foreach ($Folder in $Folders) {
        $FolderSize = Get-ChildItem -Path $Folder.FullName -Recurse -File -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum
        if ($FolderSize -ne $null) {
            $FolderSizeInMB = $FolderSize.Sum / 1MB
            $SizeSuffix = "MB"
            if ($FolderSizeInMB -ge 1024) {
                $FolderSizeInMB = $FolderSizeInMB / 1024
                $SizeSuffix = "GB"
            }
            Write-Output "$($Folder.FullName) - Size: $($FolderSizeInMB.ToString('N2')) $SizeSuffix"
        } else {
            Write-Output "$($Folder.FullName) - Size: Unable to determine size"
        }
    }
} else {
    Write-Output "No folders found in $UserDirectory"
}

```
