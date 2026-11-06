# Extension Ecosystem

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Extensibility and integrations

## 1. Purpose

Extension Ecosystem allows third parties and advanced users to extend ATLAS with integrations, panels, tools and workflow actions. It should provide a controlled capability model rather than granting extensions unrestricted access to the user's computer.

## 2. Extension manifest

An extension should declare:
- Unique identifier, name, version and publisher.
- Description and supported ATLAS API/protocol versions.
- Requested capabilities and why they are needed.
- Entry points and UI contributions.
- Commands/actions it exposes.
- Network endpoints or external services it contacts, where applicable.
- Data categories it reads or writes.
- Update and compatibility metadata.

Undeclared capabilities must not be granted implicitly.

## 3. Permission model

Use least privilege. Extensions should receive only the capabilities the user explicitly grants. Sensitive capabilities—filesystem access, command execution, project modification, network access, Vault integration, microphone/screen capture and Git operations—must be separately declared and controlled.

An extension cannot grant itself permissions, change global ATLAS security settings or bypass AAP. Any extension action that affects user data must be validated and authorised by trusted ATLAS services.

## 4. Installation and updates

Show publisher, source, version, requested permissions and compatibility before installation. Do not silently install extensions from an AI suggestion. Updates must show meaningful permission changes; a new permission request requires renewed user consent.

Provide disable, uninstall and permission-revoke controls. Uninstalling an extension should not delete user project data or unrelated settings.

## 5. Runtime isolation

Choose a sandbox or process-isolation model appropriate to the extension type. Do not claim complete isolation unless the architecture enforces it. Extensions should not access internal databases, raw secrets or arbitrary host APIs by default.

## 6. Review and trust

Distinguish verified publisher identity, signed packages, source availability and community ratings; none alone guarantees safety. If an extension is unsigned or from an unknown source, show that fact clearly. Avoid presenting a curated catalogue as a security guarantee.

## 7. Compatibility and failure

Check API version and platform compatibility before enabling an extension. If it crashes or misbehaves, allow it to be disabled without making ATLAS unusable. Record extension errors without logging secrets.

## 8. Acceptance criteria

- Extensions declare capabilities before installation.
- User consent is required for sensitive permissions.
- Runtime access is limited to granted capabilities.
- Permission changes during updates trigger renewed consent.
- Extensions cannot bypass AAP or alter security settings.
- Users can disable, uninstall and revoke access.
- Extension failure does not crash the entire application.

## 9. Dependencies and open decisions

Depends on AAP, Permission Manager, local package/update architecture and UI extension points. Define a stable extension API and threat model before publishing an ecosystem or marketplace.

## 10. Related documentation

- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Secret Vault](../Core/secret-vault.md)
- [Privacy and Offline Operation](../Core/privacy-and-offline.md)
- [Workflow Automation](../Core/workflow-automation.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
