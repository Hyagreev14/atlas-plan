# Remote Development Manager

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Remote and virtualised development

## 1. Purpose

Remote Development Manager provides a unified interface for connecting to and working with supported development environments outside the local host context. Targets may include SSH hosts, WSL distributions, remote Linux machines, development VPS instances and supported containers.

## 2. Target inventory

Each target should have a user-defined name, connection type, address or local identifier, username/identity reference, platform details when known and last connection state. Do not store private keys or passwords in plain-text configuration. Use OS credential facilities or Secret Vault references.

## 3. Connection workflow

Users should be able to add, edit, test, connect, disconnect and remove targets. Before connecting, show the destination and authentication method. For SSH, validate host identity using known-host mechanisms and clearly report host-key changes. Do not silently accept a changed host key.

## 4. Remote workspace

Where supported, allow users to browse selected remote directories, open a remote project, inspect tools and execute supported tasks. Keep remote paths and local paths distinct. The UI must clearly show which machine receives a command or file operation.

## 5. Command and file execution

Remote file operations and terminal commands use AAP and the same Permission Manager policy as local operations. Scope actions to the selected remote workspace. Do not assume that local path validation is sufficient for remote paths. Remote scripts and repository content are untrusted.

## 6. Environment and tool detection

Detect remote OS, architecture and developer tools where permitted. Report detection source and timestamp. Avoid installing remote tools automatically. Any installation or system-level change requires a preview and explicit consent on the target machine.

## 7. Connection reliability

Handle offline hosts, DNS failures, authentication failures, timeouts, host-key mismatches and interrupted connections. A dropped connection must not be reported as a completed remote action. For long-running tasks, show whether the remote process may continue after the client disconnects.

## 8. Security

- Use secure transport and host identity verification.
- Protect private keys and tokens.
- Do not expose credentials to AI.
- Confirm the target host and working directory for sensitive commands.
- Avoid forwarding agents or ports without explicit user configuration.
- Apply Git push and other permission policies to remote operations.
- Record remote target identity in Activity Timeline.

## 9. Acceptance criteria

- Users can register and connect to supported remote targets.
- The active target is always visible.
- Host identity and authentication errors are handled safely.
- Remote commands/files pass through AAP and Permission Manager.
- Local and remote paths/processes are not conflated.
- Disconnects and partial operations are reported accurately.

## 10. Dependencies and open decisions

Depends on Project Hub, Developer Tool Manager, Environment Profiles, Secret Vault, AAP and platform SSH/WSL/container APIs. Define the first supported connection types and whether file browsing or remote terminal is the first milestone.

## 11. Related documentation

- [Environment Profiles](environment-profiles.md)
- [Developer Tool Manager](../Core/developer-tool-manager.md)
- [Secret Vault](../Core/secret-vault.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
