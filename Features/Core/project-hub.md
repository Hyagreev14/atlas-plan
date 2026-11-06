# Project Hub

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Project organisation

## 1. Purpose

Project Hub is the central catalogue for development projects the user chooses to manage in ATLAS. It should make projects easy to register, find, open and inspect without moving, copying or taking ownership of their files.

## 2. Project registration

Users can add a project by selecting an existing directory or choosing a supported repository location. ATLAS should record a stable project reference and basic metadata such as display name, root path, date added and last opened. The user can edit the display name, description, tags and optional project icon.

Project discovery must be opt-in and scoped. ATLAS must not crawl the entire drive or index unrelated personal folders without clear user action. A discovered project is only a suggestion until the user adds it.

## 3. Project overview

A project page may show:

- Project name, root path and user description.
- Detected languages, frameworks and project markers, labelled as detected rather than guaranteed.
- Common entry points and configuration-file names.
- Git repository status when a repository is detected.
- Available launch actions and configured development commands.
- Known running tasks associated with the project.
- Project Doctor findings and recent ATLAS activity.
- User-defined tags, notes and favourite status.

Do not expose secret values from configuration files. Detection should report that a secret-like variable exists only when necessary, never its value.

## 4. Project actions

Users should be able to open the root directory, open a selected IDE, open a terminal at the project root, inspect Git status, run a configured action or remove the project registration. The user chooses preferred IDE and terminal defaults. ATLAS must not assume every project uses the same editor, shell or start command.

## 5. Project lifecycle and filesystem boundaries

Removing a project from Project Hub removes its ATLAS registration only. It must never delete, move or modify the project directory. Any future delete-files action must be a separate, clearly labelled operation with a path preview and independent approval.

If a registered path is moved, renamed, disconnected or unavailable, show the project as unavailable and let the user locate it again. Do not silently substitute a similarly named directory.

## 6. Search and organisation

Support search by project name and path, plus user-defined tags and filters such as favourite, recent or unavailable. Sorting should be predictable and user-selectable. Avoid requiring a cloud account or remote service for basic organisation.

## 7. Persistence and privacy

Store only the metadata required for the Hub. Project file contents remain in their original locations. Provide controls to clear recent-project history and remove registrations. Protect local project paths as personal information and do not upload them to an AI provider unless the user has chosen to share relevant context.

## 8. Acceptance criteria

- Users can add, rename, tag, search, open and unregister projects.
- Unregistering never deletes project files.
- Missing paths are clearly identified and can be relinked.
- Project detection is transparent and does not run unbounded background scans.
- Project information can be used by other ATLAS features through a shared project identity.
- The Hub remains functional when Git or AI integrations are unavailable.

## 9. Dependencies and open decisions

Provides project identity to Developer Home, AI Workspace, Git Centre, Project Doctor and Quick Actions. Define the supported project metadata schema before implementation. Decide whether project discovery is manual-only for Core or includes a user-selected folder scan.

## 10. Related documentation

- [Developer Home](developer-home.md)
- [Project Doctor](project-doctor.md)
- [Project Quick Actions](project-quick-actions.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
