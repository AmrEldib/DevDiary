# Easily migrate to latest version of Node.js

# Problem

I use [nvm](https://github.com/creationix/nvm/) to manager different versions of Node.js  
However, when upgrading to the latest version, I always miss the global packages I installed earlier.  

# Solution

nvm actually already has a solution for this. When installing the latest version, use:  
```bash
nvm install latest --reinstall-packages-from=<VERSION>
```
Where `<VERSION>` is the version you're migrating from.  
This will install the latest version of Node.js and then install all the global packages you had in the earlier version.  

