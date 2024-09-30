# Custom Stylesheet for the vAMSYS v5
This stylesheet contains an end to end solution made for the SW Virtual virtual airline, however based on the popular reception of previous version, was made available to the public, where the only thing you need to do, is to change your primary and secondary colors.

## Download link
Download here: https://github.com/DarrianCZE/vamsys-v5-custom-css/releases

## How to use
- Change your VA colors in the first section of the CSS:

```
:root{ /* Variable section of the CSS, edit your colors only here: */
	--primary-rgb: 0,69,138; /* Primary VA Color in RGB format. Should be darker. */
	--secondary-rgb: 241,144,1; /* Secondary VA Color in RGB format. Should be brighter. */
	--primary-darkmode-color: 255,255,255; /* Primary Dark mode color. In this case, it's white, but theoretically it can be any very bright color. */
}
```
- Import the stylesheet into the vAMSYS v5 Orwell Design section!

# Changelog:
- 1.0
	- Initial Release
- 1.1
	- Tweaked button colors on the Dispatch page. 
	- Tweaked border color of the buttons on the booking page.
	- Added custom colors to the Cancel booking buttons. 
	- Tweaked Success badge border color.
	- Tweaked Primary button hover color
 	- Better color brightness for primary and sucess buttons in Dark mode
- 1.2
	- Fixed Border color in the Flight Map filtering section in the Dark Mode - credits to Lukas for helping!
	- Fixed Text color "Start typing to search..." in the Flight Map filtering - credits to Lukas for helping!
- 1.3
	- Early implementation of the PIREP cards styling
	- Alert - Danger styling
- 1.4
	- Add flight progress bar styling in dark mode
- 1.4.1
	- Tweaked the Alert Danger brightness in the Light mode
- 1.4.2
	- Tweaked the brightness of the Alert Success
- 1.5
<<<<<<< HEAD
	- Various tweaks in the Dark mode and Light mode, especially regarding the color brightness in the Dark mode.
- 1.6
	- Various color fixes and tweaks
	- Added Card - Info styling
- 1.7
	- Changed airport code badge on the Flight Map
=======
	- Various tweaks in the Dark mode and Light mode, especially regarding the color brightness in the Dark mode.
>>>>>>> parent of f1cb7b9 (1.6)
