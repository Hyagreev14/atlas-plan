# ATLAS CORE V1.0 — SCOPE & ARCHITECTURE LOCK

**Status:** Approved scope  
**Version:** 1.0  
**Target development:** April – early July 2027 (12 weeks)  
**Development model:** Solo developer  
**Primary platform:** Windows  
**Architecture:** Local-first desktop application

---

## 1. Product Objective

ATLAS Core is a standalone developer workspace that brings projects, development tools, and local AI assistance into one organized desktop application.

It should make starting and managing development sessions easier without attempting to replace specialist IDEs, terminals, or other development tools.

**Core principle:** Ship a useful standalone desktop application first. Keep its architecture maintainable without prematurely implementing future Pro infrastructure.

Core must work without a remote server, cloud account, or AI connection.

## 2. Locked Technology Stack

| Component | Technology |
|---|---|
| Desktop runtime | Electron |
| Frontend | React + TypeScript |
| Backend logic | Node.js |
| Local AI | Ollama |
| Initial AI models | Small local models, including 3B-class models |
| Local storage | SQLite or JSON, selected according to actual requirements |
| Primary OS | Windows |

### Why Electron?

Electron is retained because it fits the existing React, TypeScript, and Node.js skill set.

Switching to Tauri would introduce Rust and additional development complexity during a limited solo-development window. Its potential resource advantages do not justify that disruption for v1.0.

### Electron performance requirements

- One primary application window.
- Lazy-load screens and expensive integrations.
- Avoid unnecessary background processes and polling.
- Keep the preload API small.
- Do not initialize or load AI models automatically.
- Measure actual RAM and CPU usage on the target hardware.

## 3. Core v1.0 — Four Capability Groups

### A. Developer Home & Project Hub

- Developer dashboard.
- Register and manage projects.
- Display basic project information.
- Recently used projects.
- Open registered projects in their configured IDE.
- Basic project-specific actions.

### B. Universal App Launcher

- Register desktop applications.
- Launch registered applications.
- Save application launch configurations.
- Create and launch saved application groups.
- Connect projects with their preferred development tools.

### C. AI Workspace

- Connect to a locally running Ollama instance.
- Detect available local models.
- Select an AI model.
- Stream AI responses.
- Explicitly select project context.
- Support three simple interaction modes:

| Mode | Purpose |
|---|---|
| Helper | Guidance and explanations |
| Developer | Development assistance |
| Hybrid | Combination of both |

AI functionality must remain optional. The rest of ATLAS must work when Ollama is unavailable.

### D. Core Services & Permission System

- Local settings and project metadata.
- Secure Electron IPC.
- Main-process action validation.
- Application and project launching.
- Permission checks.
- Explicit user confirmations.
- Structured action results and error handling.

The Permission Manager and AAP are foundational infrastructure, not a general-purpose autonomous agent framework.

## 4. AAP v1.0 & Permission Manager

AAP stands for **ATLAS Action Protocol**.

AAP v1.0 is strictly limited to three action types:

1. **Open registered projects:** Open a registered project folder using its configured IDE.
2. **Launch registered applications:** Launch a whitelisted desktop application or saved application group.
3. **Run registered project scripts:** Execute a previously registered project script after explicit user confirmation.

### Security requirements

- The Electron main process validates and executes actions.
- The renderer and AI provider cannot grant themselves permissions.
- Only registered projects, applications, and scripts may be invoked.
- Script execution must display the exact command, arguments, and working directory.
- Every script execution requires explicit user confirmation.
- Validate the registered script and project scope before execution.
- Never silently execute scripts.
- Never execute arbitrary AI-generated shell commands.
- Return structured success or failure results.

### Explicitly excluded from AAP v1.0

- Plugin sandboxes.
- Custom DSLs or scripting languages.
- Background autonomous agents.
- General-purpose agent orchestration.
- Arbitrary command execution.
- Complex workflow automation.

Keep AAP small, typed, predictable, and testable.

## 5. Developer Tool Management

Automatic developer-tool installation is excluded from Core v1.0.

Do not implement:
- Automatic installers.
- Package-manager wrappers such as `winget`, `apt`, or `brew`.
- Automatic PATH modification.
- Silent software installation.
- Cross-platform installation orchestration.

Basic detection is allowed. For example, ATLAS may check whether Git or Ollama is installed and display its availability or version.

Users remain responsible for installing and configuring their development tools.

## 6. Hardware & AI Guardrails

### Target development hardware

- Intel Core i5 processor.
- 8 GB DDR4 RAM.
- Intel integrated graphics.
- Windows.
- WSL2 available for development.
- Ollama with small local models, including 3B-class models.

ATLAS must be designed and tested with these resource constraints in mind.

### Ollama startup behavior

- Never automatically load an Ollama model when ATLAS starts.
- Do not assume Ollama is running.
- Connect when the user requests AI functionality.
- Allow model selection.
- Communicate model availability and resource expectations.
- Keep the application usable without AI.

### Context Budgeter

Context overflow and slow inference are major technical risks when using small local models.

ATLAS must implement a Context Budgeter that:

- Limits injected project context.
- Prefers relevant snippets and metadata over complete files.
- Avoids injecting entire project trees.
- Avoids large package-lock files and dependency trees.
- Avoids unnecessarily long terminal logs.
- Allows users to inspect and control included context.

