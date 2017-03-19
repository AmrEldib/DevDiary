# Customizing PowerShell Prompt

## Steps
Install [posh-git](https://github.com/dahlbyk/posh-git) to add git support.  
```powershell
install-module posh-git
```
Edit `user-profile.ps` in Cmder config folder to add git prompt.  
In PowerShell task settings, change icon by changing _Task Parameters_ to `/icon "%CMDER_ROOT%\icons\cmder_blue.ico"`

# Cmder PowerShell Prompt
Two files participate in setting up the prompt in Cmder:  
- `%cmder%\vendor\profile.ps1`  
- `%cmder%\config\user-profile.ps1`  

The second file doesn't actually overwrite the first file. They work together.  
The profile.ps1 file sets up some hooks for the user-profile.ps1 file to use. These are: 

PowerShell task in Cmder starts with `-NoProfile` flag which disables loading the PowerShell user profile as stored in `%USERPROFILE%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` file. [Source](https://superuser.com/a/962094/96992)  

# SSH-Agent
[SSH Agent in PowerShell](https://markembling.info/2009/09/ssh-agent-in-powershell)  
> SSH-agent is a process which runs in the background and stores the private key and passphrase. This means that you do not have to repeatedly type it every time you need to use your key. Instead you just provide it once, when the ssh-agent process is started.

Get-SshAgent - Returns the process ID of the running agent, or zero if there is not one currently running.  
Start-SshAgent - Starts the agent process and sets the appropriate environment variables for SSH.  

Git Credential Manager for Windows [doesn't support connecting with SSH](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/issues/25#issuecomment-208932990).  
[How to set up Git to use Git Credential Manager to store HTTPS credentials](http://stackoverflow.com/a/5343146/463).  

Add `Start-SshAgent` to shell starting script.  
Posh-Git module has `Add-SshKey` command to add SSH key and use it later. [more info](http://haacked.com/archive/2011/12/19/get-git-for-windows.aspx/)

It's possible there's [a way to save SSH key password in Windows Credential Manager](https://github.com/lukesampson/scoop/wiki/SSH-on-Windows#save-your-ssh-key-password-in-windows-credential-manager)  

# Test authentication to GitHub
After adding SSH key, you can test if it works against GitHub.  
```bash
ssh -T git@github.com
```  
Or, Gitlab  
```bash
ssh -T git@gitlab.com
```  

# Colorize directory listing
[Colorize your directory listing](https://hodgkins.io/ultimate-powershell-prompt-and-git-setup#colorize-your-directory-listing)  
Use [Get-ChildItem-Color](https://github.com/joonro/Get-ChildItem-Color/blob/develop/Get-ChildItem-Color.ps1) script, and set an alias  
```powershell
Set-Alias ls Get-ChildItem-Color -option AllScope -Force
```

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

