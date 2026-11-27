# ATLAS deployment modes

**Status:** Proposed product and architecture direction. This document records the accepted direction from planning discussions; it does not claim that either deployment mode or server exists in code.

ATLAS should be usable in two deployment modes without becoming two unrelated products:

1. **Standalone** — the desktop application stores its data on the user's own device and does not require an ATLAS account, server or network connection for ordinary local functionality.
2. **Self-hosted** — the user or organisation deploys an ATLAS Server on infrastructure they control. Desktop clients and the hosted web client can connect to that server for accounts, shared identity and synchronization.

The server is optional. It must extend ATLAS, not become a dependency for the standalone experience.

## Product goals

- Preserve a complete, useful local-first desktop experience.
- Let users opt into a server they operate and administer.
- Support multiple independent user accounts on one server.
- Let one user connect multiple authorised devices to the same account.
- Provide a browser-accessible ATLAS interface served by the self-hosted deployment.
- Avoid requiring an ATLAS-operated cloud service.
- Make migration from standalone to self-hosted possible without reinstalling the desktop application.

## Mode comparison

| Capability | Standalone | Self-hosted |
|---|---|---|
| Desktop application | Yes | Yes |
| Local workspace data | Yes | Yes, with a local working copy/cache as appropriate |
| ATLAS account | Not required | Server-managed account |
| Server required | No | Yes, for server-backed features |
| Cross-device sync | No built-in server sync | Yes, for explicitly supported data |
| Browser web client | Not included in standalone mode | Served by the ATLAS Server deployment |
| Multiple users | Device-local OS user separation | Server accounts with isolated data and roles |
| Works during server outage | Fully, for local features | Local desktop functionality remains available; server-only operations pause |

## Mode selection and lifecycle

- First launch should allow the user to continue in Standalone mode without creating an account.
- Connecting to a server should be an explicit, reversible setup action.
- The client should clearly show whether it is Standalone, connected to a named server, disconnected from that server, or undergoing synchronization.
- A server URL change must not silently move or upload local data.
- Disconnecting must not erase local data. The user should be able to choose whether to retain or remove a local account's cached server data, with clear consequences.
- Moving from Standalone to Self-hosted should be an explicit import/enrolment flow with a preview of what will be transferred.
- Moving away from a server should provide an export path for user-owned data where technically and legally appropriate.

## Local-first guarantees

- Server connectivity must not be required to open the desktop app or access data already stored locally.
- A server outage must not corrupt local work or cause the app to block at startup.
- Features that genuinely require the server must report that dependency and fail gracefully.
- The client must not silently queue sensitive operations for later execution. Any queued work must be visible, cancellable and re-authorised when necessary.
- The local device remains responsible for local filesystem, process and application-launch permissions.

## Data ownership boundaries

The server is a synchronization and coordination service, not a remote replacement for the user's computer. It does not automatically gain access to local project directories, terminals, installed applications or local secrets.

Each data category must have an explicit storage and sync policy:
- Device-local only.
- User-account synchronized.
- Server/organisation managed.
- Derived/cache data that can be regenerated.

Do not assume every setting, credential, project file or activity record should synchronize.

## Relationship to Core and Pro

This is a product-wide architectural direction, not a decision that all server functionality must ship in the first Core release. Feature allocation, release sequencing, hosting requirements and any future plan restrictions require explicit product decisions. Do not invent paywalls or claim a feature is Core/Pro until the feature matrix is updated.

## Acceptance criteria for the architecture

- Standalone startup and core local workflows have no server dependency.
- A user can explicitly connect a desktop client to a configured self-hosted instance.
- Multiple accounts on one instance have isolated user data.
- One account can authorize more than one device.
- A web client is served by the instance and uses the same identity and authorization model.
- Server disconnection does not destroy or lock local work.
- Data categories and conflict behaviour are documented before sync implementation.
- Security review covers account isolation, device revocation, transport security, backup and restore, and secret handling.
