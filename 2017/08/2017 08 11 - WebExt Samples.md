# Firefox WebExtensions

[Samples on GitHub](https://github.com/mdn/webextensions-examples)  

## web-ext

[web-ext](https://github.com/mozilla/web-ext) is a command line tool built by Mozilla to help speed up various parts of extension development.  
[Get it](https://www.npmjs.com/package/web-ext) from npm:  
```npm install --global web-ext```  

Test that web-ext was installed:  
```web-ext --version```

To test an extension, browse to the root folder of the extension and run:  
```web-ext run```  
This starts Firefox and loads the extension temporary into it.  
_To load extensions manually, use the [about:debugging page](https://developer.mozilla.org/en-US/docs/Tools/about:debugging#Add-ons)_  

Web-ext also watches the folder for changes and reloads the extension when you save one of the files.  

It's better to use [Firefox Developer edition](https://www.mozilla.org/en-US/firefox/developer/) and not your main Firefox browser. This keeps your browser running, and makes sure your debugging isn't affected by other extensions.  
To do this, run:  
```web-ext run --firefox="C:\Program Files\Mozilla Firefox\firefox.exe"```  

To further isolated your debugging, you can run using a specific profile:  
```web-ext run --keep-profile-changes  --firefox-profile=your-custom-profile```  
_Notice that --keep-profile-changes saves changes in the profile across sessions_  

To open the browser console on the browser startup, use:  
```web-ext run --browser-console```  

You can also set the start URL:  
```web-ext run --start-url www.mozilla.com```  

Sample command to start debugging in Developer edition and with console window open:  
```web-ext run --firefox="C:\Program Files\Firefox Developer Edition\firefox.exe" --browser-console```  

Once you settle on how your optimum config for web-ext, store that command in a `debug.bat` file (or any other name or extension)  and run every time you want to start debugging.  

## manifest.json

