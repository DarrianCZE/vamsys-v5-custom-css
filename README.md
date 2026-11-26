# Custom Stylesheet for the vAMSYS v5
This stylesheet contains an end to end solution made for the virtual airline SW Virtual, however based on the popular reception of previous version, I have decided to make this available to the public as well. The only thing which needs to be done, is to change your primary and secondary colors.

It restyles the **Phoenix** pilot interface (dashboard, PIREPs, dispatch, booking, maps, events, settings) in both **light and dark mode**.

## Download link
Download here: https://github.com/DarrianCZE/vamsys-v5-custom-css/releases

## How to use
- Change your VA colors in the first section of the CSS:

```
:root {
	--primary-rgb: 0,69,138;               /* Primary VA colour. Should be darker. */
	--secondary-rgb: 241,144,1;            /* Secondary VA colour. Should be brighter. */
	--primary-darkmode-color: 255,255,255; /* Text colour in dark mode. Any very bright colour. */
	--danger-rgb: 241,87,118;              /* Warning/danger colour, some shade of red. */
}
```

- Values are **RGB numbers separated by commas** (for example `0,69,138`), not hex codes.
- Import the stylesheet into the vAMSYS v5 Orwell Design section!

## Fine-tuning (optional)
From version 2.0, every colour decision lives in one place: the **design tokens** in section 2 of the file. There is one block for light mode (`:root`) and one for dark mode (`:root:is(.dark)`). Change a token once and every button, badge, card or label that uses it follows, in both modes. Some useful ones:

| Token | What it controls |
|---|---|
| `--sw-text` … `--sw-text-4` | Text colour, from strongest to weakest |
| `--sw-btn-bg` / `--sw-btn-hover-bg` | Filled buttons, badges and chips, and their hover |
| `--sw-accent` | Accent surfaces: the dispatch button, active tabs, highlighted cards |
| `--sw-on-fill` | Text on filled buttons and accent surfaces. In dark mode, `rgb(18,19,28)` gives much better contrast on a bright secondary colour. |
| `--sw-glass` | Opacity of the map sidebar cards |
| `--sw-danger` / `--sw-danger-bg` | Red text and red fills (danger alerts, Cancel Booking, MZFW exceeded), derived from `--danger-rgb` |
| `--sw-alert-bg` / `--sw-alert-border` | The dashboard welcome box (success alert) |
| `--sw-quiet-*` | Outlined secondary buttons (map buttons in dark mode, SimBrief Actions) |
| `--sw-alert-info-*` / `--sw-alert-warn-*` | Tinted info and warning panels (also the booked-flight card) |
| `--sw-link` | Links inside page content |

## What's new in 2.0.1 – 2.0.7
- **2.0.7:**
  - the dashboard welcome box uses the same tinted panel with a coloured left edge as the other alerts, in both modes;
  - danger colours are derived from `--danger-rgb` so white text on red buttons/alerts and red text are readable (~5.8:1);
  - dark mode uses one neutral text colour (page text matches labels and titles);
  - themed the leaderboard "Your Position" box, the live-map Help & Guide pop-up, PIREP map button labels and the Book Flight Map airport-card captions;
  - checked at phone width (375 px) as well, no horizontal scrolling.
  - Note: uses CSS `color-mix()` (all current browsers).
- **2.0.6 (accessibility):**
  - all text, including the faintest grey labels, now meets WCAG AA contrast (4.5:1) in both modes;
  - keyboard focus shows a 2px outline (primary colour in light mode, secondary in dark mode);
  - dark-mode top bar (clock, name, pilot ID) is brighter and readable.
- **2.0.5:** the booked-flight card on the dashboard is a tinted panel with an orange edge instead of a solid orange block.
- **2.0.4:**
  - aircraft picker card, dropdown and highlighted row match the theme;
  - the Create Booking bar uses the same grey as the other cards in dark mode;
  - booking page: Edit SimBrief OFP, Navigraph Charts and Download are quiet outlined buttons (Open OFP stays solid), field labels are softer than values, small outline buttons have a visible ring;
  - info and warning alerts are tinted panels with a coloured left edge, and links in page content use the theme colour.
- **2.0.3:** the Dispatch Flight button glows in the secondary colour instead of vAMSYS green.
- **2.0.2:** dark mode: Dispatch Flight is the one solid button on the Book Flight Map; the other map buttons are outlined.
- **2.0.1:** dark mode: the active dashboard tab is brighter than the others again, and the accepted PIREP count uses the neutral text colour.

## What's new in 2.0
- Rebuilt around design tokens, with each component written once instead of once per mode (about 600 lines instead of about 1,700).
- Fixed declarations that browsers silently ignored (wrong colour syntax, `0,6` instead of `0.6`, a `rgbaa(` typo).
- Danger stays red: danger alerts, the Cancel Booking and Cancel & Rebook buttons, and the MZFW-exceeded badge in dark mode.
- Dashboard PIREP counts: accepted and pending now use different colours in both modes.
- Dark mode:
  - dispatch cards use the same grey as the rest of Phoenix;
  - dispatch dropdowns are no longer filled orange;
  - the welcome box is a readable tinted panel.
- Grey text levels are ordered correctly: darker Tailwind step means stronger text.
- Themed elements that kept vAMSYS defaults:
  - the cargo meter;
  - map sidebar labels, icons and buttons;
  - airport buttons on the Book Flight Map;
  - the PIREP "Accepted" pill and the PIREP map buttons;
  - the OFP summary labels.

## Contributing
See [AGENTS.md](AGENTS.md) for the file structure, the rules for adding selectors and the known pitfalls.
