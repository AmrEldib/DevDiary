# Problem

Chocolatey keeps asking for approval when installing package.

# Solution

To bypass installation prompt, turn on `allowGlobalConfirmation`.  

`choco feature enable -n=allowGlobalConfirmation`

To see other features that could be controlled, use `choco feature -h`