# Electron security requirements

These are mandatory design constraints for the Electron implementation.

## Renderer isolation

- Enable `contextIsolation`.
- Keep `nodeIntegration` disabled in renderer processes.
- Enable sandboxing where compatible with the selected architecture.
- Apply a restrictive Content Security Policy.
- Do not load arbitrary remote content with privileged application access.
- Validate navigation, new-window requests and external URL handling.
- Keep dependencies current and review Electron security advisories.

## Preload and IPC

- Expose a small, purpose-specific API through `contextBridge`.
- Never expose raw Electron or Node objects.
- Validate every IPC payload at the receiving boundary.
- Check the sender/frame and expected origin for privileged requests.
- Avoid generic methods such as unrestricted `runCommand(command)` or `readFile(path)`.
- Return structured results and errors; do not leak stack traces or secrets.

## Filesystem and process operations

- Restrict file operations to user-selected or explicitly authorised paths.
- Defend against traversal, symlink and time-of-check/time-of-use issues.
- Validate executable identity and arguments.
- Avoid shell string concatenation; prefer safe argument arrays and explicit executable paths.
- Display the action and target to the user before sensitive operations.
- Do not run with administrator/root privileges by default.

## Secrets and privacy

- Use OS-protected credential storage where available, with a documented fallback.
- Never hard-code secrets or commit them to the repository.
- Redact secrets from logs, crash reports and AI context.
- Explain what information is sent to an external AI provider.
- Keep offline/local workflows usable where the feature permits.

## AI and permissions

- AI output is untrusted input.
- The model cannot choose its own approval requirement or approve an action.
- Permission decisions are enforced by trusted ATLAS code.
- Voice and screenshot context do not bypass normal permissions.
- Log action outcomes without logging secret values.

## Verification

Create threat models and tests for renderer compromise, malformed IPC, path traversal, unsafe URLs, command injection, secret leakage, malicious project content and permission bypass. Security claims require tests and evidence, not only configuration intent.
