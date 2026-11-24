# Component library

Build and maintain reusable Figma components before duplicating patterns across screens. Use component properties and variants for meaningful states; avoid creating a separate unrelated component for every colour or label.

## Initial component inventory

### Navigation
- App sidebar and navigation item.
- Section heading and breadcrumb.
- Top bar, workspace switcher and tab strip.
- Search/command entry.

### Actions
- Primary, secondary, tertiary and destructive buttons.
- Icon button with tooltip specification.
- Split button and menu item.
- Checkbox, radio, switch and segmented control.

### Content
- Project card and project row.
- Tool/application row.
- Status indicator, badge and metadata label.
- Empty state, skeleton/loading placeholder and error panel.
- Activity item and notification.

### Containers
- Card, panel, popover, dropdown, modal/dialog and side panel.
- Toast/snackbar and confirmation prompt.
- Table, list, filter bar and pagination where needed.

### AI and permissions
- Message bubble, composer and attachment/context chip.
- Tool/action proposal card.
- Permission decision panel.
- Execution status and result summary.

## Component specification

Each component should state:
- Purpose and when to use it.
- Anatomy and content slots.
- Variants and properties.
- Interaction states.
- Keyboard and focus behaviour.
- Light/dark theme behaviour.
- Responsive constraints.
- Do-not-use guidance where a pattern is easy to misuse.

## Quality rules

- Components use semantic design tokens.
- Keep labels and icons consistent.
- Do not encode meaning only through colour.
- Icon-only controls require an accessible name and a tooltip plan.
- Disabled controls should remain legible.
- Destructive actions require clear distinction and appropriate confirmation.
- Prefer composition and variants over duplicating near-identical components.
