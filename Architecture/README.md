# Architecture documentation

This directory records the intended technical architecture and the boundaries that must remain clear as ATLAS evolves.

## Selected stack

- Electron desktop runtime.
- React + TypeScript renderer.
- Node.js application services in the Electron main process or controlled utility processes.
- Chromium-rendered UI for consistent rendering across Windows and Linux.

Rust is optional only if a measured requirement justifies a native module. It is not part of the required initial stack.

## Documents

- [System overview](SYSTEM_OVERVIEW.md)
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
6. Secrets are never placed in model-visible prompts, renderer state or ordinary logs.
7. Expensive integrations are loaded on demand.

## Status

These documents describe intended architecture. They must be revisited against the actual application repository and implementation as work begins.
