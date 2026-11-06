# Project Quick Actions

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Project workflow shortcuts

## 1. Purpose

Project Quick Actions provides a compact set of context-aware operations for the currently selected project. It reduces repetitive navigation while keeping actions explicit and understandable.

## 2. Action catalogue

Potential actions include:
- Open project root in the file manager.
- Open project in the preferred IDE.
- Open a terminal at the project root.
- Open the project in Git Centre.
- Inspect project health with Project Doctor.
- Copy the project path.
- Open known documentation or configuration files.
- Run a user-configured development command.
- Start a registered workflow.
- Open a project-specific notes or snippets view.

Only actions supported by the selected project and installed tools should appear as immediately available. Unsupported actions should be hidden or clearly marked unavailable with an explanation.

## 3. Context resolution

Actions must use the registered project root and user-selected application defaults. If the project path is missing or ambiguous, ask the user to locate it; never choose a similarly named folder automatically. If multiple IDEs or terminals are installed, use the configured preference or ask the user.

## 4. Custom actions

Allow users to define a label, action type, working directory and supported parameters. A custom command must be stored as structured executable and argument data where possible, not treated as trusted arbitrary text. Display the command and target before execution. User-defined actions remain subject to AAP, validation and Permission Manager policy.

## 5. AI integration

AI may suggest a quick action based on project context, but the user must invoke it and the action must pass normal checks. AI cannot add a custom action, change its permissions or execute it outside the shared action system without user authorisation.

## 6. Failure handling

Report missing applications, invalid paths, unavailable commands and execution errors. Preserve the user's project registration and configuration when an action fails. Do not claim that a server or tool started unless ATLAS can verify the relevant process state.

## 7. Acceptance criteria

- Users can access common project actions from the project view.
- Actions use the correct registered project root.
- Custom actions are editable and inspectable.
- Commands require appropriate validation and approval.
- Missing tools or paths produce clear errors.
- Quick Actions never bypass Git, file or terminal permissions.

## 8. Dependencies and open decisions

Depends on Project Hub, Universal App Launcher, Git Centre, Workflow Automation and AAP. Decide which actions are first-class Core defaults and which are user-configured.

## 9. Related documentation

- [Project Hub](project-hub.md)
- [Universal App Launcher](universal-app-launcher.md)
- [Workflow Automation](workflow-automation.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
