# Interactive prototype specification

## Purpose and limitation

Figma prototypes are used to validate user journeys and interaction intent. They do not execute real filesystem operations, launch applications, run terminal commands, connect AI providers or enforce permissions. Those behaviours must be specified separately and tested in the application.

## Interaction catalogue

For each interactive element, document:
- Trigger: click, keyboard, hover or focus.
- Initial state.
- Resulting state or destination.
- Dismissal/cancellation behaviour.
- Keyboard behaviour.
- Loading, error and disabled behaviour where relevant.
- Whether confirmation is required in the real product.

## Required prototype flows

### 1. First launch
Welcome → explain local-first approach → choose basic preferences → finish → dashboard. Include skip and revisit tutorial paths. Do not imply that setup silently installs software or uploads data.

### 2. Daily start
Dashboard → open recent project → project overview → choose an installed tool → show the intended launch confirmation/transition. The prototype can simulate the result but must not imply that a real process was launched.

### 3. Project registration
Projects → add project → select/browse representation → review detected information → confirm registration → project appears in list. Include invalid path and cancellation states conceptually.

### 4. AI request and permission
AI Workspace → enter a request → show a proposed action summary → show ATLAS permission decision/confirmation → approved or denied outcome → activity record. The prototype must make clear that ATLAS, not the AI model, decides authorisation.

### 5. Tool detection
Tool Manager → detection result → tool details → user chooses whether to install or configure → progress and completion/error states. Do not represent automatic installation as the default.

### 6. Settings and theme
Settings → change theme or preference → preview change → save/reset path. Include a light/dark theme transition if practical.

## Component states to prototype

- Default, hover, pressed, keyboard focus, disabled.
- Selected and unselected navigation.
- Open and closed menus/overlays.
- Empty, populated and filtered lists.
- Loading, success, warning and error feedback.
- Permission requested, approved, denied and cancelled.
- Destructive confirmation and safe cancellation.

## Animation rules

Use Smart Animate for small, meaningful continuity transitions such as sidebar expansion, panel reveal or selection changes. Use overlays for menus and dialogs. Prefer simple transitions with consistent duration/easing. Avoid long decorative sequences, excessive parallax, motion that delays task completion or animation that obscures state.

Reduced-motion behaviour must be documented for implementation even if the Figma prototype cannot fully reproduce the OS preference.

## Prototype review checklist

- Can a reviewer complete each primary journey without verbal explanation?
- Are clickable elements visually identifiable?
- Does every overlay have a clear dismissal route?
- Is the back/navigation path predictable?
- Are errors and denied permissions understandable?
- Are keyboard and focus expectations documented?
- Does the prototype avoid claiming backend behaviour that is not implemented?
