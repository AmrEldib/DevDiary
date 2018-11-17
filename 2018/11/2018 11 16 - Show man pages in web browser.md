# Problem

Using `man` command displays the documentation in the terminal which can be difficult to read, and very difficult to have the docs open while writing the command.  

# Solution

Instead, export the result of the `man` command to HTML and open it a browser.  
To do this, the `groff` package needs to be installed.  
Groff (GNU troff) is a document-formatting system.  
```bash
sudo dnf install groff.x86_64 groff-doc.noarch
```
Then use this command to open the result in Firefox
```bash
man -Hfirefox dnf
```
To set Firefox as the default browser, use:
```bash
export BROWSER=firefox
```
Note: add this line in `.zshrc` file to run it each time.

then use
```bash
man -H dnf
```

Add `alias docs="man -H"` to `.zshrc` to create an alias.


[Source](https://askubuntu.com/questions/339255/how-do-i-make-man-pages-open-in-a-web-browser)