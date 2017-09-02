# Problem

I need to find files that has a certain criteria and then rename them.  
Those files are all over the place and not in a single directory. They're spread over multiple machines.  
However, all of them are indexed using [Everything](https://www.voidtools.com/)  
Everything has a [command line interface](https://www.voidtools.com/support/everything/command_line_interface/) that can return results in the command line, or save it to an `efu` file.  
`efu` file is a comma separated file that lists file info; one file per line.  
You can also use the UI to export results to file.  


# Solution
Write a PowerShell script that reads the `efu` file as CSV file, then rename those files.  

```powershell
$DebugPreference = "Continue"

$files = Import-Csv .\files.efu 
$key = ".srt"
$newkey = ".eng.srt"
$renameCount = 0

foreach ($file in $files) {
    Write-Debug $file.Filename
    # generate new name
    $newName = $file.Filename.Replace($key, $newkey)
    # Check if file still exists
    if (Test-Path $file.Filename) {
        # Check first that a file with the new name doesn't exist
        if ((Test-Path $newName) -eq $False) {
            Write-Debug "Renaming to: $newName" 
            # rename item
            Rename-Item -Path $file.Filename -NewName $newName             
            # increase count
            $renameCount += 1
        }
        else {
            # If a file with the new name already exist, write a message to console
            Write-Host "Conflict: " + $newName 
        }
    }
}

Write-Host "All done. Renamed $renameCount files"
```

## Notes
`$DebugPreference` lets PowerShell prints out lines with `Write-Debug`. Comment it out to stop seeing these messages.  
`$key` and `$newkey` are the strings to look for and replace with.  
Script will check if file still exists, and if a file with the new name already exist.  
If a file with the new name already exists, it'll skip renaming and print out a Conflict message.  

## Common Issue
If you run this script as Administrator, you might run into an issue when renaming files on a mapped network drive. To avoid that, run script as a regular user.  
This issue is due to a PowerShell bug. [Read more](https://stackoverflow.com/questions/4742992/cannot-access-network-drive-in-powershell-running-as-administrator).   