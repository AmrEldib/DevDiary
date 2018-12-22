# Problem

With 100% HiDPI scaling (and the absense of fractional scaling), Chrome/Chromium UI and web pages can seem very small. How to make it look better?

# Solution

- In a terminal, enter `sudo gedit /usr/share/applications/google-chrome.desktop` or `sudo gedit /usr/share/applications/chromium-browser.desktop`
- Find this line: `Exec=/usr/bin/chromium-browser %U`
- Change it to: `Exec=/usr/bin/chromium-browser --force-device-scale-factor=1.3 %U`
- Instead of 1.3, you can enter the value you like.

[Source](https://superuser.com/questions/1116767/chrome-ui-size-zoom-levels-in-ubuntu-16-04)