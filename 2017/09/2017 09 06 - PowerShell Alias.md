# PowerShell Alias

# Problem

How to set up PowerShell aliases in a way so that each alias is in its file?  
I'm using Cmder and [cmder-powershell-powerline-prompt](https://github.com/AmrEldib/cmder-powershell-powerline-prompt)  

Right now, aliases are stored in the `%CMDER%\config\profile.d\alias.ps1` file.  

# Solution

[Cmder docs on PowerShell aliases](https://github.com/cmderdev/cmder#powershellexe-aliases) explains that any `.ps1` file listed under `$ENV:CMDER_ROOT\config\profile.d` folder will be loaded. Simply place one file per alias with a `.ps1` extension.  
To easily identify alias files, use `.alias.ps1` as extension.  

Some alias files are private and shouldn't be excluded using gitignore, name those files with `.private.alias.ps1` extension.  

