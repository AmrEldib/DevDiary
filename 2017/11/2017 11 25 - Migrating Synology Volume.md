# Migrating Synology Apps and Shared Folders between Volumes

# Problem 

After moving apps from Volume1 to Volume4, some apps can't start. This includes: CardDav Server, Sickbeard, and Couchpotato.  
Apps were moved from one volume to another following the steps in [this guide](http://www.mcleanit.ca/blog/synology-move-application-volumes/)

# Solution

Some references aren't updated when apps are moved between volumes.  
Those references are in the folder `/usr/local`  
Go to `/usr/local`, update the references by deleting it, and recreating it.  
Here are the references I updated:  
- /usr/local/couchpotatoserver  
- /usr/local/git  
- /usr/local/python  
- /usr/local/sickbeard-custom  
- /usr/bin/easy_install  

```bash
# Delete the obsolete Symlink pointing at the old app path
sudo rm -fv /usr/local/couchpotatoserver
 
# Create a new Sim link pointing at the new, correct app path.
sudo ln -s /volume4/@appstore/couchpotatoserver /usr/local/couchpotatoserver
```

## CardDAV Server

Even after I update the links above, CardDAV Server still wouldn't start.  
I found that it depends on the package _Python Module_ which has too many symlinks all over the place (for example, in `/usr/lib`).  
I found that it would be too much work to update all these symlinks.  
I broke the _Python Module_ package by removing the symlink to it from `/var/packages/PythonModule/target/`  
```bash
sudo rm -fv /var/packages/PythonModule/target
```
This prompted Package Center to offer a _Repair_ button for this package. I clicked _Repair_ which reinstalled the package, and updated all the symlinks.  
For this to work, I had already changed the install location of new packages to the new volume4.  
To update the install location, go to Package Center > Settings > General > Default Volume.  

## Synology Drive

Synology Drive has a database. Use the _Drive Admin Console_ to move this database to the new volume. Use the Settings tab to do this.  


