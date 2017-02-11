# Install Jekyll on Windows

## Problem

Need to install Ruby and Jekyll to preview blog changes before publishing them.  

## Solution

- [Guide](http://jekyllrb.com/docs/windows/#installation)  
- Install Ruby via Chocolatey  
`choco install ruby -y`  
- Installing Ruby modifies PATH enviroment variable. Restart the command shell for this to take effect.
- Install Jekyll as a Ruby package.  
`gem install jekyll`  
- I ran into an error: `ERROR:  Could not find a valid gem 'jekyll' (>= 0) in any repository`  
- I needed to [check if `rubygems.rog` is actually added to gem sources](http://stackoverflow.com/a/9962847/463).  
- Check gem sources  
`gem sources`  
- Add rubygems.org as a source   
`gem sources --add https://rubygems.org/`  
- This caused an error  
```
Error fetching https://rubygems.org/:  
        SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://api.rubygems.org/specs.4.8.gz)
```
- Try [re-installing Ruby Gems](http://stackoverflow.com/a/27641786/463)  
    - Go to [Ruby Gems Downloads](http://rubygems.org/pages/download)
    - Download the latest zip file
    - Unzip it
    - run "ruby setup.rb" in unzipped folder
    - now run gem install command
- Now, I'm getting another error:  
```
ERROR:  While executing gem ... (Errno::EACCES)
    Permission denied @ rb_sysopen - C:/Users/Amr/.gemrc
```
- After trying so many things, this was finally resolved by deleting the `.gemrc` file. The `gem` command created a new file with the appropriate permissions.  
- Now, try again `gem sources --add https://rubygems.org/`  
- Install Jekyll  
`gem install jekyll`
- Change codepage to avoid character encoding issues in Windows  
`chcp 65001`  
