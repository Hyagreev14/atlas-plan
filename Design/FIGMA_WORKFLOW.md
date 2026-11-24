# Figma-first workflow

**Planning window:** 24 November 2026 through January 2027  
**Implementation handoff:** February 2027  
**Target:** a coherent, buildable ATLAS Core interface, not a collection of disconnected mockups.

## 1. Purpose

Use Figma to explore information architecture, establish a reusable visual language, design Core screens, prototype realistic journeys and resolve major UX questions before application implementation. Figma prototypes demonstrate intended interaction; they are not the running Electron application and do not prove backend behaviour.

## 2. File setup

Create a Figma file named **ATLAS — Core UI/UX Design**. Use the page structure listed in [Design README](README.md). Keep one canonical file where practical so components and variables stay consistent.

On the cover page include:
- Product name and one-sentence purpose.
- Current design version/date.
- Core or Pro designation.
- Status legend: Draft / In review / Approved for build / Superseded.
- Links to this planning repository and relevant specifications.
- A short changelog with date, author and summary.

Use clear frame names such as `Core / Dashboard / Default / 1440x900`. Name components by role, not by visual appearance alone.

## 3. Design sequence

### Phase A — Information architecture
1. Review the product principles and Core scope.
2. Identify the main navigation areas and their relationships.
3. Define the primary user journeys before polishing visuals.
4. Decide what belongs in global navigation, contextual navigation and page content.
5. Record unresolved questions instead of hiding them in mockups.

### Phase B — Foundations
1. Define typography, spacing, colour, radii, borders, elevation and icon rules.
2. Create semantic colour variables rather than scattering raw hex values.
3. Define light and dark themes.
4. Create responsive desktop layout rules for compact, standard and wide windows.
5. Check contrast and text sizing before building dozens of screens.

### Phase C — Components
Build reusable components with variants and states: buttons, fields, navigation items, tabs, cards, menus, dialogs, toasts, badges, empty states, tables, command/search surfaces and panels. Include keyboard focus, disabled, loading, error and destructive states where relevant.

### Phase D — Screens
Design the Core screen inventory in [SCREENS](SCREENS/README.md). Start with the app shell and dashboard, then projects and the most important daily workflows. Avoid polishing secondary screens before the primary navigation works.

### Phase E — Interactive prototypes
Create clickable prototypes for the flows in [Prototype specification](PROTOTYPE_SPEC.md). Use overlays for dialogs and menus, component variants for button states, and Smart Animate only where it improves comprehension. Prototype both successful and unsuccessful paths.

### Phase F — Review and handoff
Run a usability walkthrough, check keyboard paths and accessibility, verify component consistency, then complete [Handoff checklist](HANDOFF.md). Mark approved frames and link them to their relevant feature specifications.

## 4. Prototype fidelity

Use three deliberate fidelity levels:
- **Low fidelity:** layout, navigation and hierarchy; minimal styling.
- **Mid fidelity:** real typography, spacing, components and representative content.
- **High fidelity:** approved Core screens, variants, key transitions and realistic sample data.

Do not spend time animating an interaction whose basic information architecture is still unsettled.

## 5. Review routine

For each review:
- State the question the design is trying to answer.
- Test the flow at a realistic desktop window size.
- Check the default state and at least one empty, loading, error or permission state as appropriate.
- Review keyboard navigation and visible focus.
- Record feedback and decisions in the design changelog or [Research log](../Research/RESEARCH_LOG.md).
- Update the screen status.

## 6. Figma-to-code handoff

For every approved screen, provide:
- Frame link/name and target dimensions.
- Component names and variants used.
- Semantic colour and spacing tokens.
- Interaction description and navigation destination.
- Loading, empty, error, disabled and confirmation states where applicable.
- Keyboard and accessibility notes.
- Any behaviour that requires a real service and cannot be represented in Figma.

The February handoff should include the app shell, Core screen set, component library, token definitions, primary prototypes and a list of known unresolved design questions.

## 7. Scope guardrails

- Core is the design priority until its mid-March 2027 target.
- Pro concepts stay on the Pro page and are labelled exploratory.
- Figma does not determine security policy; security rules come from the architecture and permission specifications.
- A clickable prototype must never be described as a functional implementation.
- Do not invent platform behaviour based only on a visual mockup.
