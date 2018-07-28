# Problem

When calling a PowerShell script from another script, files at a relative path in the called script use the path of the first-invoked script. This is incorrect. It should use the path of the script called from the invoked script.  

# Solution

Prefix all relative files with the variable `$scriptPath` with this value:   

```powershell
$scriptPath = split-path -parent $MyInvocation.MyCommand.Definition
```

Use `Join-Path`  

```powershell
$customizationsFile = Join-Path $scriptPath "file.txt"
```