**Initial context target:** Approximately 600–800 tokens of injected project context for a 3B model configured around a 2,048-token context window.

This is a starting target, not a universal fixed limit.

The budget must be configurable and account for:
- System instructions.
- Conversation history.
- User's question.
- Injected project context.
- Expected response space.

The selected model's actual context configuration must always be respected.

## 7. Electron Security Requirements

Security must be included in the initial architecture.

Minimum requirements:

- `contextIsolation: true`
- `nodeIntegration: false`
- Renderer sandboxing enabled where compatible.
- Narrow, explicitly defined preload API.
- Main-process validation of IPC requests.
- Restricted application navigation and external window creation.
- Restrictive Content Security Policy.
- No arbitrary renderer access to Node.js or operating-system APIs.
- No arbitrary AI-controlled command execution.
- Keep secrets out of model context and ordinary logs.

The renderer is not trusted to make security decisions.

## 8. Explicit Exclusions & Deferrals

The following features are outside Core v1.0:

| Feature | Decision |
|---|---|
| Automatic developer-tool installation | Deferred |
| Full Developer Tool Manager | Deferred |
| Complex workflow automation | Deferred |
| General-purpose autonomous agents | Excluded |
| Plugin ecosystem and sandboxing | Deferred |
| Advanced Git Centre | Deferred |
| Project Doctor | Deferred |
| Workspace Snapshots | Deferred |
| Activity Timeline | Deferred |
| Advanced Hardware Profiler | Deferred |
| Voice Essentials | Deferred |
| Advanced Voice | Deferred |
| Visual Context / screenshot understanding | Deferred |
| Remote Development Manager | Pro |
| Web client | Pro |
| Multi-device synchronization | Pro |
| Self-hosted ATLAS server | Pro |
| Remote authentication and device registration | Pro |
| Cloud or server-side project storage | Pro |
| Docker deployment for ATLAS Pro | Future |

These features may be reconsidered after Core has shipped and been validated.

**Scope rule:** Do not quietly introduce deferred features during Core development. Any proposed addition must be evaluated against the 12-week schedule and must replace or reduce another commitment.

## 9. Core vs Pro Architecture Boundary

### Core

- Standalone local desktop application.
- Local project and application management.
- Local AI through Ollama.
- Local settings and storage.
- Local permission and action execution.
- No server dependency.
- No cloud account requirement.

### Pro / Future v2

- Optional self-hosted server.
- Web client.
- Multi-device access.
- Remote development.
- Synchronization.
- Advanced collaboration and orchestration.

Do not build fake synchronization queues, distributed authentication, conflict-resolution systems, or remote APIs into Core just in case they are needed later.

Keep local storage clean and documented so migration can be considered when Pro is actually developed.

## 10. Overall Project Timeline

| Period | Focus | Goal |
|---|---|---|
| Now – January 2027 | Specifications and Figma | Finalize product requirements, architecture, and UI/UX |
| February – March 2027 | Birthday eligibility, Hack Club warmup, and warmup project delivery | Complete and ship the warmup project, then prepare for the main ATLAS build |
| April – early July 2027 | ATLAS Core development | Complete the 12-week Core v1.0 development cycle |

### ATLAS Core — 12-Week Development Plan

| Weeks | Focus | Expected outcome |
|---|---|---|
| 1–2 | Electron foundation, project structure, secure IPC, local storage | Launchable desktop foundation |
| 3–4 | Developer Home and Project Hub | Register, view, and open projects |
| 5–6 | Universal App Launcher | Register and launch apps and groups |
| 7–8 | AI Workspace and Ollama integration | Local model selection and streaming |
| 9–10 | AAP v1.0 and Permission Manager | Three validated action types |
| 11–12 | Integration, testing, performance, and release preparation | Core v1.0 release candidate |

The exact calendar dates should be established when the April start date is confirmed.

### Schedule rules

- Prioritize working end-to-end functionality.
- Avoid expanding the feature list.
- Do not introduce Pro infrastructure.
- Reserve the final two weeks for integration, testing, and stabilization.
- Defer features that threaten the release target.

## 11. Definition of Done — Core v1.0

Core v1.0 is ready when:

1. ATLAS launches as a standalone desktop application.
2. Users can register, view, and open projects.
3. Users can register and launch applications and saved groups.
4. Users can connect to Ollama and select a local model.
5. AI responses support streaming.
6. Project context is explicitly selected and budgeted.
7. AAP supports only the three defined action types.
8. All executable actions are validated by the main process.
9. Registered scripts require explicit confirmation.
10. ATLAS remains usable when Ollama is unavailable.
11. No remote server or cloud account is required.
12. Resource usage has been measured on the target hardware.
13. Critical workflows have been tested and documented.

## 12. Final Scope-Lock Principles

- Build a small, excellent standalone ATLAS first.
- Prefer working functionality over an impressive feature checklist.
- Keep AI optional and user-controlled.
- Keep execution explicit, restricted, and validated.
- Measure performance on actual hardware.
- Avoid premature Pro architecture.
- Protect the 12-week schedule by deferring nonessential features.

**ATLAS Core v1.0 is the foundation of the long-term product, not the entire long-term vision.**
