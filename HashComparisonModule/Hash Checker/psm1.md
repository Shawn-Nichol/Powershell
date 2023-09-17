<#
.SYNOPSIS
This function, Compare-Hash, is designed to compare the SHA-512 hash of a file with a known hash value.

.DESCRIPTION
The Compare-Hash function calculates the SHA-512 hash of a specified file and compares it to a provided known hash value. It is useful for verifying the integrity of files using cryptographic hashes.

.PARAMETER FilePath
Specifies the path to the file for which you want to calculate the hash.

.PARAMETER KnownHash
Specifies the known SHA-512 hash value to compare with the calculated hash of the file.

.EXAMPLE
PS C:\> Compare-Hash -FilePath "C:\Path\To\Your\File.ext" -KnownHash "YourKnownSHA512HashHere"

.NOTES
File Name: Compare-Hash.ps1
Author: Your Name
Copyright (c) 2023 Your Company. All rights reserved.
#>

function Compare-Hash {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$true)]
        [string]$FilePath,

        [Parameter(Mandatory=$true)]
        [string]$KnownHash
    )

    process {
        # Calculate the SHA-512 hash of the specified file
        $hash = Get-FileHash -Algorithm SHA512 -Path $FilePath

        # Compare the calculated hash with the provided known hash
        if ($hash.Hash -eq $KnownHash) {
            Write-Output "File is valid. The SHA-512 hash matches the known hash."
        } else {
            Write-Output "File is not valid. The SHA-512 hash does not match the known hash."
        }
    }
}
