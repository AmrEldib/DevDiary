# Rename Downloaded Files using Context Menu

# Problem

There are lots of files that I download on regular basis and need to rename and move to their correct location. For example: Bank statements and bills.  
These files are predictable in their name, but I want to rename them to easily sort them and find them later.  
I also want to move them to the correct folder.  
I want to be able to simply right-click on the downloaded file, and execute one command that would:  
- Recognize which file it is.  
- Rename it.  
- Move it to where it should be filed.  
- (Optionally) Show up a notification of where it went.  

# Solution

I can use [AdvancedRenamer](https://www.advancedrenamer.com/) to create a preset for each category of files.  
This takes care of renaming the files.  

## Adding shortcut to Windows Context Menu

A quick solution is to use Windows SendTo menu.  
Simply place a shortcut in the SendTo folder. You can reach that by going to `shell:sendto` or `%APPDATA%\Microsoft\Windows\SendTo`.  
This is great because it involves no modification of the registry to add an entry to the Context Menu.  
However, it can only pass a single file to the target script.  

