# Problem

Point Synology's Photo station to use an existing folder rather than its own `photo` folder.

# Solution

Using a folder other than `photo` for Synology Photo Station is not possible.  
However, you can achieve the same result by mounting your existing folder as the `photo` folder.  
To do so, you need to access your Synology via SSH.  
SSH service must be enabled to do this. Go to `Control Panel` and enable access over SSH.  
Then, use a Linux terminal or Window's PuTTY or Bash Shell to access Synology over SSH.  
Access using the `root` account which has the same password as `admin`.  
Use this command to mount your folder:  
```bash
mount --bind /volume2/Pictures /volume1/photo
```
However, once your NAS reboots, this mount will go away. To save it across reboots. Add the same command to this file `/etc/rc.local`.  
Use Vim to modify this file, and add the line. 


# Sources
[Change folders for Synology media server](http://www.king-foo.com/2010/06/change-folders-for-synology-media-server/)  
[Synology forums - How to point Photo Station to existing folder](https://forum.synology.com/enu/viewtopic.php?t=58546)  