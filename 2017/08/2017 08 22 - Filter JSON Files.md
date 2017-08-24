# Filter JSON Files

## JSONata
[JSONata](http://docs.jsonata.org) is a lightweight query and transformation language for JSON data (even though it has the worst name).  
It uses semantics like XPath.  
There's a [playground](http://try.jsonata.org/) to try it out.  
If you pass a selection statement, it'll return the value in the document.  
Try: `Account.Order[0].OrderID`  to get `order103`  
If you pass a expression to evaluate, it'll return true or false.  
Try: `Account.Order[0].OrderID = "order103"` to get `true`  
Try: `Account.Order[0].OrderID = "order100"` to get `false`  

## Read multiple files
Here's a [snippet](https://github.com/zishon89us/node-cheat/blob/master/files/read_dir_files.js) with two ways to read multiple files in Node.js. This snippet was mentioned in this [StackOverflow answer](https://stackoverflow.com/a/35824248/463).  
The first one uses [read-multiple-files](https://github.com/shinnn/read-multiple-files) package.  
The other uses the [map](https://caolan.github.io/async/docs.html#map) function in [async](https://caolan.github.io/async/) package.  

I went with async because I could have access to the file name after reading is complete.  

## Command arguments  
To parse command arguments, I used [minimist](https://github.com/substack/minimist) which is lightweight and straightforward.  
For an option with more features, use [yargs](https://github.com/yargs/yargs).  

## Turning Node script to executable command  
The [`bin` property](https://docs.npmjs.com/files/package.json#bin) in the `package.json` file lets you turn a script into an executable command.  
You need to add the line `#!/usr/bin/env node` at the top of the script.  
However, [this might not work on Windows](https://stackoverflow.com/a/10398567/463).  