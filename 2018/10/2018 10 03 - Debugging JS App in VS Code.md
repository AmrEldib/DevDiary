ToDo:

- Launch specific browser when starting to debug
    - We'll use Firefox Developer Edition. This should separate my browsing history and settings from development work.
    - Installed VS Code extension: Debugger for Firefox
    - Read on [how to configure it](https://marketplace.visualstudio.com/items?itemName=hbenl.vscode-firefox-debug)
    - Two configurations were used
        ```json
            "configurations": [
                {
                    "name": "Launch index.html",
                    "type": "firefox",
                    "firefoxExecutable": "C:\\Program Files\\Firefox Developer Edition\\firefox.exe",
                    "firefoxArgs": [
                        "--devtools"
                    ],
                    "reloadOnChange": {
                        "watch": "${workspaceFolder}/**/*.js",
                        "ignore": "**/node_modules/**"
                    },
                    "request": "launch",
                    "reAttach": true,
                    "file": "${workspaceFolder}/index.html"
                },
                {
                    "name": "Launch localhost",
                    "type": "firefox",
                    "firefoxExecutable": "C:\\Program Files\\Firefox Developer Edition\\firefox.exe",
                    "firefoxArgs": [
                        "--devtools"
                    ],
                    "reloadOnChange": {
                        "watch": "${workspaceFolder}/**/*.js",
                        "ignore": "**/node_modules/**"
                    },
                    "request": "launch",
                    "reAttach": true,
                    "url": "https://localhost/myapp/",
                    "webRoot": "${workspaceFolder}"
                }
            ]
        ```
    - Note the use of the `firefoxExecutable` property to specify the use of Firefox Developer Edition instead of default Firefox.
    - Firefox has also been configured to open the devtools when it starts. This is done via the `firefoxArgs` property. See the full [list of Firefox arguments](https://developer.mozilla.org/en-US/docs/Mozilla/Command_Line_Options).
- Hit breakpoints
    - Use Breakpoints panel.
- Inspect values while app is running
    - Use Watch panel.
- Skip files
    - Some code files are not meant to be debugged (like 3rd party).
    - VS Debugger for Firefox allows for [skipping/blackboxing files](https://github.com/hbenl/vscode-firefox-debug#skipping-blackboxing-files)
- Debug minified code
- Auto-refresh page when code is updated (Live reload)
    - Done via the `reloadOnChange` property.
