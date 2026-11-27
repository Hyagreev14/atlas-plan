# ATLAS identity, devices and synchronization model

**Status:** Proposed design requirements. The exact protocol, database schema and authentication technology are not yet selected.

This document defines the conceptual model needed for multiple users and multiple devices on one self-hosted ATLAS instance.

## Core entities

### Server instance

A single deployed ATLAS Server with its own URL, configuration, administrator policy, database and cryptographic configuration. Instance identity must be stable across ordinary restarts and documented backup/restore operations.

### User account

An identity scoped to one server instance. Each account has a stable internal identifier, authentication credentials or identity-provider linkage, profile/preferences and owned synchronized records.

A username or email address is a display/login attribute, not a safe database ownership key.

### Device

A registered client installation associated with one user account. Each device has:
- A server-issued device identifier.
- A user-visible device name and client type/version.
- Registration and last-seen metadata.
- A revocable authorization state.
- Its own session/credential material.

Device registration must be explicit. A copied configuration file must not silently clone an authorized device identity.

### Session

A time-bounded authenticated connection associated with a user and, where applicable, a device. Sessions can be expired or revoked independently. Signing out one device must not accidentally revoke all other devices unless the user chooses that action.

### Synchronized record

A versioned piece of user-owned data whose category is approved for synchronization. Each record has an owner, stable identifier, schema/version, revision metadata and deletion state.

## Account and device flows

### Initial server setup

1. Operator deploys the server and completes secure first-run setup.
2. Server bootstraps an initial administrator through a one-time or otherwise protected process.
3. Administrator configures registration/invitation policy.
4. Users receive accounts according to that policy.

### Linking a desktop device

1. User enters or scans the intended server address.
2. Client validates the server identity and establishes a protected connection.
3. User authenticates.
4. Server authorizes device registration.
5. Client stores its device credential using the platform's protected local storage where available.
6. User can view and revoke the device from account settings.

The exact pairing UX (password login, short-lived pairing code, QR code or passkey flow) is intentionally undecided.

### Linking another device

A second desktop or browser signs into the same server account and receives only that account's authorized data. It does not inherit local filesystem access or secrets from the first device.

## Data classification and synchronization policy

Synchronization must be opt-in by data category, not a blanket upload of the entire local profile.

| Data category | Initial policy direction | Reason |
|---|---|---|
| UI preferences and layout | Candidate for sync | Portable, low sensitivity |
| Project metadata and pinned-project lists | Candidate for sync | Useful across devices; paths are device-specific |
| Recent activity metadata | Optional, configurable | May reveal work patterns or project names |
| Project file contents | Not synced by default | Large, sensitive and better handled by Git or a separately designed file-sync feature |
| Local absolute paths | Device-specific mapping only | Paths differ between machines |
| API keys and provider secrets | Never sync in plaintext | High-impact credentials |
| SSH private keys and OS credentials | Never sync in plaintext | Must remain under device/OS control by default |
| AI conversation history | Explicit product/privacy decision | May contain sensitive project information |
| Device-specific integration state | Local only unless explicitly designed | Bound to local OS and installed tools |

Any later encrypted secret synchronization would require a separate end-to-end encryption design, key recovery model and threat review. Server-side encryption at rest alone does not mean the server cannot read data.

## Synchronization protocol requirements

The eventual protocol should support:
- Authenticated, authorized pull and push operations.
- Per-user data scoping enforced on the server.
- Stable record IDs and schema versions.
- Incremental change cursors or equivalent efficient updates.
- Idempotency keys for retryable writes.
- Revision numbers or causal metadata for concurrent edits.
- Deletion tombstones and documented retention.
- Bounded payload sizes and validation.
- Backoff and resumability after offline periods.
- Clear client-visible sync status and errors.

Do not design sync as “last write wins” for every record. Conflict handling must match the data type. For example, simple preferences may use a documented merge policy, while more complex records should surface a conflict or preserve both versions.

## Offline and conflict behaviour

- A disconnected desktop continues to use its local data.
- The client records pending synchronization changes locally only for categories the user has enabled.
- Pending changes must be visible and cancellable where safe.
- On reconnect, the client exchanges changes and resolves conflicts according to the category's policy.
- A server must not silently overwrite a newer local revision.
- Deletions require special care so stale clients do not resurrect deleted records indefinitely.
- A user who revokes a device should cause its future server requests to be rejected; local data already present on that device cannot be assumed to be remotely erased.

## Multi-user isolation

- Every user-owned query and mutation is scoped by the authenticated principal on the server.
- Never trust an owner ID supplied by the browser or desktop client.
- Instance administrators receive only the access necessary to operate the instance; administrative status should not automatically mean unrestricted visibility into private user content unless a clearly disclosed policy and product requirement explicitly define it.
- Invitations, role changes, account disablement and device revocation are audited.
- Account deletion must define treatment of owned records, backups and audit history.

## Security and privacy requirements

- Use TLS for remote connections.
- Store passwords using a modern password-hashing scheme if password authentication is selected.
- Protect session secrets and rotate/revoke them appropriately.
- Store device credentials using OS-protected storage when available.
- Keep secrets out of logs, analytics, error messages and AI prompts.
- Provide account export and deletion policies.
- Document backup encryption and access controls.
- Threat-model compromised devices, stolen sessions, malicious server operators and malicious clients.

## Open decisions

- Authentication and account recovery method.
- Whether the first release supports invitations only or open registration.
- Exact roles and administrative visibility.
- Syncable record catalogue and per-category defaults.
- Conflict-resolution strategy for each record type.
- Server-side versus end-to-end encryption boundaries.
- Device pairing and revocation UX.
- Data retention, export and account deletion policy.
