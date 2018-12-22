# Problem

When opening an AppImage, it always asks to add a .desktop file to integrate with the applications menu. Sometimes this is useful, but sometimes a file is already added. How can I disable this dialog?

# Solution

Add a file named `no_desktopintegration` under `$HOME/.local/share/appimagekit/`

[Source](https://github.com/electron-userland/electron-builder/issues/1962#issuecomment-352531262)