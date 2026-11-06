# Developer Productivity Tools

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Daily developer utilities

## 1. Purpose

Provide a focused collection of small utilities that reduce everyday development friction. These tools should be quick to access, predictable and useful alongside existing IDEs and terminals. ATLAS should not attempt to become a full office suite or duplicate every feature of specialist applications.

## 2. Initial utility set

The exact Core set should be prioritised after testing, but candidates include:

- **Quick notes:** lightweight notes associated with a project or kept globally.
- **Snippet library:** save and search reusable text or code snippets, with optional language/category labels.
- **Command palette:** search ATLAS pages, projects, applications and available actions from one keyboard-accessible interface.
- **Text search helpers:** search selected text or user-selected files using supported local tools.
- **Port helper:** inspect listening ports and identify owning processes when the platform exposes reliable information.
- **Clipboard helpers:** access explicitly copied recent items or pin selected snippets, subject to OS clipboard permissions.
- **Session helpers:** save a named collection of project, terminal and application references for a work session.
- **Encoding/format helpers:** small transformations such as JSON formatting or URL encoding, where they can be implemented safely and locally.

## 3. Notes

Notes should support create, edit, rename, search and delete. A note may be global or associated with a registered project. Autosave behaviour must be visible and robust. Deleting a note should be recoverable where feasible and require confirmation if it contains substantial unsaved changes.

## 4. Snippets

Snippets should store user-authored content with a title, description, tags and optional language. Users should be able to copy a snippet or insert it into an explicitly selected destination. Insertion into project files is a modifying action and must use AAP and normal approval rules. Never execute a snippet simply because it is selected.

## 5. Command palette

The palette should support keyboard navigation, clear action labels and a way to understand what a command will do. Destructive or external actions must not execute merely because a fuzzy-search result was highlighted. The user must intentionally invoke the action and pass its normal permission checks.

## 6. Port and process helpers

Show port number, protocol and owning process only when the platform provides reliable evidence. A port conflict diagnosis is not proof that a particular application is safe to terminate. Any stop action must identify the exact process and require appropriate approval.

## 7. Data, import and export

Keep utility data local by default. If import/export is supported, use documented formats and warn before overwriting existing records. Snippets and notes may contain sensitive text, so do not automatically attach them to AI context.

## 8. Accessibility and usability

Support keyboard-first operation, readable labels, sensible focus order and clear empty states. Utilities should open quickly and not require a multi-step setup for basic use.

## 9. Acceptance criteria

- Users can create, search, edit and delete notes.
- Snippets can be copied without executing them.
- Command palette results clearly identify action type.
- Port information includes evidence and limitations.
- Utility content is not automatically uploaded to AI providers.
- Optional utilities can be disabled without breaking the rest of ATLAS.

## 10. Dependencies and open decisions

Integrates with Project Hub, AAP, Secret Vault and Activity Timeline. Choose a small set of utilities for Core rather than shipping every candidate at once.

## 11. Related documentation

- [Project Hub](project-hub.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Activity Timeline](activity-timeline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
