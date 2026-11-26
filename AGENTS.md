# AGENTS.md

Guidance for AI coding agents (and humans) working on this repository.

## What this is

A single custom stylesheet, `SW_Virtual_CSS_vAMSYS_v5.css`, that rebrands the **Phoenix** pilot
interface of [vAMSYS](https://vamsys.io) v5 for SW Virtual. It is public: other virtual airlines
download it from GitHub releases, change four colour values and paste it into
**Orwell → Design → Custom CSS**. There is no build step, no package manager and no tests;
the file is pasted into vAMSYS as-is.

## Hard rules

- **Phoenix only.** Style and test the pilot-facing pages (`/phoenix/...`). Do not open, test against
  or automate **Orwell** or any other admin interface.
- **One file.** Keep everything in `SW_Virtual_CSS_vAMSYS_v5.css`. vAMSYS accepts one CSS blob; no
  `@import`, no external fonts or assets.
- **Keep the user contract.** Section 1 (`--primary-rgb`, `--secondary-rgb`,
  `--primary-darkmode-color`, `--danger-rgb`) must stay at the top and stay comma-separated RGB
  triplets. The README tells users to edit only those lines.
- **Bump `Version:`** in the header comment for every released change, and mention it in the commit
  message (history uses messages like `1.20 fix dispatcher rmk`).

## How the stylesheet is organised (v2.0)

1. **Brand colours** - the four user-editable RGB triplets.
2. **Design tokens** - `--sw-*` variables, defined once in `:root` (light) and once in
   `:root:is(.dark)` (dark). Every colour decision lives here:
   `--sw-text`, `--sw-text-2..4` (text steps, strongest to weakest), `--sw-btn-bg`,
   `--sw-btn-hover-bg`, `--sw-accent`, `--sw-accent-hover`, `--sw-on-fill`, `--sw-danger`,
   `--sw-danger-bg`, `--sw-tint`, `--sw-glass`, `--sw-icon-bg`, `--sw-meter`, `--sw-focus-ring`,
   `--sw-gradient-from`, `--sw-alert-*`, and dark-only `--sw-surface`, `--sw-field-bg`,
   `--sw-field-border`.
3. **vAMSYS variable remap** - overrides vAMSYS/Filament/Tailwind variables (`--primary`,
   `--success`, `--gray-*`, `--tw-*`). Values are RGB triplets because vAMSYS consumes them as
   `rgb(var(--x))`.
4. **Components** - each component written **once**, coloured **only through tokens**, grouped by
   role (text, filled buttons, hover, text-only dispatch actions, accent surfaces, alerts, map,
   dispatch). Do not add a second `:is(.dark *)` copy of a component rule; change the token instead.
5. **Dark-only overrides** - Tailwind `dark:` utility classes and surfaces that exist only in dark
   mode (`.dark\:text-white:is(.dark *)`, dispatch card surfaces, ...).

### Adding or changing a rule

- New element that should look like existing text, button, hover, etc.: **add its selector to the
  matching group** in section 4. Don't write a new rule with literal colours.
- Different look in dark mode: add or change a **token** in section 2, not a dark copy of the rule.
- Never put literal brand colours in components; use `var(--sw-*)` or `rgb(var(--primary-rgb))`.

## Pitfalls that have bitten this file before

- **Comma vs slash colour syntax.** Tokens are comma triplets. `rgb(var(--primary-rgb) / 0.5)`
  expands to `rgb(0,69,138 / 0.5)` and is **invalid** (the declaration is silently dropped). Use
  `rgba(var(--primary-rgb), 0.5)`.
- **Decimal commas.** `rgb(var(--x),0,6)` (meaning 0.6) is invalid. Always `0.6`.
- **Bare triplets as colours.** `color: var(--gray-800)` gives `color: 49, 58, 70` - invalid. Wrap
  it: `rgb(var(--gray-800))`.
- **Selector lists.** `.a, .b:hover` styles every `.a`, not only on hover. Write `.a:hover, .b:hover`.
  One invalid selector in a list drops the whole rule.
- **Cascade order matters**, because every rule is `!important` and most have equal specificity:
  - The weaker text steps (`.text-gray-400/500/600`) come **before** the strongest-step group, so an
    element with both `text-gray-500` and `text-gray-900` (the active dashboard tab) gets the
    stronger one.
  - The text-only dispatch actions come **after** the filled-button and hover groups.
- **Semantic colours.** Keep danger red (`--danger-rgb`) for danger: alerts, `btn-danger-outline`
  (Cancel Booking), MZFW exceeded, callsign taken. Dark `--success` stays the secondary colour,
  because cards with `bg-success` use it as a background. The dashboard *text* is fixed separately
  with `.text-success:is(.dark *)`.
- **Broad utilities.** `.text-white`, `.bg-transparent` and `.hover\:text-white` in dark mode catch
  many elements. `ui-select` (dispatch dropdowns) is explicitly excluded from `.bg-transparent`.
- **Map pages re-initialise on theme change.** Toggling `.dark` on `/phoenix/flight-center/book`
  or the flight map reloads the map and clears the selected airport or route.
- **Charts** on PIREP pages are drawn on canvas; CSS cannot recolour their lines.

## How to test a change

There is no automated suite. Check in a browser, signed in to Phoenix:

1. Paste the CSS into a test copy or preview it. In DevTools, replace the text of
   `<style id="custom-va-style">` (the element vAMSYS renders the custom CSS into) and compare.
2. Dark mode: vAMSYS uses the Tailwind `dark` class on `<html>`. Add it with
   `document.documentElement.classList.add('dark')` to preview without changing account settings.
3. Validity: after loading, check that no declaration was dropped. Resolve `var()` values and run
   `CSS.supports(prop, value)` on each, or compare computed colours before and after.
4. Pages worth covering (each in light and dark):
   - dashboard (`/phoenix`)
   - PIREPs list and a PIREP detail page
   - dispatch: empty, with all sections expanded, and with the OFP summary open
   - booking page (`/phoenix/flight-center/booking/<id>`)
   - flight map with a flight selected
   - Book Flight Map with an airport and a route selected
   - settings, events, NOTAMs
5. Never click irreversible actions while testing: Create Booking, Cancel Booking, Generate OFP,
   Send to VATSIM, comment or claim forms.

## Known gaps

- `card-primary`, `card-info`, `card-warning` and `card-danger` have not been seen on any Phoenix
  page during testing. Their rules are kept but unverified.
- `.fal` / `.fa-light` hover rules target Font Awesome Light, which vAMSYS currently uses only for
  the top-bar bulb.
- Contrast: white text on the secondary orange is about 2.4:1. Setting `--sw-on-fill` to
  `rgb(18,19,28)` in the dark token block gives about 7:1. Left as white on purpose; it is a
  branding decision.
