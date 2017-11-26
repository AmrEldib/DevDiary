# Move Synology Apps between Volumes

# Problem

Need to move apps from one Synology volume to another before removing that volume.  

# Solution

[This guide](http://www.mcleanit.ca/blog/synology-move-application-volumes/) outlines the solution.  

- Stop the app using the Package Center, or using this command  
```bash
sudo /var/packages/[app_name]/scripts/start-stop-status stop
```

- Then, move the app and change the references  
```bash
# Move the app files from the old volume to the desired one.
sudo mv /volume1/@appstore/[app_name] /volume3/@appstore/
 
# Delete the obsolete Symlink pointing at the old app path
sudo rm -fv /var/packages/[app_name]/target
 
# Create a new Sim link pointing at the new, correct app path.
sudo ln -s /volume3/@appstore/[app_name] /var/packages/[app_name]/target
```