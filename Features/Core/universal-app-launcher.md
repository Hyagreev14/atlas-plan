# Universal App Launcher

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Application access

## 1. Purpose

Universal App Launcher provides one searchable place to find and open installed applications, development tools, IDEs, terminals and user-defined launch targets. It should reduce the friction of switching between the applications developers use every day.

## 2. Discovery

Use platform-appropriate application discovery mechanisms rather than assuming one operating system's installation layout. Discovery may include registered desktop applications, Start Menu entries, known executable registrations and user-added paths, depending on platform support.

Each result should identify its source and distinguish a detected application from a manually added shortcut. Discovery must not execute an application to test it. Do not scan unrelated folders recursively by default.

## 3. Search and organisation

- Search by display name and, where useful, executable or command name.
- Support favourites, recent launches and user-defined groups.
- Allow custom entries for portable applications, scripts and development commands.
- Let users edit labels and icons without changing the underlying executable.
- Provide filters such as all, favourites, recent and custom entries.
- Support keyboard navigation and a command-palette-style quick launch.

## 4. Launch behaviour

Launching an item should use the platform's supported process/application mechanism. Where appropriate, allow launch arguments, working directory and environment profile to be configured by the user. A project-specific launch target should be able to use the project's registered root directory.

ATLAS should report launch failures with a useful explanation when available: missing executable, invalid path, permission issue or process start failure. It must not claim an application opened merely because a launch request was sent.

## 5. Custom launch entries

A custom entry may refer to an application executable, a registered application, a directory, a document or a supported development command. The UI should explain the type of target and show the path or command before saving. Shell scripts and commands must use the execution and permission architecture; they are not ordinary trusted app shortcuts.

## 6. Installation boundary

The Launcher opens applications that are already installed or explicitly configured. Finding an unavailable application may offer a handoff to Developer Tool Manager, but the Launcher itself must not silently download or install software.

## 7. Settings and user control

Allow users to choose preferred launch behaviour, manage favourites, edit custom entries, clear recent history and disable automatic discovery sources where practical. A failed or removed application should be marked unavailable and remain editable or removable.

## 8. Security and privacy

- Validate executable and target paths.
- Do not interpret arbitrary search text as a command.
- Do not elevate privileges automatically.
- Do not expose secret command-line arguments in logs or recent history.
- Treat custom scripts as executable actions and apply AAP/Permission Manager rules.
- Do not upload the installed-application inventory to cloud AI without disclosure and user consent.

## 9. Acceptance criteria

- Users can search and launch supported installed applications.
- Users can add, edit, favourite and remove custom entries.
- Missing targets are reported accurately.
- Launch groups open only the items the user selected.
- No software is installed as a side effect of searching or launching.
- The feature degrades gracefully when platform discovery is incomplete.

## 10. Dependencies and open decisions

Integrates with Developer Home, Project Hub, Developer Tool Manager and AAP. Platform-specific discovery adapters and the supported custom-entry types must be defined before implementation.

## 11. Related documentation

- [Developer Tool Manager](developer-tool-manager.md)
- [Project Hub](project-hub.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
