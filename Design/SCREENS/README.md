# Core screen inventory

This is the initial screen inventory for Figma. It is a planning list, not proof that all screens are approved or committed to the release. Link each screen to the corresponding feature specification as the design matures.

| Area | Screen / frame set | Key states |
|---|---|---|
| App shell | Main window, sidebar, title bar, global search | Expanded/collapsed navigation, compact window |
| Onboarding | Welcome, preferences, completion | First run, skip, revisit |
| Dashboard | Developer Home | First run, populated, no recent projects, loading |
| Projects | Project list and project detail | Empty, populated, filtered, unavailable path |
| Project actions | Register/import, quick actions | Validation, confirmation, cancellation |
| AI Workspace | Conversation and context panel | Empty, active, waiting, error, offline |
| AI actions | Proposed action and permission review | Pending, approved, denied, cancelled |
| Tools | App launcher and tool manager | Detected, missing, install consent, failure |
| Git | Repository overview and changes | Clean, modified, unavailable remote |
| System | System monitor and hardware profile | Normal, warning, unavailable metrics |
| Settings | General, appearance, providers, privacy | Saved, unsaved, validation error |
| Activity | Activity timeline | Empty, populated, filtered |

## Design order

1. App shell and navigation.
2. Developer Home dashboard.
3. Project list, project detail and registration.
4. AI Workspace and permission review.
5. Tools and launcher.
6. Settings and onboarding.
7. Remaining Core screens based on validated priorities.

## Per-screen specification template

For each screen, document:
- User goal and entry points.
- Primary action and secondary actions.
- Content hierarchy and key information.
- Components used.
- Default, empty, loading, error and permission states.
- Keyboard navigation and focus order.
- Responsive behaviour at compact, standard and wide sizes.
- Links to feature requirements and prototype flows.
- Design status and review notes.

## Scope note

A screen should not be added solely because it looks impressive. It must support a Core user need, have a clear owner in the feature specifications and be feasible to implement and test.
