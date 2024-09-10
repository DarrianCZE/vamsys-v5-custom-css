# Custom Stylesheet for the vAMSYS v5
This stylesheet contains an end to end solution made for the SW Virtual virtual airline, however based on the popular reception of previous version, was made available to the public, where the only thing you need to do, is to change your primary and secondary colors.

# How to use
- Change your VA colors in the first section of the CSS:

```
:root{ /* Variable section of the CSS, edit your colors only here: */
	--primary-rgb: 0,69,138; /* Primary VA Color in RGB format. Should be darker. */
	--secondary-rgb: 241,144,1; /* Secondary VA Color in RGB format. Should be brighter. */
	--primary-darkmode-color: 255,255,255; /* Primary Dark mode color. In this case, it's white, but theoretically it can be any very bright color. */
}
```
- Import the stylesheet into the vAMSYS v5 Orwell Design section!

# Known Issues
- Dark mode
	- Border color in the Flight Map filtering, when the filter is highlighted, doesn't change to the primary or secondary color. I unfortunately had no luck finding out why.
	- Text color "Start typing to search..." in the Flight Map filtering, when the filter is highlighted, doesn't change to the primary or secondary color. I unfortunately had no luck finding out why.

# Changelog:
- 1.0
	- Initial Release
- 1.1
	- Tweaked button colors on the Dispatch page. 
	- Tweaked border color of the buttons on the booking page.
	- Added custom colors to the Cancel booking buttons. 
	- Tweaked Success badge border color.
	- Tweaked Primary button hover color