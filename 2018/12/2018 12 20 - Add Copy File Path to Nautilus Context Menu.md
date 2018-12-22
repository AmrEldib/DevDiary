# Problem



# Solution

- Install `xclip` to copy text into clipboard using this command.
`dnf install xclip`
- Any script added at this location is loaded under the *Scripts* menu in Nautilus context menu
/home/{USER NAME}/.local/share/nautilus/scripts  
- Create a script at that folder, name it `Copy Path`
- In the script permissions, mark it as `Allow executing file as program`
- The content of the script is:
```bash
#!/bin/bash    
echo -n $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS | xclip -selection clipboard
```
- Nautilus scripts has a number of variables listed [here](https://help.ubuntu.com/community/NautilusScriptsHowto):
    - `NAUTILUS_SCRIPT_SELECTED_FILE_PATHS`: newline-delimited paths for selected files (only if local) 
    - `NAUTILUS_SCRIPT_SELECTED_URIS`: newline-delimited URIs for selected files 
    - `NAUTILUS_SCRIPT_CURRENT_URI`: current location 
    - `NAUTILUS_SCRIPT_WINDOW_GEOMETRY`: position and size of current window 