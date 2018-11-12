# Problem
How to turn webapp to a desktop app on Linux

# Solution 
Use [Nativefier](https://github.com/jiahaog/Nativefier/)  

When using Nativefier on Linux, note that:  

1. When you run it in the terminal, it installs the app in the current folder. 

2. It fails to add an icon to the applications menu. See [this bug](https://github.com/jiahaog/nativefier/issues/204)  

To fix this, a .desktop file should be added at this folder
`/home/$USER/.local/share/applications`

The .desktop file content is like this:
```
[Desktop Entry]
Comment=Whatsapp created with nativefier
Terminal=false
Name=Whatsapp
Exec=/the/folder/of/the/Webapp/Whatsapp
Type=Application
Icon=/the/folder/of/the/Webapp/resources/app/icon.png
Categories=Network;
```