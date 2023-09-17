<#
.SYNOPSIS
    Compares a provided hash with the calculated hash of a file and displays the result in color-coded text.

.DESCRIPTION
    This function calculates the hash of a file using a specified hash algorithm, compares it to a provided hash,
    and displays the result in green (valid) or red (invalid) text. It also displays the provided and calculated hashes.

.PARAMETER FilePath
    Specifies the path to the file you want to calculate the hash.

.PARAMETER ProvidedHash
    Specifies the hash value to compare against the calculated hash of the file.

.PARAMETER HashType
    Specifies the hash algorithm to use. Valid values are "MD5," "SHA1," "SHA256," "SHA384," or "SHA512." The default is "SHA512."

.EXAMPLE
    Compare-Hash -FilePath "C:\Path\To\Your\File.txt" -ProvidedHash "YourProvidedHashHere"
    This example calculates the SHA-512 hash of the specified file and compares it to the provided hash.

.EXAMPLE
    Compare-Hash -FilePath "C:\Path\To\Another\File.txt" -ProvidedHash "AnotherProvidedHash" -HashType "SHA256"
    This example calculates the SHA-256 hash of a different file and compares it to the provided hash using the SHA-256 algorithm.
#>

function Compare-Hash {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$true)]
        [string]$FilePath,

        [Parameter(Mandatory=$true)]
        [string]$ProvidedHash,

        [Parameter(Mandatory=$false)]
        [ValidateSet("MD5", "SHA1", "SHA256", "SHA384", "SHA512")]
        [string]$HashType = "SHA512"
    )

    process {
        # Calculate the specified hash type of the specified file.
        $hash = Get-FileHash -Algorithm $HashType -Path $FilePath

        # Compare the calculated hash with the provided hash
        if ($hash.Hash -eq $ProvidedHash) {
            # Display the result in green if it is valid.
            Write-Host "File is valid. The $($HashType) hash matches the provided hash." -ForegroundColor Green
        } else {
            # Display the result in red if it is invalid.
            Write-Host "File is not valid. The $($HashType) hash does not match the provided hash." -ForegroundColor Red
        }

        # Print both the provided and calculated hash values in a formatted manner.
        Write-Output "Provided Hash  : $ProvidedHash"
        Write-Output "Calculated Hash: $($hash.Hash)"
    }
}
