# Problem
How to change the font for the Reader mode in Firefox?

# Solution
In the `userContent.css` file, add this CSS:  
```css
/* When serif font is selected */
body.serif {
font-family: "Noto Serif" !important;
}
/* When sans-serif font is selected */
body.sans-serif {
font-family: "Noto Sans Display" !important;
}
```
The CSS used in the Reader can be viewed at `chrome://global/skin/aboutReader.css`

## Source 
[Superuser - How to change font of reader view in Firefox](https://superuser.com/questions/975920/how-to-change-font-of-reader-view-firefox/1146113#1146113)  
[How can I add the CSS styles used by Firefox reader mode?](https://support.mozilla.org/en-US/questions/1069513)