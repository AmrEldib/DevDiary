# manifest.json

To easily work with manifest.json files, add this property at the top of the JSON file:  
```
"$schema": "http://json.schemastore.org/webextension",
```
In VS Code, this enables auto-completion using schemas collected by [Schema Store](http://schemastore.org/json/).  
This is very helpful for common JSON files that follow a certain schema. It enables discovery.  

## manifest version and extension version

It's always `"manifest_version": 2`.  
This is the version of the manifest, not your web extension.  

`version: 1.0` is the version of your extension, and in this case, it's 1.0

## Icons

Provide icons with two sizes: 48 and 96  
If you want to provide SVG, read the [SVG section first](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/manifest.json/icons#SVG)  

## Folder structure

There's no specific folder structure for web extension. However, I hate having to think up a folder structure with every new project. I use this structure by default, but I make changes as needed:  
- css
- html
- js
- icons
- images
