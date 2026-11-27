# Architecture documentation

This directory records the intended technical architecture and the boundaries that must remain clear as ATLAS evolves.

## Selected desktop stack

- Electron desktop runtime.
- React + TypeScript renderer.
- Node.js application services in the Electron main process or controlled utility processes.
- Chromium-rendered UI for consistent rendering across Windows and Linux.

Rust is optional only if a measured requirement justifies a native module. It is not part of the required initial stack.

## System architecture

- [System overview](SYSTEM_OVERVIEW.md)
- [Deployment modes: Standalone and Self-hosted](DEPLOYMENT_MODES.md)
- [Self-hosted server architecture](SELF_HOSTED_SERVER.md)
- [ATLAS Web client](WEB_CLIENT.md)
- [Identity, devices and synchronization model](SYNC_IDENTITY_MODEL.md)
- [Electron security model](ELECTRON_SECURITY.md)
- [IPC contract](IPC_CONTRACT.md)
- [AAP and permission architecture](AAP_AND_PERMISSIONS.md)
- [Architecture decision records](DECISIONS/README.md)

## Architectural boundaries

1. Renderer code is untrusted UI code; it must not receive unrestricted Node.js access.
2. A narrow preload API exposes only explicit capabilities.
3. Main/services validate all IPC input and enforce authorization.
4. AI providers can propose structured actions but cannot grant permission.
5. Platform-specific operations sit behind adapters and are tested on each target.
6. Secrets are never placed in model-visible context, renderer state or ordinary logs.
7. Expensive integrations are loaded on demand.
8. Standalone desktop functionality must not depend on an ATLAS Server.
9. Server authorization is enforced on the server for every user-owned object and operation.
10. Browser clients do not inherit desktop filesystem, process or application-launch privileges.
11. Synchronization is category-based and explicit; local secrets and project files are not uploaded by default.

## Status

The standalone desktop architecture remains the baseline. Self-hosted server and browser access are proposed extensions documented for future design and implementation. These documents do not imply that a server, Docker image, sync protocol or web client has been implemented.

Revisit these documents against the actual application repository as implementation begins.
