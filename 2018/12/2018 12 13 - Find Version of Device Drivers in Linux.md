# Problem

How to find version number of installed driver for a certain device.

# Solution

- First, find the driver for the device using `lspci`
- The driver name should be the name of a kernal module
- Use `lsmod` to list all modules
- Use `lsmod | grep [MODULE NAME]` to make sure the module is loaded
- Use `modinfo [MODULE NAME]` to list the details of the module.
- Use `modinfo [MODULE NAME] | grep -i version` to only list the lines that has the word *version*