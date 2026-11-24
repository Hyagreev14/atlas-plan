# ATLAS design system

**Status:** Direction and specification in progress. Exact token values must be selected and tested in Figma; this document does not pretend those values are final.

## Design goals

ATLAS should feel like a focused professional developer workstation: calm, precise, capable and efficient. It should avoid both generic consumer-app styling and an overly dense control-room aesthetic.

## Visual direction

- Dark-first interface with a complete light theme.
- Neutral surfaces; one restrained primary accent and carefully limited semantic colours.
- Strong text hierarchy and predictable alignment.
- Compact information density with enough breathing room for long sessions.
- Consistent icon family and stroke weight.
- Subtle borders and elevation; avoid excessive gradients, glow and glass effects.
- Use motion sparingly and consistently.

## Token groups

Create Figma variables for the following semantic groups. Select actual values in the Figma file and document them here after contrast testing.

### Colour
- `surface/canvas`, `surface/raised`, `surface/sunken`, `surface/overlay`
- `text/primary`, `text/secondary`, `text/tertiary`, `text/inverse`
- `border/subtle`, `border/default`, `border/strong`, `focus/ring`
- `accent/primary`, `accent/hover`, `accent/pressed`
- `status/success`, `status/warning`, `status/danger`, `status/info`

Status must never rely on colour alone; pair it with text or an icon.

### Typography
Define a compact type scale for display/page title, section heading, body, secondary body, label, caption and code/monospace. Specify font family, size, weight, line height and letter spacing. Use a readable system-compatible stack where possible; do not assume a font exists on every target machine.

### Spacing and sizing
Use a consistent base spacing scale and document the chosen values. Define standard control heights, icon sizes, panel padding, sidebar width, top-bar height, dialog widths and minimum window dimensions. Avoid arbitrary one-off values.

### Shape and elevation
Define radii for small controls, cards, panels and dialogs. Define border and shadow levels with restraint. Ensure the design remains clear when shadows are unavailable or reduced.

### Motion
Define short, medium and long motion tokens, easing curves and reduced-motion behaviour. Motion should communicate hierarchy, continuity or state change. Do not animate every hover or panel.

## Layout rules

- Establish a minimum usable window size based on real content, then test smaller sizes.
- Use a stable app shell with predictable navigation and content regions.
- Allow content areas to scroll independently only when it improves usability.
- Avoid horizontal overflow in ordinary workflows.
- Use responsive breakpoints for compact, standard and wide desktop windows; test actual Electron window sizes.
- Keep primary actions discoverable and destructive actions visually distinct.

## Themes

Design dark and light themes using semantic variables. Components must consume semantic tokens rather than hard-coded theme colours. Check charts, code blocks, status indicators, borders, focus rings and disabled states in both themes.

## Accessibility baseline

- Meet WCAG AA contrast targets where applicable.
- Keep text readable and allow OS display scaling.
- Provide visible keyboard focus and logical tab order.
- Do not communicate state using colour alone.
- Avoid tiny hit targets; make frequent controls comfortably clickable.
- Respect reduced-motion preferences in implementation.
- Use clear labels and accessible names for icon-only controls.

## Token handoff

Before implementation, export or transcribe the approved variables into a token reference with token name, light value, dark value, intended use and contrast notes. The React implementation should consume shared tokens rather than re-create values screen by screen.
