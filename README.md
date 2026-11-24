# ATLAS

**ATLAS — Your Development Command Centre.**

ATLAS is a planned desktop workspace that brings projects, developer tools, applications, workflows, system information and AI assistance into one place. It is designed to be a useful starting point for daily development without replacing the IDEs, terminals and specialist tools developers already use.

## Technology direction

The selected application stack is **Electron + React + TypeScript + Node.js**. Electron provides a consistent Chromium-based UI runtime across the initial Windows and Linux targets; Node.js powers desktop-side services and integrations. Rust is optional only if a future, specific native/performance requirement justifies it.

## Release plan

- **ATLAS Core — target: mid-March 2027:** the first focused, usable foundation.
- **ATLAS Pro — development target: late March 2027 onward:** a larger milestone that builds on Core.

Dates are planning targets and may change as implementation and testing progress.

See [Core vs Pro](CORE_VS_PRO.md) for the current feature split and [Release and signing plan](RELEASE_AND_SIGNING.md) for packaging, code-signing concerns and distribution decisions.

## Documentation

- [Master specification](ATLAS_MASTER_SPEC.md) — product direction, selected stack and shared rules.
- [Core vs Pro](CORE_VS_PRO.md) — release scope.
- [Release and signing plan](RELEASE_AND_SIGNING.md) — Windows/Linux release packaging and signing research.
- [Core features](Features/Core/) and [Pro features](Features/Pro/) — detailed feature specifications.

Feature documents describe planned behaviour; they do not imply implementation. Status must be based on the actual codebase and verified tests.
