# ATLAS — Master Specification

> **ATLAS — Your Development Command Centre.** One workspace to launch, organise, monitor and manage development work, with an integrated AI layer.

**Status:** Product overview and architectural guide. Features are planned unless their implementation is independently verified.

## Product vision

ATLAS is a developer workspace and command centre: a single starting point for projects, applications, developer tools, workflows, system information and AI-assisted development. It complements specialist IDEs, terminals and developer applications rather than replacing them.

## Product principles

- **Local-first:** ordinary desktop functionality should not require an ATLAS-hosted account or backend.
- **Privacy-first:** disclose external data sharing and protect credentials and project information.
- **User control:** installations, sensitive actions and external sharing require clear consent.
- **Useful before clever:** prioritise complete workflows over feature count.
- **Explain uncertainty:** distinguish verified facts from estimates and AI inferences.
- **Cross-platform by design:** Windows and Linux are the initial release targets. Other platforms require a deliberate support decision and platform-specific validation.
- **Self-hosting as an option:** users may eventually run their own ATLAS Server; this must not make the standalone desktop app dependent on a server.

## Release model and schedule

- **ATLAS Core — target: mid-March 2027:** first functional foundation; useful on its own and built on the shared architecture.
- **ATLAS Pro — development target: late March 2027 onward:** larger milestone building on Core with advanced capabilities.
- **ATLAS:** long-term product vision.

Dates are planning targets, not guarantees. See [CORE_VS_PRO.md](CORE_VS_PRO.md) for feature allocation and [RELEASE_AND_SIGNING.md](RELEASE_AND_SIGNING.md) for packaging and distribution planning.

## Technology direction

The selected desktop application stack is:

- **Electron** for the desktop runtime and application packaging.
- **React + TypeScript** for the user interface.
- **Node.js** for application services, process management, integrations and the JavaScript ecosystem.

Electron's bundled Chromium provides a more predictable rendering environment across supported systems than relying on each operating system's separately installed web view. This is a consistency and ecosystem decision, not a claim that Electron is inherently lighter than native alternatives.

Rust is not a required part of the initial stack. A Rust component may be considered later for a clearly justified native or performance-sensitive task, but it should not be added without a concrete need.

### Performance approach

Optimise for responsiveness and sensible resource use without sacrificing useful functionality to chase an arbitrary tiny memory target. Measure the complete ATLAS process tree, including Electron's renderer and utility processes, under cold start, idle and representative active workloads. Distinguish ATLAS's own resource use from separately launched tools such as IDEs, Docker and local AI models. Load expensive features only when needed; do not start local models or heavyweight services without user intent.

## Shared architecture

ATLAS should separate its desktop UI, project and system services, AI provider adapters, action protocol, permission system and platform integrations. Keep platform-specific operations behind well-defined interfaces and validate behaviour on Windows and Linux independently.

### Optional deployment modes

ATLAS is planned to support two deployment modes within one product:

1. **Standalone:** desktop application with local data storage. No ATLAS account, server or network connection is required for ordinary local functionality.
2. **Self-hosted:** an operator deploys an ATLAS Server on infrastructure they control. Multiple user accounts and multiple authorized devices can connect to that instance, and the instance is intended to serve an ATLAS Web interface.

The self-hosted mode is an optional extension. Standalone users must retain local access when offline or when no server is configured. Connecting to a server is explicit and reversible. Data migration and synchronization must be transparent and category-based.

The proposed server responsibilities include account/session management, device registration and revocation, server-side authorization, synchronization of explicitly supported data, administration and hosting the browser client. Docker is the intended deployment direction, with persistent data stored outside the disposable container filesystem. Exact image, port, database, API and deployment contract remain undecided.

The web client shares the server identity and authorization model but cannot directly perform privileged desktop operations such as launching local applications, arbitrary filesystem access or local terminal execution. Such capabilities remain local to the desktop app unless a separately reviewed companion architecture is designed.

See [Architecture/DEPLOYMENT_MODES.md](Architecture/DEPLOYMENT_MODES.md), [Architecture/SELF_HOSTED_SERVER.md](Architecture/SELF_HOSTED_SERVER.md), [Architecture/WEB_CLIENT.md](Architecture/WEB_CLIENT.md) and [Architecture/SYNC_IDENTITY_MODEL.md](Architecture/SYNC_IDENTITY_MODEL.md).

### AI modes

- **Helper/Tutor:** explains and guides; cannot modify files or execute modifying actions.
- **Developer:** performs requested implementation work through approved actions.
- **Hybrid:** performs work and explains decisions and changes.

Chat and Voice can have independent modes. Voice follows Chat by default unless the user chooses an override. Voice is an additional interface to the shared ATLAS core, not a separate assistant. Core Voice Essentials provides push-to-talk and basic spoken interaction; Pro adds advanced voice and optional Visual Context Mode.

## Security invariant

**AI requests; ATLAS validates, authorises and executes.**

- AI-generated requests cannot decide whether approval is required.
- The Permission Manager independently evaluates every action.
- AI cannot approve its own requests, grant itself permissions or change security settings.
- File operations must be constrained to authorised locations and protect against path traversal and unsafe links.
- Commands must be validated; sensitive operations require appropriate approval.
- Secrets must remain outside model-visible context and logs.
- Voice and screenshot context never bypass the same permission boundaries.
- Agent-initiated Git pushes are OFF by default and remain subject to operation-specific controls.
- Server authorization must be enforced server-side for every account-owned object; client-side visibility is not a security boundary.
- Server sync must not upload local secrets, SSH private keys or entire project directories by default.

## Privacy and platform support

Store settings and user-controlled workspace data locally by default. Optional cloud AI, downloads, updates and integrations must identify the external service and information shared. Windows and Linux are the initial supported targets; compatibility claims require platform-specific validation.

For self-hosting, users control the server infrastructure and its backups, network exposure and updates. Remote deployments require protected transport and a deliberate network/reverse-proxy configuration; Docker port mapping alone is not a complete internet-exposure or security setup.

## Planning and verification

Keep planned, in-progress, implemented and tested work distinct. Record meaningful platform limitations, test results and deviations from the plan. For Hack Club or other programmes, follow current official rules, disclose prior work and track eligible work honestly; never promise rewards or eligibility.

## Documentation map

The planning repository is organised by responsibility:

- [Design/](Design/README.md) — Figma-first workflow, design system, interactive prototype specification, screen inventory, component library and February handoff.
- [Architecture/](Architecture/README.md) — desktop architecture, deployment modes, self-hosted server, web client, identity/sync, Electron security, IPC, AAP and ADRs.
- [Product/](Product/README.md) — product principles, Core scope and user journeys.
- [Research/](Research/README.md) — reference-app evaluations and research log.
- [Planning/](Planning/README.md) — roadmap, decision register and risk register.
- [Quality/](Quality/README.md) — test strategy, accessibility and usability.
- [Features/Core/](Features/Core/) and [Features/Pro/](Features/Pro/) — detailed feature requirements.
- [Release and signing plan](RELEASE_AND_SIGNING.md) — packaging, code signing and distribution.

Figma is the canonical visual/interaction specification through January 2027. February is the planned handoff to React + TypeScript implementation. The application source and tested runtime behaviour become authoritative for what is implemented.

Keep this document focused on product-wide direction and rules; put detailed behaviour, boundaries, dependencies and acceptance criteria in the corresponding documents.
