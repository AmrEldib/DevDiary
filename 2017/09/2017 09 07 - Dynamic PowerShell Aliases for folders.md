# Dynamic PowerShell Aliases for Folders

# Problem

I want to have a CSV file where I define all the folders I want to have a quick shortcut for in PowerShell.  
For example, when I type `c`, I want to go to `~\Code`.  
The CSV file will have two columns: `alias` hold `c` and `folder` which holds `~\Code`.  

# Solution

Use `Set-Alias` to create aliases.  
Use `Import-Csv` to import Csv file.  

PowerShell uses `Set-Location` cmdlet to change directory.  
When creating an alias for `Set-Location ~\Code`, it must be enclosed in a function. This is mentioned in [Set-Alias notes](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/Set-Alias?view=powershell-5.1#notes).  

This didn't end up working. I couldn't find a way to pass arguments to the value of the alias.  
To get around this, I created a new command with alias `g` and just pass the folder alias to it: `g c` to go to the folder with alias `c`.  