# Primary user journeys

These journeys guide Figma prototypes and later acceptance testing.

## Journey 1 — Start a development session

1. User launches ATLAS.
2. Dashboard shows useful local context and recent projects.
3. User opens a project.
4. ATLAS displays project information and available quick actions.
5. User launches an installed IDE or terminal.

**Success:** user can orient themselves and reach the intended project/tool without hunting through multiple unrelated screens.

## Journey 2 — Register a project

1. User opens Projects and chooses Add Project.
2. User selects a local project location.
3. ATLAS previews detected project details.
4. User confirms registration.
5. Project appears in the project hub.

**Success:** no project is silently moved, modified or uploaded during registration.

## Journey 3 — Ask AI for help

1. User opens AI Workspace.
2. User chooses or reviews the current mode/provider.
3. User asks a question.
4. AI responds or proposes a structured action.
5. If an action is requested, ATLAS independently validates and applies permission policy.
6. User sees the result or a clear denial/cancellation.

**Success:** AI assistance is useful without bypassing user control.

## Journey 4 — Manage a developer tool

1. User opens Tool Manager.
2. ATLAS displays detected status and source of information.
3. If a tool is missing, ATLAS explains the proposed installation.
4. User chooses whether to proceed.
5. ATLAS shows progress and outcome.

**Success:** no silent install; user can decline.

## Journey 5 — Change a preference

1. User opens Settings.
2. User changes a preference such as theme.
3. The interface previews/applies the change.
4. User can restore defaults where appropriate.

**Success:** settings are discoverable, consistent and reversible where possible.
