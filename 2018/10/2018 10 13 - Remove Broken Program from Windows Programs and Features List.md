# Problem
A program was uninstalled, but it's still stuck in the _Programs and Features_ list.

# Solution
[Source](https://superuser.com/questions/401511/how-to-remove-a-broken-program-from-the-programs-and-features-list-in-windows-7)  

The programs showing in the Programs and Features list are generated from the registry keys under: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall` 

32 bit programs installed on a 64 bit machine will be in the `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall` 
