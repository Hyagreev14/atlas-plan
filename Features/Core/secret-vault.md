# Secret Vault

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Credential protection

## 1. Purpose

Secret Vault protects API keys, tokens and other credentials used by ATLAS integrations. It should make credentials available to trusted provider or execution adapters when needed without exposing raw values to AI models, ordinary UI surfaces or logs.

## 2. Secret types and metadata

A secret record may include a user-defined name, provider/service association, creation/update time and optional expiry reminder. The secret value itself must be protected. Do not store credentials in project files, chat history, workflow definitions or plain-text settings.

## 3. Storage architecture

Prefer platform credential storage where it is suitable. If application-managed encrypted storage is required, use a vetted authenticated-encryption design and a key protected by OS-backed facilities. The exact cryptographic implementation must be selected and reviewed during engineering; do not invent a custom cipher or claim a fixed security guarantee without validation.

A user authentication or unlock step may be required before sensitive vault operations. Support secure locking on application exit or inactivity according to user settings and platform capabilities.

## 4. Secret use

Provider adapters and approved execution services may request access to a secret through a narrow interface. The raw value should be passed only to the component that requires it, never inserted into model prompts or returned in action results. Prefer environment or credential channels that avoid command-line exposure.

## 5. User experience

Users should be able to add, rename, replace, test where safe, rotate and delete secrets. After saving, show a masked identifier rather than the full value. Pasting or revealing a secret should require a deliberate action and be clearly indicated. Never reveal a secret automatically in response to an AI request.

## 6. Backup and migration

If backup/export is supported, make it an explicit protected operation with clear warnings. Never create an unencrypted export by default. Explain what happens when moving to another device or reinstalling the OS. Provide safe migration guidance without uploading vault contents to ATLAS servers.

## 7. Logging and redaction

Redact secrets from application logs, terminal output, error messages and activity history. Avoid leaking credentials through process arguments, crash reports or debugging tools. If a secret is accidentally exposed in a result, treat it as a security incident and guide the user to rotate it.

## 8. Threat model and limitations

Protect against casual local disclosure, accidental logging and model-context leakage. The Vault cannot guarantee protection against malware, a compromised operating system, a user-level attacker with full access or memory inspection. State these limitations honestly.

## 9. Acceptance criteria

- Secrets are not stored in plain-text settings or project files.
- AI models cannot read raw Vault values.
- Only authorised adapters can request secret use.
- Logs and activity records redact credential values.
- Users can rotate and delete secrets.
- Backup/export is protected and opt-in.
- Security claims match the actual reviewed implementation.

## 10. Dependencies and open decisions

Depends on OS credential facilities, provider adapters, AAP and Privacy settings. Choose the storage/key-management design only after platform-specific security review.

## 11. Related documentation

- [AI Model Manager](ai-model-manager.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Privacy and Offline Operation](privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
