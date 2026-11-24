# February 2027 design-to-development handoff

## Handoff objective

Give the implementation work a coherent, reviewed interface specification so React + TypeScript development can begin without guessing basic layout, component behaviour or navigation.

## Required deliverables

- [ ] Canonical Figma file with cover, changelog and page structure.
- [ ] Approved app shell and navigation.
- [ ] Approved Core screen frames linked to feature specifications.
- [ ] Reusable component library with variants and states.
- [ ] Light and dark semantic variables.
- [ ] Typography, spacing, radii, border and motion token references.
- [ ] Clickable prototype for primary user journeys.
- [ ] Empty, loading, error, disabled and permission states where relevant.
- [ ] Keyboard, focus, scaling and accessibility notes.
- [ ] Compact, standard and wide window layout guidance.
- [ ] Known design questions and deliberate deferrals.
- [ ] Clear separation between Core-approved and Pro-exploration frames.

## Per-screen handoff packet

For each screen provide the Figma frame link/name, purpose, entry/exit paths, dimensions, component list, token usage, interaction behaviour, states, keyboard notes and linked feature requirement.

## Developer review

The developer should review the handoff before implementing a screen and raise ambiguities early. If implementation constraints require a design change, record the reason and update Figma. Do not silently diverge from the approved design.

## Source of truth

Figma is the visual/interaction specification during planning. The application code and tested runtime behaviour become authoritative for what is actually implemented. Keep both aligned through documented design changes.
