# Problem
When running Ember, I get an error `Error: Cannot find module 'internal/fs'`
I have the latest version of Ember, and the latest version of Node.js 7.7.2 and npm 4.1.2

# What I tried
I've tried the following with no effect:  
- Uninstalling and re-installing Ember.  
- Cleaning npm cache. `npm cache clean`  

This seems to be like a common issue, and no limited to Ember. [SO thread](http://stackoverflow.com/questions/40308623/cannot-find-module-internal-fs-afer-upgrading-to-node-7).  
There's a suggestion to install [npm-check-updates](https://github.com/tjunnone/npm-check-updates).  
However, running this package immediately fails.  
An [npm issue on this error](https://github.com/npm/npm/issues/14232)

Tried removing all global packages, cleaning npm cache and reinstalling Ember. This didn't resolve the issue.

Tried reinstalling npm and node.js. Still no luck.  

# Solutions
Tried installing Ember using Yarn. This worked.  
Tried switching to Node.js LTS 6.10.0. This worked.  

