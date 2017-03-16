# Adding intellisence for Ember in VS Code

- Install [Ember Cli in VS Code extension](https://github.com/felixrieseberg/vsc-ember-cli)  
- Install [typings](https://www.npmjs.com/package/typings)  
`npm install -g typings`  
- Install Ember typings `typings install ember --source dt --save --global`  
    - We need to specify the source of where to get the typings file. We're getting it from dt (Definitely-Typed), the default source is npm.  
    - Ember is installed globally in npm, so its typings needs to be installed globally.  
- A new `typings` folder is created in the Ember project folder.  
