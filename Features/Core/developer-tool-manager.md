# Developer Tool Manager

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Developer environment setup

## 1. Purpose

Developer Tool Manager detects developer tools and their installed versions, explains project requirements and helps users install missing tools through explicit, reviewable workflows. It should reduce setup friction without taking control away from the user.

## 2. Tool inventory

Potential tools include Git, Python, Node.js, package managers, Docker, language runtimes, compilers, IDEs and platform-specific development utilities. The actual supported list must be defined incrementally. For each detected tool, show:

- Display name and tool category.
- Detected version and executable location, where available.
- Detection source and confidence.
- Whether it is available in the current shell/environment.
- Whether a project appears to require it.
- Any compatibility warning or known limitation.

Do not claim a tool is absent just because one discovery method cannot find it. Distinguish not detected, not installed, unsupported and detection failed.

## 3. Project requirement checks

When a project is selected, compare its declared or detected requirements with the available environment. Use project files and explicit configuration as evidence; label inferred requirements. Explain version mismatches and show the relevant file or setting when possible.

## 4. Installation workflow

An installation proposal must show the tool, version, source, package manager or installer, destination/environment, approximate download size when known, required privileges and any material changes. The user must explicitly approve installation before it begins.

- Never install tools automatically just because a project is opened.
- Never silently upgrade, downgrade or replace an existing version.
- Let the user decline an individual tool while continuing other setup steps.
- Do not bypass OS security prompts or privilege controls.
- If a setup script will run, disclose its purpose and source before execution.
- Support cancellation where the underlying installer permits it.
- Report partial success and failure accurately.

The system must allow a user to deny a suggested version or installation. A denied installation must remain denied unless the user later chooses it.

## 5. Version and environment handling

Where multiple versions are installed, show which one is selected by the current environment and avoid changing global PATH or system defaults without explicit consent. Prefer project-scoped or user-scoped configuration when supported, and explain trade-offs. WSL, containers and remote environments must not be conflated with the host environment.

## 6. Updates and removal

Core may identify outdated tools and show available update information. Updating or uninstalling must be a separate user-initiated action with a clear impact summary. Do not remove dependencies merely because they are not currently used by a registered project.

## 7. Reliability and security

Use trusted official sources or established package managers where possible. Verify downloaded artifacts using available signatures or checksums when supported. Do not invent verification if the source does not provide it. Keep installer output available for troubleshooting, redact credentials and avoid running installers with unnecessary privileges.

## 8. Acceptance criteria

- Inventory results show version and detection confidence.
- A project requirement can be compared with detected tools.
- Every installation displays a review screen and requires consent.
- Users can decline individual tools and versions.
- No global environment changes occur without explicit approval.
- Failures and partial installations are visible and recoverable.
- Host, WSL, container and remote tool inventories are kept distinct.

## 9. Dependencies and open decisions

Integrates with Hardware Profiler, Project Hub, AI Model Manager, Universal App Launcher and AAP. Define an initial small supported-tool catalogue and platform adapters before attempting broad package-manager support.

## 10. Related documentation

- [Hardware Profiler](hardware-profiler.md)
- [Project Hub](project-hub.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
