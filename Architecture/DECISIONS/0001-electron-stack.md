# ADR-0001: Electron desktop stack

- **Status:** Accepted
- **Date:** 24 November 2026
- **Decision owner:** ATLAS project owner

## Context

ATLAS needs a desktop interface for Windows and Linux with a consistent rendering environment, a large ecosystem for desktop integrations and a productive UI development workflow. Tauri was considered, including its smaller native-runtime footprint, but reliance on each operating system's installed WebView raised a concern about cross-platform rendering consistency.

## Decision

Use Electron with React + TypeScript for the renderer and Node.js for trusted desktop services. Chromium is bundled with Electron, providing a more predictable rendering baseline across supported platforms.

Rust is not required for the initial architecture. It may be introduced later only for a specific measured native or performance need.

## Consequences

- More bundled runtime weight than a minimal native shell; manage it through lazy loading and measurement.
- Familiar web UI and Node.js ecosystem.
- Explicit Electron security boundaries are mandatory.
- Windows and Linux behaviour still requires real platform testing.
- Do not reopen framework selection without new evidence or a concrete blocker.
