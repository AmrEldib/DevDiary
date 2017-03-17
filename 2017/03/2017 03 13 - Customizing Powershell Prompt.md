# Customizing PowerShell Prompt

## Steps
Install [posh-git](https://github.com/dahlbyk/posh-git) to add git support.  
```powershell
install-module posh-git
```

# Cmder PowerShell Prompt
Two files participate in setting up the prompt in Cmder:  
- `%cmder%\vendor\profile.ps1`  
- `%cmder%\config\user-profile.ps1`  

The second file doesn't actually overwrite the first file. They work together.  
The profile.ps1 file sets up some hooks for the user-profile.ps1 file to use. These are: 

# Resources
[Ultimate PowerShell Prompt Customization and Git Setup Guide](https://hodgkins.io/ultimate-powershell-prompt-and-git-setup): this adds git, ssh, and sets up SSH keys

## Prompt
[ConEmu on extending PowerShell prompt](http://conemu.github.io/en/PowershellPrompt.html)  
[Script to reload profile](http://stackoverflow.com/a/5501909)  
[Pshazz](https://github.com/lukesampson/pshazz) adds some customizations to shell prompt.  

## Colors
[Display Output in Color Using Windows PowerShell](https://technet.microsoft.com/en-us/library/ff406264.aspx)  

To print something with color and background, try:  
```powershell
write-host "hi" -foregroundcolor "magenta" -background "yellow"
```

## Available colors
    Black  
    Blue  
    Cyan  
    DarkBlue  
    DarkCyan  
    DarkGray  
    DarkGreen  
    DarkMagenta  
    DarkRed  
    DarkYellow  
    Gray  
    Green  
    Magenta  
    Red  
    White  
    Yellow  

