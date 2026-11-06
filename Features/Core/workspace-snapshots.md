# Workspace Snapshots

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Workspace continuity

## 1. Purpose

Workspace Snapshots save a restorable description of the user's ATLAS workspace at a point in time. They help users return to a familiar arrangement of projects, applications and workspace preferences without copying or backing up project source files.

## 2. Snapshot contents

A snapshot may contain:
- Selected or pinned project references.
- Open ATLAS sections and layout preferences.
- Favourite applications or launch groups.
- Selected workspace profile references when supported.
- User-selected session labels and notes.
- References to known terminal/task sessions, where safe and technically reliable.

Snapshots should store references and preferences, not project contents, credentials or raw environment-variable values.

## 3. Create and manage

Users can create a named snapshot manually, add a description, rename it, duplicate it or delete it. Automatic snapshot creation should not be enabled by default unless the user explicitly opts in. Show when a snapshot was created and which categories it contains.

## 4. Restore workflow

Before restoring, show a preview of what will change. Identify missing projects, unavailable applications and stale references. Let users choose whether to skip unavailable items or cancel. Restoring a snapshot must not silently close applications, terminate processes, overwrite files or alter system configuration.

If future functionality restores terminal sessions or running processes, it must be a separate explicit action with its own safety checks.

## 5. Data lifecycle

Snapshots should be local by default and easy to delete. Removing a snapshot must not remove the referenced project, application or user data. If a project path has moved, ask the user to relink it rather than choosing another location automatically.

## 6. Privacy and security

Do not store API keys, passwords, tokens, raw secrets, private file contents or unredacted command arguments. Treat project paths and application usage as personal information. If export/import is supported, explain the contents and protect the file appropriately.

## 7. Acceptance criteria

- Users can create, rename, duplicate, restore and delete snapshots.
- Restore preview identifies changes and unavailable references.
- Snapshot deletion never deletes referenced resources.
- Secrets and project file contents are excluded.
- Missing references are handled without guessing.
- Restoring does not terminate or modify external processes by default.

## 8. Dependencies and open decisions

Integrates with Developer Home, Project Hub, Universal App Launcher and Activity Timeline. Define the snapshot schema and decide whether layout restoration or project/application selection is the first useful Core milestone.

## 9. Related documentation

- [Developer Home](developer-home.md)
- [Project Hub](project-hub.md)
- [Universal App Launcher](universal-app-launcher.md)
- [Activity Timeline](activity-timeline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
