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
- **Cross-platform by design:** consider Windows, Linux and macOS, documenting unverified platform differences.

## Release model

- **ATLAS Core:** first functional foundation; approximately 40 hours is a planning estimate, not an event threshold.
- **ATLAS Pro:** larger milestone building on Core with advanced capabilities.
- **ATLAS:** long-term product vision.

See [CORE_VS_PRO.md](CORE_VS_PRO.md) for feature allocation. Feature-specific scope belongs in the individual documents under [Features/Core](Features/Core/) and [Features/Pro](Features/Pro/).

## Shared architecture

ATLAS should separate its desktop UI, project and system services, AI provider adapters, action protocol, permission system and platform integrations. Proposed technology direction (subject to validation) includes Tauri 2, React/TypeScript, local storage such as SQLite, platform credential storage and provider adapters.

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

## Privacy and platform support

Store settings and user-controlled workspace data locally by default. Optional cloud AI, downloads, updates and integrations must identify the external service and information shared. Windows, Linux and macOS are targets; compatibility claims require platform-specific validation.

## Planning and verification

Keep planned, in-progress, implemented and tested work distinct. Record meaningful platform limitations, test results and deviations from the plan. For Hack Club or other programmes, follow current official rules, disclose prior work and track eligible work honestly; never promise rewards or eligibility.

## Documentation map

- [README](README.md) — repository introduction.
- [Core vs Pro](CORE_VS_PRO.md) — release split.
- [Core features](Features/Core/) and [Pro features](Features/Pro/) — feature-specific requirements.

Keep this document focused on product-wide direction and rules; put detailed behaviour, boundaries, dependencies and acceptance criteria in the corresponding feature document.
