# Problem

The context menu in Firefox doesn't have any icons. It would be nice to add icons that easily show which command is which.  

# Solution

You can use `userChrome.css` to edit the looks of Firefox UI beyond what's possible to WebExtensions.  
There's a subreddit for [FirefoxCSS](https://www.reddit.com/r/FirefoxCSS/). It has a [tutorial](https://www.reddit.com/r/FirefoxCSS/comments/73dvty/tutorial_how_to_create_and_livedebug_userchromecss/) for how to create `userChrome.css` and preview styles before applying them. 

Create the userChrome.css

    Open about:support
    Click on "Profile Folder" -> "Open Folder"
    Create a sub-folder named "chrome"
    Change into the new folder
    Create a file named "userChrome.css"
    Add some rules
    Restart Firefox

Live-Testing styles
Pre-setup

Before being able to try styles, you need to enable two developer options (only do this once). To do that:

    Press Ctrl + Shift + I on Win/Linux or Cmd + Opt + I on Mac
    Click on the cog that appears in a right or left top corner, next to other buttons.
    Scroll down to Advanced Settings and check the settings "Enable browser chrome and add-on debugging toolboxes" and "Enable remote debugging".
    Close the developer tools panel and proceed with next tutorial
    Use the Inspector tab in the developer tools to find the CSS selectors for the elements you want to edit

Testing a style

    Press Ctrl + Alt + Shift + I on Win/Linux or Cmd + Opt + Shift + I on Mac
    A permission dialog will prompt you to allow remote debug, accept
    Click on the tab Style Editor, choose file userChrome.css on the sidebar
    Choose the style you want to preview from this repository, copy the code
    Scroll down on the development tools window textbox, paste the code
    You should see the style being applied. If you like what you see, you can click Save, otherwise it will disappear after restarting the browser.

userChrome.org has some [good starting points](https://www.userchrome.org/what-is-userchrome-css.html)  

## Setting up CSS files for better organization

You can have a separate CSS files for each edit you want to make instead of adding everything into one big file.  
Create a file for each change, then use `@import url("filename.css");` to import this file into `userChrome.css`.  