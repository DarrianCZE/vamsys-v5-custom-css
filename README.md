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
