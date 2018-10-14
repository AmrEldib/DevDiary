# Firefox configurations to improve privacy and performance

[Source](https://gist.github.com/0XDE57/fbd302cef7693e62c769)  


## Control and Misc.
`dom.event.contextmenu.enabled = false`  
Don't allow websites to prevent use of right-click, or otherwise messing with the context menu.  
This causes problems for websites that legitimately blocks the context menu to show their own context menu.

`dom.event.clipboardevents.enabled = false`  
Don't allow websites to prevent copy and paste.  
Disable notifications of copy, paste, or cut functions.  
Stop webpage knowing which part of the page had been selected.

`network.IDN_show_punycode = true`  
Show punycode. Help protect from character 'spoofing' eg: `xn--80ak6aa92e.com -> аррӏе.com`  
Source: [IDN homograph attacks](https://www.xudongz.com/blog/2017/idn-phishing/)

## Privacy Settings

`browser.send_pings = false`  
Prevent website tracking clicks.
		
`browser.send_pings.require_same_host = true`  
Only send pings if send and receiving host match (same website).

`dom.battery.enabled = false`  
Disable website reading how much battery your mobile device or laptop has.

`
extensions.pocket.enabled = false
extensions.pocket.site = blank
extensions.pocket.oAuthConsumerKey = blank
extensions.pocket.api = blank
`  
Disable 3rd party closed-source Pocket integration.  
Note, this is browser.pocket.enabled for older versions of firefox

## Performance 
On a machine that has more than 8 GB of RAM: 
- Go to _Options_ > _Performance_
- Uncheck _Use recommended performance settings_
- Change _Content process limit_ to a higher number than 4.
[Full details](https://support.mozilla.org/en-US/kb/performance-settings)

