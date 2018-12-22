# Problem

How to find the device drivers in Linux

# Solution

- Use `lspci -v` to list PCI devices with Verbose output.
- Go through the list and find the device you want to find its driver
- One of the properties is "Kernel driver in use".
- The first number of each entry is the bus number, pick up the bus number for the device you want to find more info about.
- You can do `lspci -vv -s [BUS NUMBER]` to find detailed info about this specific device.
    - `-vv` for Very Verbose
    - `-s` for Slot (specified by bus number. ex: `05:00.0`)
    - Use `sudo` to get all info. Otherwise, you might get some permission denied errors.

## Resources
- [Decoding PCI data and lspci output on Linux hosts](https://prefetch.net/articles/linuxpci.html) explains the details of the output from `lspci` as:  
```
Field 1 : 05:00.0 : bus number (05), device number (00) and function (0)
Field 2 : 0200    : device class
Field 3 : 14e4    : vendor ID
Field 4 : 1659    : device ID
```