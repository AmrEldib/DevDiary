# Problem

KeepassXC looks wrong on HiDPI screen

# Solution

QT (which KeepassXC is built on) can use an environment variable to fix auto scaling on HiDPI screens.

Add the environment variable `QT_AUTO_SCREEN_SCALE_FACTOR` with value `1`

There's an [ongoing bug on this issue](https://github.com/keepassxreboot/keepassxc/issues/1888)