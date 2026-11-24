# Design documentation

This directory defines the ATLAS user experience and visual interface. During the planning period, the Figma design file is the canonical visual workspace; these Markdown documents explain its structure, decisions and implementation intent.

## Design workspace

Create one Figma design file named **ATLAS — Core UI/UX Design**. Keep the file organised by pages rather than creating a separate file for every screen.

Suggested page order:

1. `00 — Cover & Changelog`
2. `01 — Foundations`
3. `02 — Components`
4. `03 — App Shell`
5. `04 — Dashboard`
6. `05 — Projects`
7. `06 — AI Workspace`
8. `07 — Tools & Integrations`
9. `08 — Settings & Onboarding`
10. `09 — Prototype Flows`
11. `10 — Pro Exploration`
12. `11 — Archive`

Keep Pro exploration visually and structurally separate from Core designs. Do not let Pro concepts silently expand the Core milestone.

## Documents

- [Figma workflow](FIGMA_WORKFLOW.md) — how to organise, design, prototype and review the file.
- [Design system](DESIGN_SYSTEM.md) — tokens, typography, layout, colour and theming rules.
- [Prototype specification](PROTOTYPE_SPEC.md) — interaction, animation and state requirements.
- [Screen specifications](SCREENS/README.md) — screen inventory and required states.
- [Component library](COMPONENTS/README.md) — reusable component inventory and behaviour.
- [Handoff checklist](HANDOFF.md) — what must be ready before implementation.

## Design status

Every screen should carry a visible status in its Figma section or cover note: Draft, In review, Approved for build, or Superseded. Approval means the layout and intended behaviour are sufficiently specified; it does not mean the application is implemented.

## Design principles

- Desktop-first, keyboard-friendly and efficient for repeated daily use.
- Clear hierarchy without turning every screen into a dense dashboard.
- Consistent spacing, typography, icons, states and navigation.
- Dark-first visual direction, while designing a complete light theme too.
- Accessible contrast, readable text and non-colour-only status communication.
- Motion should explain state changes, not decorate every interaction.
- Avoid copying reference-app layouts; record the problem a pattern solves and design an ATLAS solution.
