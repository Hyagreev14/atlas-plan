# Environment Profiles

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Project environment management

## 1. Purpose

Environment Profiles lets users define named development environments for a project or workspace, such as Development, Testing and Production-like. It should make environment selection repeatable while avoiding accidental changes to global system configuration or exposure of secret values.

## 2. Profile contents

A profile may reference:
- Project-specific runtime and tool versions.
- Working directory and launch configuration.
- Environment-variable names and references to Vault secrets.
- Container, WSL or remote environment identifiers where supported.
- Build/test task selections.
- Application and terminal preferences.
- Non-secret configuration values.

Secret values must remain in Secret Vault or an appropriate OS credential facility. Profiles should store references, not raw credentials.

## 3. Profile lifecycle

Users can create, clone, rename, edit, activate and delete profiles. A profile may be project-specific or workspace-wide. Show which profile is active and which settings it controls. Deleting a profile must not uninstall tools, delete environments or remove secrets unless the user separately chooses those actions.

## 4. Switching profiles

Before activation, show the changes that will take effect, including tool selection, environment references and launch behaviour. If a change requires restarting a terminal or application, explain it. Do not silently rewrite global PATH, system variables or OS configuration.

If a referenced runtime or environment is missing, report the profile as partially available and offer a user-approved resolution path.

## 5. Environment isolation

Where supported, integrate with project-local virtual environments, containers or WSL distributions. Clearly distinguish host, WSL, container and remote environments. Do not imply isolation if a profile merely changes environment variables or command paths.

## 6. AI and workflow integration

AI may inspect the active profile metadata and request profile-related actions through AAP. It cannot read secret values or change profile permissions. Workflow and Build & Test Centre tasks should record which profile they use so results are understandable.

## 7. Security and privacy

- Keep secret values in Vault.
- Avoid logging environment-variable values.
- Show which environment receives a command.
- Require approval for profile changes with material system effects.
- Treat project configuration as untrusted.
- Do not send profile contents to cloud AI without disclosure.

## 8. Acceptance criteria

- Users can create and manage named profiles.
- Switching previews the relevant changes.
- Host, WSL, container and remote targets are distinguished.
- Missing dependencies are reported without silent installation.
- Secret values never appear in profile files or AI context.
- Profile deletion does not delete the underlying environment.

## 9. Dependencies and open decisions

Depends on Project Hub, Developer Tool Manager, Secret Vault, Build & Test Centre and Remote Development Manager. Decide which environment types and variables are supported in the first release.

## 10. Related documentation

- [Developer Tool Manager](../Core/developer-tool-manager.md)
- [Secret Vault](../Core/secret-vault.md)
- [Build & Test Centre](build-and-test-centre.md)
- [Remote Development Manager](remote-development-manager.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
