# ATLAS — Product Vision & Feature Specification

> **ATLAS — Your Development Command Centre.**  
> One workspace to launch, organise, monitor and manage everything involved in software development, with an integrated AI layer.

**Document status:** Product concept / living specification  
**Implementation status:** Not yet implemented  
**Repository location:** `ATLAS/ATLAS_MASTER_SPEC.md`  
**Product direction:** Local-first, privacy-first, cross-platform desktop software

---

## Contents

1. [Product vision](#1-product-vision)
2. [Product principles](#2-product-principles)
3. [Who ATLAS is for](#3-who-atlas-is-for)
4. [Application structure](#4-application-structure)
5. [Developer Home](#5-developer-home)
6. [Project Hub](#6-project-hub)
7. [Universal App Launcher](#7-universal-app-launcher)
8. [Developer Tool Manager](#8-developer-tool-manager)
9. [Integrated AI Workspace](#9-integrated-ai-workspace)
10. [AI Model Manager](#10-ai-model-manager)
11. [Hardware Profiler & Compatibility Engine](#11-hardware-profiler--compatibility-engine)
12. [System Monitor](#12-system-monitor)
13. [Git Centre](#13-git-centre)
14. [Workflow Automation](#14-workflow-automation)
15. [Developer Productivity Tools](#15-developer-productivity-tools)
16. [Secret Vault & Security](#16-secret-vault--security)
17. [Privacy, networking & offline operation](#17-privacy-networking--offline-operation)
18. [Permissions & action safety](#18-permissions--action-safety)
19. [Cross-platform support](#19-cross-platform-support)
20. [Proposed technical architecture](#20-proposed-technical-architecture)
21. [Data storage](#21-data-storage)
22. [UX, accessibility & customisation](#22-ux-accessibility--customisation)
23. [Reliability, diagnostics & updates](#23-reliability-diagnostics--updates)
24. [Extension system](#24-extension-system)
25. [Non-goals and boundaries](#25-non-goals-and-boundaries)
26. [Suggested delivery roadmap](#26-suggested-delivery-roadmap)
27. [Quality and acceptance criteria](#27-quality-and-acceptance-criteria)
28. [Open product decisions](#28-open-product-decisions)
29. [Glossary](#29-glossary)
30. [AI handoff document & release plan](#30-ai-handoff-document--release-plan)
31. [Hack Club Context, Event Goals & Rewards](#31-hack-club-context-event-goals--rewards)
32. [Additional Core & Pro Feature Decisions](#32-additional-core--pro-feature-decisions)

---

# 1. Product vision

ATLAS should be the application a developer opens first when they sit down to work.

Developers often start a work session by opening several unrelated applications: an IDE, terminal, browser, Git client, Docker, project folders, documentation, monitoring utilities and perhaps an AI assistant. ATLAS brings the entry points to those tools into one coherent workspace.

ATLAS is **not intended to replace every IDE, terminal, editor or specialist application**. It should make those applications easier to discover, launch, organise and use together.

The central product identity is a **developer workspace and command centre**. AI is an integrated capability that helps developers understand and work on projects, but AI is not the only reason to use ATLAS.

### Core promise

- Open ATLAS and quickly understand what is happening across your development work.
- Open a project and launch the tools that belong to it.
- Discover missing developer tools and choose whether to install them.
- Monitor the computer and development processes.
- Automate repeatable workspace setup.
- Use AI in a mode that matches the developer's preferred way of working.
- Keep private data and secrets under the user's control.

### Product positioning

**ATLAS — Your Development Command Centre.**

A single desktop workspace for projects, applications, tools, workflows, system information and AI-assisted development.

---

# 2. Product principles

These principles should guide feature design and implementation.

## 2.1 Local-first

The core application should work on the user's computer. Projects, settings, notes, project context, history and sensitive information should be stored locally by default.

ATLAS must not require an ATLAS cloud account or an ATLAS-hosted backend for ordinary desktop functionality.

## 2.2 Privacy-first

- Secrets must never be uploaded to ATLAS servers.
- API keys and credentials must be encrypted locally.
- Private project data must not be sent to an AI provider without a clear user choice and disclosure.
- Network-dependent features must explain what external service they contact.
- Local-only operation should be available.
- Diagnostics must not silently collect project contents or secrets.

## 2.3 User control

- Ask before installing software.
- Ask before running sensitive or potentially destructive commands.
- Ask before sending project content to external AI services.
- Let users deny, cancel, retry or change decisions.
- Do not silently change a user's working mode or security settings.
- Make automated actions visible and inspectable.

## 2.4 Useful before clever

ATLAS should make common development tasks faster and easier. Features should solve real workflow problems rather than exist only to make the application look futuristic.

## 2.5 Respect existing tools

ATLAS should integrate with existing IDEs, terminals, runtimes and developer applications. It should not force developers to abandon tools they already like.

## 2.6 Explain uncertainty

Hardware compatibility, model requirements, automatic project detection and tool recommendations can involve estimates. ATLAS must distinguish verified facts from estimates and clearly communicate uncertainty.

## 2.7 Cross-platform by design

Windows, Linux and macOS should be considered in architecture and UX decisions from the beginning. Platform-specific capabilities may differ, but those differences should be documented rather than hidden.

---

# 3. Who ATLAS is for

ATLAS is intended for developers who use multiple tools and want a consistent starting point for their work.

Potential users include:

- Students learning software development.
- Hobbyist developers.
- Web and backend developers.
- Game developers.
- Application developers.
- Developers working with containers and virtual machines.
- Developers experimenting with local or hosted AI models.
- Experienced developers managing several repositories and environments.

The application should be approachable for beginners without becoming restrictive for advanced users.

---

# 4. Application structure

The proposed primary navigation is:

| Section | Purpose |
| --- | --- |
| **Home** | Daily development dashboard |
| **Projects** | Discover and manage development projects |
| **Launcher** | Launch installed applications |
| **Tools** | Discover, install and manage developer tools |
| **AI Workspace** | Integrated AI assistant and project help |
| **Models** | Manage AI models and providers |
| **System** | Hardware and resource monitoring |
| **Workflows** | Automate repeatable development tasks |
| **Git Centre** | View and manage local repositories |
| **Notes** | Developer notes, snippets and reusable commands |
| **Vault** | Securely manage secrets and credentials |
| **Settings** | Configure ATLAS |

The navigation is a starting proposal, not a requirement that every section must appear in the first release. Related features may be grouped differently after usability testing.

---

# 5. Developer Home

The Home screen is the daily starting point. It should provide a useful overview without becoming a wall of charts.

## 5.1 Dashboard content

- Recently opened projects.
- Pinned and favourite projects.
- Recently used applications.
- Quick-launch actions.
- Active development sessions.
- Running local development servers.
- Recent Git activity.
- Pending tool installation requests.
- Active or recently completed workflows.
- Hardware and resource overview.
- Recent AI conversations.
- Tasks and reminders.
- Notifications and actionable warnings.

## 5.2 Customisation

- Add, remove and rearrange dashboard widgets.
- Resize widgets where appropriate.
- Pin frequently used actions.
- Hide information the user does not need.
- Save dashboard layouts.
- Provide a useful default layout for first-time users.

The Home screen should load quickly and should not run expensive scans or benchmarks just to display basic information.

---

# 6. Project Hub

The Project Hub is the central place to organise development projects.

## 6.1 Project discovery

ATLAS may scan directories explicitly selected by the user. It should not silently index the entire computer.

Detection can use project markers and configuration files, for example:

- Git repository metadata.
- `package.json`.
- Python project metadata and requirements files.
- `pyproject.toml`.
- Java build files such as `pom.xml` and Gradle build files.
- Unity project markers.
- Docker Compose files.
- Common framework configuration files.

Detection should be explainable. ATLAS should show why it classified a directory as a particular project type and allow the user to correct the classification.

## 6.2 Project management

- Recent and pinned projects.
- Search and filtering.
- Project tags and categories.
- Custom icons and descriptions.
- Project notes.
- Project-specific settings.
- Project-specific launch profiles.
- Multiple workspace configurations.
- User-defined project locations.
- Remove a project from ATLAS without deleting its files.

## 6.3 Project actions

A project can expose context-aware actions. For example, a Flask project might offer:

- Open in VS Code or another configured editor.
- Open the project folder in the file manager.
- Open a terminal at the project root.
- Activate an existing virtual environment.
- Inspect dependencies.
- View Git status and history.
- Open project documentation.
- Start a development server after showing the command and receiving approval.

ATLAS must not assume that every project uses the same editor, shell, environment manager or startup command.

## 6.4 Project intelligence

ATLAS may maintain local, user-controlled project context:

- Project structure summaries.
- Architecture notes.
- Development decisions.
- Known issues.
- Useful commands.
- Dependency information.
- User-written TODOs.
- AI-generated summaries explicitly accepted by the user.

Users must be able to inspect, edit, export and delete stored project context. The AI must not treat stale notes as guaranteed truth; it should verify important facts against the current project when possible.

## 6.5 Project profiles

Project profiles can describe tools and workflows associated with a project. They are recommendations and configuration, not permission to install or execute anything automatically.

Examples:

- Python / Flask project.
- Node.js / web project.
- Java / Gradle project.
- Unity / game development project.
- General Git repository.

---

# 7. Universal App Launcher

The Launcher provides one searchable place to open applications and saved launch configurations.

## 7.1 Application discovery

Detect installed applications where platform APIs and permissions allow, including examples such as:

- Visual Studio Code.
- Visual Studio.
- IntelliJ IDEA.
- Android Studio.
- Unity.
- Blender.
- Docker Desktop.
- Git GUI clients.
- Windows Terminal and other terminals.
- Browsers.
- WSL distributions.
- Other installed development utilities.

Discovery must be platform-aware and should not assume that every application is installed in a standard location.

## 7.2 Launcher features

- Search applications.
- Pin favourites.
- Categories and tags.
- Recently launched applications.
- Custom application registration.
- Custom display names and icons.
- Configurable executable paths.
- Launch arguments.
- Working directory.
- Environment variables.
- Multiple launch profiles for one application.
- Open several applications together.
- Detect missing executables and explain the problem.

## 7.3 Workspace launch groups

A user could create a group such as **Web Development** that opens an editor, terminal, browser and other selected tools.

Launch groups should support optional delays and dependencies, but failures must be visible. ATLAS should not claim an application launched successfully until it has verified the process launch result.

---

# 8. Developer Tool Manager

The Tool Manager discovers, recommends, installs and tracks developer tools.

## 8.1 Discovery and detection

- Detect installed tools and versions.
- Detect missing dependencies.
- Detect outdated versions.
- Inspect project configuration to identify likely requirements.
- Detect multiple installations and version conflicts where possible.
- Identify the source and location of a detected installation.
- Re-scan after installation or a user-requested refresh.

## 8.2 Example tool categories

| Category | Examples |
| --- | --- |
| Languages and runtimes | Python, Java, Node.js |
| Package managers | pip, npm, pnpm |
| Build tools | Gradle, Maven |
| Version control | Git |
| Containers | Docker |
| Game development | Unity-related tools, Blender |
| IDEs | VS Code, IntelliJ IDEA |
| Project dependencies | Framework and build dependencies |

The list is illustrative. ATLAS should use a maintained catalogue and platform-specific installation strategies rather than hardcoding every tool into the UI.

## 8.3 Installation recommendations

For each recommendation, show:

- Tool name and exact version.
- Why ATLAS believes it is needed.
- Which project or feature needs it.
- Download size when known.
- Expected disk space.
- Official source or package manager.
- Installation location where configurable.
- Whether administrator privileges are required.
- Any known compatibility concerns.

## 8.4 Consent model

Every installation requires explicit user consent.

Available decisions:

- **Install** — proceed with the displayed installation.
- **Deny** — decline the recommendation.
- **Not now** — defer the decision.

Rules:

- Never install silently, even if a project appears to require the tool.
- Detect an existing installation before downloading.
- Never overwrite or replace an existing version without consent.
- Explain administrator privileges before requesting elevation.
- Show progress, errors and verification results.
- Allow cancellation where the underlying installer supports it.
- Explain what functionality may remain unavailable if installation is denied.
- Remember denials at a clearly defined scope to avoid repeated prompts.
- Let the user reconsider from the Tool Manager.
- Use trusted official sources or reputable platform package managers.
- Validate downloaded installers and packages where supported.

## 8.5 Project profiles

Profiles can recommend common tools for a type of work:

- **Python:** Python, pip, venv and Git.
- **Web:** Node.js, npm or another selected package manager, and Git.
- **Java:** JDK, Gradle or Maven, and Git.
- **Game development:** selected game engine tooling, Blender and Git.

Profiles must remain editable. Selecting a profile does not authorise installation.

---

# 9. Integrated AI Workspace

AI is a major ATLAS capability, but it is not the entire product.

## 9.1 Three working modes

### Helper — mentor mode

Helper is for guidance and learning.

- Explains concepts.
- Suggests approaches.
- Guides the user through tasks.
- Explains errors and trade-offs.
- Does not modify project files.
- Does not execute project commands.
- Does not provide ready-made code as its operating behaviour.

Helper must not silently switch to Developer or Hybrid behaviour.

### Developer — implementation mode

Developer performs requested implementation work.

- Inspects project files.
- Plans implementation.
- Modifies files.
- Runs approved commands.
- Runs tests and checks.
- Reports changes and results.
- Identifies remaining work.

### Hybrid — learning plus implementation

Hybrid performs tasks while teaching the user.

- Implements requested changes.
- Explains why an approach was selected.
- Explains what changed and how it works.
- Describes important trade-offs.
- Provides detailed explanations suitable for learning.
- Reports tests, failures and limitations.

## 9.2 Mode settings

- Hybrid is the proposed first-time default.
- Users can switch modes at any time, including during a project.
- The selected mode persists in settings.
- A mode selector appears in the AI chat header.
- The current mode should be clearly visible.
- Switching modes changes behaviour, not necessarily the underlying model.
- Sensitive actions still require approval in every mode.

## 9.3 AI capabilities

Potential capabilities include:

- Explain code and unfamiliar projects.
- Analyse project structure.
- Debug errors.
- Suggest improvements.
- Plan features.
- Implement requested features.
- Review code.
- Explain dependencies and configuration.
- Generate documentation.
- Help with Git.
- Interpret terminal output.
- Help troubleshoot development environments.
- Summarise project context.
- Propose tests and validation steps.

## 9.4 Context and privacy

Before external AI requests, ATLAS should make it clear what context will be sent. Users should be able to control whether the AI can access:

- The current message only.
- Selected files.
- The current project.
- Project notes and saved context.
- Terminal output explicitly shared with the AI.

Secrets, credentials and sensitive values must be filtered or redacted before context is assembled. Redaction is a safety layer, not a guarantee that every possible secret format will be recognised.

---

# 10. AI Model Manager

The Model Manager manages local models and optional external AI providers.

## 10.1 Supported model sources

### A. Ollama catalogue

- Search the available model catalogue.
- View model descriptions and metadata.
- Show model size and quantisation when available.
- Show context information when available.
- Evaluate compatibility.
- Download a selected model after consent.
- Detect models already installed locally.
- Remove models only after explicit confirmation.

ATLAS should retrieve catalogue information on demand rather than downloading or mirroring the entire catalogue.

### B. Manual GGUF import

- Let the user select a local `.gguf` file.
- Inspect metadata and tensor information.
- Estimate memory requirements.
- Check architecture and runtime compatibility.
- Explain missing or inconsistent metadata.
- Use a supported runtime such as llama.cpp or a compatible integration.

A GGUF file is not automatically an Ollama model. ATLAS must not imply that every GGUF file can be loaded directly by every runtime.

### C. Custom Ollama model

- Accept a model name or custom configuration.
- Detect an existing local Ollama installation.
- Detect installed models.
- Connect to the local Ollama service.
- Validate that the selected model can be used.

All model sources must pass through the same compatibility evaluation system.

## 10.2 First-run AI setup

Proposed flow:

1. Inspect the computer's hardware.
2. Present a recommended local model, if a suitable one exists.
3. Ask: **"Would you like ATLAS to select and download a recommended local AI model?"**
4. If the user agrees, select a compatible model and request confirmation before downloading.
5. If the user declines, allow manual model selection or configuration.
6. Test model loading and inference.
7. Report the result, performance and any limitations.
8. Offer an optional external provider if local inference is unsuitable or unavailable.

No model should be downloaded without user consent.

## 10.3 Ollama installation and management

The Windows installer/app should:

- Detect an existing Ollama installation.
- Offer to install Ollama if it is missing.
- Explain what will be installed and request consent.
- Start and manage the local Ollama service where supported.
- Detect service failures and explain them.
- Download models separately from the ATLAS installer.
- Avoid bundling very large model files into the application installer.

Equivalent platform-specific handling should be designed for Linux and macOS.

## 10.4 External AI providers

External providers, for example Gemini, may be configured optionally.

- Provider selection is user-controlled.
- API keys are stored in the local encrypted Secret Vault.
- ATLAS does not store API keys on its own servers.
- Requests still travel to the selected provider when cloud inference is used.
- ATLAS must disclose which provider receives the request.
- Users should be able to choose what project context is sent.
- A local-only mode must disable external AI requests.

---

# 11. Hardware Profiler & Compatibility Engine

This is a key differentiator: model recommendations should be based on the actual computer, not only a simple RAM tier.

## 11.1 Hardware inspection

| Component | Information to inspect |
| --- | --- |
| CPU | Model, vendor, architecture, cores, threads, clock information and instruction sets |
| GPU | Vendor, model, architecture, compute support and acceleration backend |
| Dedicated VRAM | Physical dedicated GPU memory |
| Shared memory | System memory shared with integrated graphics, shown separately |
| RAM | Total, available and currently usable memory |
| Storage | Available space and drive information where supported |
| OS | Platform, version and architecture |
| Drivers | GPU driver versions and supported compute backends |
| Power | Battery or plugged-in state where available |
| Thermals | Temperature and thermal status where platform access allows |

Support Intel, AMD, NVIDIA and Apple Silicon where applicable. Do not assume NVIDIA hardware.

Hardware information should remain local unless the user explicitly chooses to share a diagnostic report.

## 11.2 Compatibility inputs

The evaluation should consider:

- Model architecture.
- Parameter count.
- Tensor sizes.
- Quantisation.
- Context length.
- KV cache requirements.
- Batch size.
- Compute buffers.
- GPU offloading.
- Runtime overhead.
- CPU architecture and instruction support.
- GPU backend and driver support.
- Dedicated VRAM versus shared memory.
- Currently available system memory.
- Available disk space.

Compatibility must be recalculated when the user changes quantisation, context length, GPU offload, batch size or other relevant runtime settings.

## 11.3 Requirements versus detected resources

Keep these concepts separate:

1. **Minimum requirements** — the estimated minimum needed to attempt a configuration.
2. **Recommended requirements** — resources likely to provide a more usable experience.
3. **Detected hardware** — installed hardware and its capabilities.
4. **Currently available resources** — resources available at the time of evaluation.

A computer may meet minimum requirements but still deliver poor performance.

## 11.4 Model evaluation status

- **Recommended** — the configuration appears suitable.
- **Possible but slow** — it may work with significant performance limitations.
- **Not recommended** — important requirements are not met.
- **Unsupported** — required architecture, format or runtime support is unavailable.

## 11.5 Confidence levels

- **High:** metadata and runtime estimates agree and important information is available.
- **Medium:** some requirements rely on estimates.
- **Low:** important metadata is missing, inconsistent or unsupported.

ATLAS must never present estimates as exact facts.

## 11.6 GGUF inspection and memory estimation

GGUF metadata can provide architecture information, dimensions, layer counts, attention configuration, context-related metadata, tensor information and quantisation details. It does not generally provide a complete authoritative minimum hardware specification.

The proposed evaluation process:

1. Inspect GGUF metadata and tensor information without loading the full model where possible.
2. Estimate weight memory from tensor sizes and quantisation.
3. Estimate KV cache memory using architecture, context length and runtime settings.
4. Account for compute buffers and runtime overhead.
5. Estimate memory placement based on GPU offloading.
6. Use runtime estimates where available.
7. Run a controlled loading and inference test only after the compatibility check.
8. Monitor resources and stop tests if resource use becomes unsafe.

Filenames and marketing descriptions must not be treated as reliable hardware specifications.

## 11.7 Optional benchmarking

- Model loading time.
- Tokens per second.
- CPU inference speed.
- GPU acceleration availability.
- Memory consumption.
- GPU and CPU utilisation.

Benchmarks should be optional, explain what they will do, avoid unnecessary stress and stop if resource use becomes unsafe.

## 11.8 Manual incompatible-model warning

When a user selects an incompatible model, show the specific detected issues.

Example layout:

| Requirement | Model configuration | Computer |
| --- | --- | --- |
| RAM | Calculated requirement | Detected total and available RAM |
| CPU | Required architecture and instructions | Detected CPU capabilities |
| GPU | Required backend and support | Detected GPU and backend |
| VRAM | Estimated dedicated VRAM need | Available dedicated VRAM |
| Storage | Required disk space | Available disk space |

The displayed values must be calculated from actual metadata and hardware inspection. Do not use fabricated numbers in real compatibility reports.

### Continue-anyway behaviour

For configurations where continuing is allowed:

- Explain each compatibility issue.
- Distinguish minimum and recommended requirements.
- Require a five-second reading period before enabling Continue.
- Do not skip the timer.
- Do not automatically continue when the timer expires.
- Require the user to click Continue.

The five-second period is an acknowledgement mechanism, not a technical safety guarantee.

Some conditions should block continuation until resolved:

- Unsupported model format or runtime with no compatible option.
- Insufficient disk space to complete a download or installation.
- Other conditions where the operation cannot safely or correctly proceed.

---

# 12. System Monitor

A live view of the computer and development processes.

## 12.1 Metrics

- CPU usage.
- GPU usage.
- RAM usage.
- Dedicated VRAM and shared memory.
- Storage usage.
- Network activity.
- Running processes.
- Development server status.
- Selected process resource usage.
- Background service status.

## 12.2 Behaviour

- Allow users to choose which metrics are visible.
- Avoid expensive polling when the screen is not active.
- Show when data was last updated.
- Handle unavailable metrics gracefully.
- Do not imply that a metric is exact when the OS exposes only an estimate.
- Do not terminate processes without explicit user action and confirmation where appropriate.

---

# 13. Git Centre

A central view of local repositories. It should complement, not replace, specialist Git applications.

## 13.1 Repository discovery

- Discover repositories in user-selected directories.
- Register repositories manually.
- Show repository paths and remotes.
- Detect repository status.
- Identify detached HEAD or other unusual states.

## 13.2 Repository features

- Working tree status.
- Changed files.
- Diff inspection.
- Commit history.
- Branch list.
- Branch switching.
- Remote information.
- Staged and unstaged changes.
- Open repository in an external Git client.
- Open a terminal at the repository root.
- Quick access to repository settings.

## 13.3 Safety

- Clearly distinguish read-only inspection from mutations.
- Confirm potentially destructive operations.
- Never silently discard changes.
- Do not force-push or rewrite history without explicit user intent and confirmation.
- Explain conflicts and failures.
- Local Git features should work without a GitHub account.

## 13.4 Optional hosting integrations

GitHub or other hosting integrations may be added later. They must be optional and should use narrowly scoped permissions. Local Git functionality must not depend on a hosting provider.

---

# 14. Workflow Automation

Workflows automate repeatable development setup and routine actions.

## 14.1 Example: Start a Flask project

A user-defined workflow might:

1. Open the project folder.
2. Launch the selected IDE.
3. Open a terminal at the project root.
4. Activate an existing virtual environment.
5. Start Docker if the project requires it.
6. Start the development server after approval.
7. Open the local website in a browser.

## 14.2 Workflow capabilities

- Reusable workflows.
- Project-specific workflows.
- Manual triggers.
- Optional startup triggers.
- Sequential actions.
- Conditions.
- Delays.
- Error handling.
- Workflow history.
- Notifications.
- User approval checkpoints.
- Enable, disable and duplicate workflows.

## 14.3 Workflow safety

- Display the actions a workflow will perform.
- Require approval for sensitive commands.
- Do not hide shell commands from the user.
- Do not execute arbitrary project scripts merely because they exist.
- Provide a stop/cancel mechanism where possible.
- Record outcomes without logging secrets.
- Treat project files and scripts as untrusted input until reviewed.

A workflow should not gain broader permissions simply because it is saved or reused.

---

# 15. Developer Productivity Tools

Smaller tools can make ATLAS useful throughout the day.

| Feature | Purpose |
| --- | --- |
| Universal Search | Search projects, applications, tools, notes and settings |
| Command Palette | Keyboard-first access to ATLAS actions |
| Developer Clipboard | Store reusable snippets and commands locally |
| Snippet Manager | Organise code snippets and templates |
| Environment Manager | View and manage language environments and versions |
| Port Manager | Identify local listeners and port usage |
| Notes | Store project and general development notes |
| Task Tracker | Track tasks and TODOs |
| Session Manager | Save and restore groups of applications and workspace settings |
| Notification Centre | Show actionable development alerts |
| Documentation Shortcuts | Open project documentation and useful references |

These should be introduced when they can be implemented reliably. A large number of half-finished utilities would make ATLAS less useful, not more.

---

# 16. Secret Vault & Security

The Secret Vault protects sensitive values such as API keys, access tokens, credentials and other user-managed secrets.

## 16.1 Local encryption

- Encrypt secret values at rest using **AES-256-GCM**.
- Use authenticated encryption so modifications to encrypted data can be detected.
- Generate cryptographically secure nonces correctly; never reuse a nonce with the same key.
- Protect encryption keys using the operating system's secure credential storage where supported.
- Do not hardcode encryption keys in application code.
- Do not store encryption keys beside encrypted vault data in plaintext.
- Plan for secure key rotation and recovery.
- Explain recovery limitations before users rely on the vault.

AES-256-GCM is the selected design direction, not a claim that the vault has already been implemented or independently audited.

## 16.2 Authentication

**Default: operating-system authentication.**

Use platform-supported authentication such as:

- Windows Hello / Windows-protected credential facilities.
- macOS Keychain and Touch ID where available.
- Linux Secret Service or an appropriate desktop credential facility.

Optional additional methods:

- Passkey authentication where platform support permits.
- TOTP through a compatible authenticator app.

Passkey and TOTP should be optional, not mandatory. Do not force repeated authentication prompts during ordinary use.

## 16.3 Vault behaviour

- Secrets are masked by default.
- Revealing a secret requires deliberate user action.
- Editing and deleting secrets require appropriate authentication.
- Auto-lock after configurable inactivity.
- Lock immediately on user request.
- Keep secret values out of logs, crash reports and analytics.
- Avoid copying secrets to the clipboard by default.
- If copying is supported, warn the user and clear the clipboard after a configurable period where the platform allows.
- Record local audit events for secret creation, editing, reveal and deletion without recording secret values.

## 16.4 Secret organisation

Potential organisation:

- Provider name.
- Secret name.
- Project association.
- Creation and modification dates.
- Optional expiry reminder.
- User-written description.
- Tags.

Examples include API keys for AI providers, Git hosting tokens and development service credentials.

## 16.5 Secret handling outside the Vault

The Vault is only one layer. ATLAS must also:

- Redact known secrets from AI context.
- Avoid printing secret values in terminal logs.
- Avoid placing secrets in command-line arguments when safer alternatives exist.
- Avoid storing secrets in project configuration files automatically.
- Protect environment variables and temporary files where possible.
- Avoid including secrets in diagnostic exports.
- Treat extension access to secrets as privileged.
- Never send secrets to ATLAS servers.

Redaction cannot guarantee detection of every secret. Users must be able to review what will be shared externally.

---

# 17. Privacy, networking & offline operation

## 17.1 No ATLAS cloud dependency

ATLAS should not require an ATLAS-hosted account, database or cloud backend for core functionality.

Local projects, notes, settings, model configuration and secrets remain on the user's device by default.

## 17.2 Network access by purpose

Some optional features naturally require network access:

- Downloading developer tools.
- Installing packages.
- Fetching model catalogue information.
- Downloading AI models.
- Updating ATLAS.
- Connecting to Git hosting services.
- Using an external AI provider.

For each feature, ATLAS should explain the external service involved and the data required.

## 17.3 Local-only mode

A strict local-only mode should:

- Disable external AI providers.
- Disable optional hosting integrations.
- Prevent ATLAS-initiated network requests for optional features.
- Keep local project and vault functionality available.
- Clearly explain that tool, package and model downloads will be unavailable while the mode is active.

Operating-system services and applications launched by the user may still make their own network connections; ATLAS should not claim to control every process on the computer.

## 17.4 External AI disclosure

When cloud AI is enabled:

- Identify the provider.
- Explain that prompts and selected context leave the computer.
- Show what files or context are included.
- Allow the user to cancel.
- Redact known secrets before sending.
- Do not imply that local API-key storage makes the AI request itself local.

---

# 18. Permissions & action safety

ATLAS can launch applications, install tools, run commands and modify project files. These capabilities require clear permission boundaries.

## 18.1 Action categories

| Category | Example | Expected handling |
| --- | --- | --- |
| Read-only | Inspect project files | Follow configured project access |
| Application launch | Open an IDE | User-configured launch action |
| Project modification | Edit source files | Explicit task intent and visible changes |
| Shell execution | Run a build or test | Show command and request approval according to policy |
| Installation | Install Python or Docker | Explicit consent for each installation |
| Destructive action | Delete files or discard Git changes | Strong confirmation |
| External transmission | Send project context to cloud AI | Clear disclosure and user control |
| Secret access | Reveal or use an API key | Vault and OS security policy |

## 18.2 General safeguards

- Least-privilege access.
- No silent installations.
- No hidden command execution.
- No automatic destructive changes.
- Clear action previews.
- Cancellation where possible.
- Visible execution status.
- Useful error reporting.
- Secret redaction.
- Audit history for important actions.

---

# 19. Cross-platform support

ATLAS is intended to be a cross-platform desktop application.

## 19.1 Windows

Target distribution:

- `.exe` installer.

Considerations:

- Windows application discovery.
- Windows Credential Manager / DPAPI.
- Windows Hello where supported.
- PowerShell and Windows Terminal integration.
- WSL distribution detection and launch.
- Docker Desktop integration.
- Installer elevation and per-user installation options.

## 19.2 Linux

Target distributions:

- AppImage.
- `.deb` package.

Considerations:

- Desktop application discovery.
- Desktop environment differences.
- Secret Service integration where available.
- Shell and terminal detection.
- Package manager differences.
- Distribution-specific dependencies.
- Wayland/X11 differences where relevant.

## 19.3 macOS

Target distribution:

- `.dmg`.

Considerations:

- Application discovery.
- Keychain integration.
- Touch ID where supported.
- Apple Silicon and Intel compatibility as appropriate.
- Code signing and notarisation.
- macOS permissions and sandbox behaviour.

The developer may not have access to every target operating system locally. macOS builds may therefore require macOS CI, and release readiness must distinguish compilation from actual platform testing.

## 19.4 Platform parity

Core product concepts should remain consistent, but exact integrations may differ. ATLAS must show unavailable platform features clearly rather than pretending they work identically everywhere.

---

# 20. Proposed technical architecture

The stack below is a starting proposal and should be validated with a small technical prototype before being treated as final.

## 20.1 Proposed stack

| Layer | Proposed technology | Responsibility |
| --- | --- | --- |
| Desktop shell | Tauri 2 | Native desktop application and platform integration |
| Frontend | React + TypeScript | UI and application state |
| Styling | Tailwind CSS or a consistent component system | Visual design |
| Local database | SQLite | Projects, settings, notes and structured local data |
| Secure storage | OS credential facilities + encrypted vault | Encryption-key protection and secret storage |
| AI integration | Provider adapters | Local and optional external AI |
| Local inference | Ollama initially; compatible runtimes as needed | Run local models |
| Git integration | Git CLI/library integration | Local repository operations |
| System inspection | Platform-specific adapters | Hardware and process information |
| Workflow engine | Explicit action registry | Controlled automation |

A separate Python service may be considered if it provides a clear benefit for AI orchestration or developer-tool integrations. It should not be introduced merely to add another moving part.

## 20.2 Architectural boundaries

Keep the application modular:

- UI and presentation.
- Project discovery and project management.
- Application launcher.
- Tool catalogue and installer adapters.
- AI provider abstraction.
- Model compatibility engine.
- Hardware inspection adapters.
- Git integration.
- Workflow execution.
- Secret Vault.
- Local persistence.
- Platform-specific integration.

Sensitive operations should go through narrow, auditable interfaces. The UI should not have unrestricted access to arbitrary shell execution or raw secret storage.

## 20.3 Provider abstraction

AI providers should implement a common interface where practical. The rest of ATLAS should not depend directly on one provider's API.

The same principle applies to tool installers, system metrics and platform-specific integrations.

---

# 21. Data storage

## 21.1 Local data

Potential local data includes:

- Application preferences.
- Dashboard layouts.
- Project registrations.
- Project metadata.
- Project notes and context.
- Launcher entries.
- Tool detection results.
- Workflow definitions.
- Workflow history.
- AI conversation history, according to user settings.
- Model configuration.
- Hardware scan results.
- Git repository registrations.
- Secret Vault encrypted records.

## 21.2 Storage rules

- Store structured application data locally, for example in SQLite.
- Store secrets separately from ordinary application settings.
- Encrypt sensitive records.
- Avoid duplicating secrets into project metadata.
- Provide export and backup options.
- Explain which data is included in backups.
- Make deletion behaviour clear.
- Avoid collecting more data than a feature needs.

## 21.3 Backup and recovery

- User-controlled local backups.
- Encrypted Vault backups.
- Clear recovery instructions.
- Versioned data migrations.
- Restore previews where possible.
- Warn users if a backup cannot restore a protected secret because its key material is unavailable.

Do not promise recoverability if the required encryption key has been lost.

---

# 22. UX, accessibility & customisation

## 22.1 Visual direction

- Dark theme as the initial default.
- Clean, modern developer-focused interface.
- Clear visual hierarchy.
- Consistent spacing and typography.
- Restrained use of accent colours.
- Useful empty states.
- Clear loading and error states.
- Avoid unnecessary decorative panels.

## 22.2 Keyboard-first interaction

- Global search shortcut.
- Command Palette.
- Keyboard navigation.
- Searchable lists.
- Configurable shortcuts.
- Focus indicators.
- Predictable Escape and Enter behaviour.

## 22.3 Accessibility

- Scalable text.
- Screen-reader labels.
- Sufficient contrast.
- Keyboard accessibility.
- Reduced-motion option.
- Clear status messages that do not rely on colour alone.

## 22.4 Personalisation

- Themes and accent colours.
- Dashboard layout.
- Pinned tools.
- Custom project categories.
- Custom launch profiles.
- Keyboard shortcuts.
- Configurable notifications.
- Preferred terminal and editor.

---

# 23. Reliability, diagnostics & updates

## 23.1 Reliability

- Recover gracefully from a failed tool scan.
- Do not lose project registrations if an application disappears.
- Handle unavailable integrations without crashing the whole application.
- Protect local data during upgrades.
- Provide useful errors and recovery steps.
- Avoid blocking the UI during long-running tasks.

## 23.2 Diagnostics

- Local diagnostic logs.
- Secret redaction.
- User-controlled diagnostic export.
- No automatic upload of project files.
- Clear explanation before any diagnostic report is shared externally.

## 23.3 Updates

- Check for updates according to user settings.
- Verify update authenticity and integrity.
- Explain release notes.
- Support cancellation where possible.
- Avoid replacing user data during upgrades.
- Provide recovery guidance if an update fails.

---

# 24. Extension system

An extension system could allow developers to add integrations and custom capabilities.

Potential extensions:

- Additional IDE integrations.
- Additional AI providers.
- Additional tool installers.
- Custom dashboard widgets.
- Workflow actions.
- Language and framework support.
- Hosting-provider integrations.

Security requirements:

- Extensions should have declared permissions.
- Users should approve privileged access.
- Extensions should not automatically access Vault secrets.
- Extension code should be isolated where practical.
- Untrusted extensions should not receive unrestricted shell access.
- Provide extension disable and removal controls.
- Explain extension origin and update source.

The extension system should come after the core permission model is reliable. It should not be rushed into the first release.

---

# 25. Non-goals and boundaries

ATLAS should remain focused.

It is not intended to:

- Replace every IDE or code editor.
- Replace every terminal.
- Become a full operating system.
- Require a cloud account for basic use.
- Silently install software.
- Run arbitrary commands without appropriate permission.
- Automatically upload project contents.
- Force users to use one AI provider.
- Force users to use local AI if their hardware is unsuitable.
- Force users to use cloud AI.
- Become a general-purpose project-management platform with excessive unrelated features.

The guiding question for every feature should be:

**Does this make ATLAS a more useful development command centre?**

If not, it probably does not belong in the product.

---

# 26. Suggested delivery roadmap

This is a proposed sequence, not a promise of release dates.

## Phase 0 — Technical foundation

- Validate Tauri and frontend architecture.
- Test Windows, Linux and macOS build paths.
- Establish local database and migration strategy.
- Establish platform integration boundaries.
- Prototype secure local storage.
- Define permissions and action execution interfaces.
- Create design system and navigation shell.

## Phase 1 — Useful daily workspace

- Application shell and navigation.
- Developer Home.
- Project registration and recent projects.
- Universal App Launcher.
- Application favourites and launch profiles.
- Local settings.
- Basic command palette.

**Goal:** ATLAS is already useful as a daily launcher and project starting point.

## Phase 2 — Developer tools

- Tool detection.
- Version reporting.
- Project type detection.
- Tool recommendations.
- Consent-based installation flow.
- Installation progress and verification.
- Project-specific tool profiles.

**Goal:** ATLAS helps developers understand and prepare their development environment.

## Phase 3 — System and Git

- Hardware Profiler.
- System Monitor.
- Local Git Centre.
- Port Manager.
- Development process visibility.

**Goal:** ATLAS becomes a useful overview of the computer and active development work.

## Phase 4 — AI and models

- AI Workspace.
- Helper, Developer and Hybrid modes.
- Ollama detection and optional installation.
- Model catalogue and manual model selection.
- Hardware-aware compatibility evaluation.
- Local inference testing.
- Optional external provider adapters.
- Context selection and secret redaction.

**Goal:** AI becomes a useful integrated layer rather than the only feature.

## Phase 5 — Vault and workflows

- Encrypted Secret Vault.
- OS authentication.
- Optional passkey/TOTP support.
- Auto-lock.
- Workflow engine.
- Approval checkpoints.
- Project workspace sessions.

**Goal:** Add secure credential handling and meaningful automation.

## Phase 6 — Polish and extensibility

- Notes and snippets.
- Notifications.
- Advanced dashboard customisation.
- Extension system.
- Additional integrations.
- Cross-platform release validation.
- Accessibility and performance improvements.

**Goal:** Make ATLAS dependable enough to become a developer's everyday starting point.

---

# 27. Quality and acceptance criteria

A feature is not complete merely because its UI exists.

## 27.1 General criteria

- Works on its declared supported platforms.
- Handles errors and missing dependencies.
- Does not silently perform sensitive actions.
- Preserves user data.
- Provides clear feedback.
- Has appropriate tests.
- Documents known limitations.

## 27.2 Project Hub

- Can register and reopen a project.
- Does not delete project files when removing a registration.
- Shows correct project paths.
- Handles inaccessible or moved directories.
- Lets users inspect and remove stored project context.

## 27.3 Tool Manager

- Detects existing installations before proposing a download.
- Shows the exact proposed tool and version.
- Requests consent before every installation.
- Handles denial and cancellation correctly.
- Verifies the result.
- Does not overwrite existing versions without permission.

## 27.4 AI Workspace

- Correctly enforces the three working modes.
- Helper cannot execute or modify project files.
- Developer and Hybrid actions follow permission policy.
- Mode changes are visible.
- External context sharing is disclosed.
- Known secrets are redacted before AI requests.

## 27.5 Model compatibility

- Reads available metadata rather than trusting filenames.
- Distinguishes dedicated VRAM from shared memory.
- Recalculates when configuration changes.
- Labels estimates and confidence.
- Does not invent hardware requirements.
- Stops unsafe benchmarks.
- Does not download without consent.

## 27.6 Secret Vault

- Secret values are encrypted at rest.
- Encryption keys are not hardcoded or stored beside ciphertext in plaintext.
- Authentication works through supported OS facilities.
- Secrets are masked by default.
- Secret values do not appear in logs or diagnostic exports.
- Auto-lock works.
- Backup and recovery limitations are explained.
- Security claims are tested and independently reviewed before being advertised as production-grade.

## 27.7 Workflows

- Actions are visible before execution.
- Sensitive actions require approval.
- Errors are reported.
- Cancellation is supported where possible.
- No workflow silently gains unrestricted permissions.

---

# 28. Open product decisions

The following decisions remain open and should be resolved before implementation reaches the relevant feature.

1. **Product name:** ATLAS is the current working name; name availability and branding have not been finalised.
2. **First supported platform:** Windows is the most practical initial development target, with Linux and macOS considered in architecture.
3. **Dashboard layout:** determine the default widgets and customisation model.
4. **Project scanning:** decide how users select directories and how often discovery runs.
5. **Tool catalogue:** choose the first supported tools and trusted installation sources.
6. **Denial memory:** decide whether denied installation requests are remembered per project, globally or both.
7. **AI provider list:** choose the first local and optional external providers.
8. **Model runtime support:** decide whether to start with Ollama only or add another runtime early.
9. **AI conversation storage:** decide retention, export and deletion defaults.
10. **Vault recovery:** design recovery carefully so convenience does not undermine encryption.
11. **Passkeys and TOTP:** confirm platform support and the exact optional authentication flows.
12. **Workflow triggers:** decide which automatic triggers are supported in the first version.
13. **Extension permissions:** define a permission model before third-party extensions are allowed.
14. **Update delivery:** choose platform-specific update mechanisms and signing requirements.

These are not reasons to delay the initial workspace prototype. Many can be decided as the relevant phases approach.

---

# 29. Glossary

| Term | Meaning |
| --- | --- |
| **ATLAS** | The proposed developer command centre |
| **Project Hub** | ATLAS's project discovery and management area |
| **Tool Manager** | The area for detecting, recommending and installing developer tools |
| **AI Workspace** | The integrated assistant with Helper, Developer and Hybrid modes |
| **Model Manager** | The area for configuring local models and optional AI providers |
| **Hardware Profiler** | The component that inspects computer capabilities |
| **Compatibility Engine** | The component that estimates whether a model configuration is suitable |
| **Secret Vault** | Local encrypted storage for credentials and sensitive values |
| **Local-only mode** | A mode that disables ATLAS-initiated optional external network requests |
| **Workflow** | A user-configured sequence of development actions |

---

## Final product statement

ATLAS is a local-first development command centre designed to become the first application developers open every day.

It brings projects, applications, developer tools, system monitoring, Git, workflows, secure local secrets and AI-assisted development into one coherent desktop workspace.

It should make development environments easier to understand, projects easier to open, repetitive work easier to automate and powerful tools easier to manage — without taking control away from the developer.

**ATLAS should feel like the home base for development, not another tool developers have to manage.**


---

# 30. AI handoff document & release plan

**Last updated:** 2026-11-03

## 30.1 Purpose of this document

This file is the **provider-independent master specification and handoff document for ATLAS**. It is maintained so that the project can be continued with different AI assistants, model providers and development environments.

It is not the README for the eventual ATLAS application/source-code repository, and the existence of a feature in this document does not mean that the feature has been implemented.

The document should make it possible for another assistant or coding agent to understand:

- The complete ATLAS product vision.
- Features and architecture already planned.
- Decisions and constraints that must be preserved.
- The current release plan.
- What is implemented, tested, deferred or still undecided.

The specification should remain usable if development moves between hosted AI providers, Ollama, Goose or other compatible tools. Avoid provider-specific assumptions in the product architecture unless a feature explicitly requires them.

## 30.2 Product release naming and progression

The current release plan has two main milestones:

### ATLAS 0.1 — Core

ATLAS 0.1 Core is the first functional foundation of the product. It is deliberately smaller than the complete vision in this specification.

The initial target is a focused milestone of approximately **40 eligible development hours**, subject to the rules of the program or event under which the work is tracked.

Proposed Core scope:

- **Developer Home:** a useful starting dashboard with recent projects and quick actions.
- **Project Hub:** register, inspect, organise and open projects.
- **Universal App Launcher:** detect and launch installed developer applications.
- **AI Workspace:** the Helper, Developer and Hybrid modes.
- **ATLAS Action Protocol (AAP):** a model-independent structured action format for safe, validated AI requests.
- **Safe execution foundation:** controlled file operations and approved command execution.
- **Basic Tool Detection:** identify selected installed developer tools and report their versions.
- **First-run tutorial:** provide interactive onboarding that can be reopened from Settings → Help & Onboarding.
- **Project Templates:** create projects from built-in or user-created templates, with preview and configuration.
- **Project Doctor:** diagnose common project configuration, dependency, tool-version and Git issues.
- **Project Quick Actions:** expose configurable, project-aware actions such as opening a terminal, editor or project-specific development task.
- **Workspace Snapshots:** save and restore selected applications, projects, launch profiles and workspace layout.
- **Activity Timeline:** provide a user-visible history of important ATLAS activity, separate from the security audit log.
- **Git agent permission controls:** provide a user-controlled setting for whether agents may initiate repository pushes, enforced outside the AI model.
- **Testing and packaging:** make the implemented Core features usable and verify their behaviour.

Core should prioritise complete, working workflows over a large number of unfinished screens. Features from the full vision that are not in this scope remain planned, not implemented.

### ATLAS Pro — expanded product

ATLAS Pro is the planned larger summer milestone, building on the Core foundation and moving substantially closer to the full ATLAS vision.

Potential Pro work includes:

- Advanced AI agent capabilities and expanded AAP actions.
- Full Developer Tool Manager, including consent-based discovery and installation.
- Hardware Profiler and model Compatibility Engine.
- Local and cloud AI provider/model management.
- Git Centre.
- Workflow Automation.
- Encrypted Secret Vault and platform authentication.
- System Monitor.
- Expanded project intelligence and productivity utilities.
- Remote Development Manager for SSH, WSL and supported remote development environments.
- Environment Profiles for project-specific development, testing and production-like configurations.
- AI Project Memory with inspectable, editable and refreshable project knowledge.
- Build & Test Centre for unified builds, test runs, logs and result comparisons.
- Dependency Security Centre for vulnerability, version and licence analysis.
- Architecture Visualizer for project modules and dependency relationships.
- Visual Workflow Builder for composing triggers, actions, conditions and approval checkpoints.
- AI Task Delegation for splitting work across providers or agents with conflict controls.
- A permission-controlled extension ecosystem.
- Cross-platform improvements, reliability, testing and packaging.

The exact Pro scope must be prioritised against the event's duration, rules, available time and the stability of Core. The complete product vision remains larger than any single event milestone.

**Naming direction:** use **ATLAS 0.1 Core** for the first functional foundation and **ATLAS Pro** for the expanded summer milestone. The long-term product may simply be called **ATLAS**; “Pro” is a milestone/release label unless a permanent edition structure is deliberately adopted later.

## 30.3 Existing work and event time tracking

The Core specification, product planning and architecture documented before a future event are prior work. They must be described transparently.

Whether an event permits continuing an existing project, reusing designs or counting particular categories of work is determined only by that event's published rules.

Do not count pre-event work as event hours unless the event explicitly allows it. Track eligible work according to the event's own rules, and distinguish prior planning from new implementation, testing and documentation.

If an event requires a new project or restricts reuse, follow its rules. Earlier specifications may only be used as a reference if that is permitted; renaming or recreating a project does not by itself make prior work new.

## 30.4 Implementation status conventions

Every future handoff or progress update should distinguish these states:

- **PLANNED** — specified or discussed, but implementation has not started.
- **IN_PROGRESS** — implementation is actively underway.
- **IMPLEMENTED** — code or functionality exists.
- **TESTED** — the stated behaviour has been verified by an identified test.
- **DEFERRED** — intentionally postponed to a later milestone.
- **BLOCKED** — cannot proceed until a dependency or decision is resolved.

A feature must not be labelled TESTED merely because code was written or a build succeeded. Record the scope of testing and any limitations.

## 30.5 AAP security invariant

The AI may request an action using AAP, but it must never decide whether that action requires approval.

AI-generated action requests must not contain authoritative permission decisions such as `requires_approval`, `approved`, `trusted` or equivalent fields. ATLAS's own Permission Manager independently evaluates every request and determines whether approval is required.

The AI cannot grant itself permissions, approve its own actions, bypass policy or modify ATLAS security settings. This rule applies to every AI provider and every AI working mode.

## 30.6 Source-of-truth and repository separation

- This master specification is the provider-independent source of truth for product intent, planned architecture and recorded decisions.
- The eventual ATLAS application repository will contain the actual source code, build configuration, tests and implementation documentation.
- Implementation status in this document must be kept consistent with the actual codebase and verified test results.
- When implementation differs from the specification, record the difference instead of silently assuming either one is correct.
- When handing the project to another AI or coding agent, provide this document together with the actual application repository and a concise current-status handoff.



---

# 31. Hack Club Context, Event Goals & Rewards

**Last reviewed:** 2026-11-03  
**Status:** Personal planning context. Future event details are unconfirmed until organisers publish their rules.

This section records why ATLAS is being developed with Hack Club opportunities in mind. It is context for future AI assistants, not a product requirement and not a guarantee of event eligibility or rewards.

## 31.1 Programme context

The user is interested in Hack Club programmes, including YSWS opportunities and summer build programmes. Programmes previously considered include Axiom, Summer of Making and Stardance. Their future availability, names, dates, eligibility and rules must not be assumed. Check current official announcements and rules before making claims.

ATLAS should remain a worthwhile, functional product independently of any event. Event constraints may shape the milestone and schedule, but must not encourage superficial features or dishonest reporting.

## 31.2 Milestone plan

- **ATLAS 0.1 — Core:** the earlier functional foundation, with an approximate 40-hour project budget. This is our planning estimate, not an official event threshold.
- **ATLAS Pro:** the larger planned summer milestone, building on Core and implementing a substantial set of advanced capabilities.
- **ATLAS:** the long-term product beyond any single event.

If a programme allows existing-project continuation, disclose the earlier Core work and clearly identify new Pro work. If it restricts existing projects, prior designs or reused code, follow the exact rules and ask organisers for clarification. Renaming a project or creating a new repository does not make old work new.

## 31.3 Time tracking and eligible work

- Use the tracker and process required by the specific event. Do not assume WakaTime or Hackatime is accepted until the rules say so.
- The user has practised with WakaTime and intends to configure Hackatime when appropriate; this does not establish that a future programme accepts either tracker.
- Do not count pre-event work unless the programme explicitly permits it.
- Keep prior planning, specification, architecture and implementation separate from work performed during the event.
- Track genuine work accurately. Never fabricate, inflate, backdate or double-count hours.
- Do not assume planning, learning, documentation, debugging, testing or passive time is eligible; check the programme's definitions.
- Keep a concise work log describing the work and its outcome.
- The Core 40-hour estimate is not an Axiom or summer-event requirement unless that event independently publishes the same threshold.

## 31.4 Existing work and disclosure

The master specification is prior planning and a provider-independent handoff document. For event submissions, explain which concepts, designs, code and documentation existed beforehand and which work was completed during the eligible period. Do not misrepresent project history or claim previous work as new. If rules are ambiguous, ask organisers before relying on prior work.

## 31.5 Hardware reward preferences

The user's current aspirational preference order is:

1. MacBook Air M5 with 24 GB RAM, if offered.
2. MacBook Air M5 with 16 GB RAM, if offered.
3. Raspberry Pi 500+ Desktop Kit.
4. Raspberry Pi 500+ Base Edition.
5. MacBook Neo.
6. Raspberry Pi 500 Desktop Kit.
7. Raspberry Pi 500 Base Edition.
8. iPad Air.

This is a preference list, not a claim that these products are offered, available or attainable in any particular event. Recheck the actual reward catalogue, device configurations, thresholds and regional shipping rules. The user is open to earning both a Mac and a Raspberry Pi in one event if its reward structure permits it; do not assume rewards are mutually exclusive or stackable.

## 31.6 How rewards should affect project planning

Rewards are motivation, not a substitute for building a genuine product.

- Prioritise a coherent, working ATLAS Pro over shallow feature-count inflation.
- Do not add needless complexity just to consume tracked hours.
- Never invent features, commits, tests, progress or time.
- Do not promise that a project or hour total will earn a particular device.
- Verify reward thresholds and conditions against the current programme rules.
- Keep the roadmap worthwhile even if an event changes or offers different rewards.

## 31.7 Verification checklist for each future event

Before committing to a programme, verify from current official sources:

1. Event dates and eligible work period.
2. Age, location, student and account eligibility.
3. Whether desktop applications and developer tools are accepted.
4. Existing-project, continuation, prior-design and code-reuse rules.
5. AI-assistance rules and required disclosure.
6. Required time tracker and exactly which activities count.
7. Hour thresholds, if any.
8. Submission, repository and demonstration requirements.
9. Reward catalogue, configurations, thresholds and shipping conditions.
10. Whether multiple rewards can be earned in one event.
11. Whether rewards are guaranteed or subject to review, stock or organiser approval.

Mark unclear details **UNCONFIRMED** and ask organisers. Never apply an older event's rules to a new edition without checking.

## 31.8 Instructions for future AI assistants

Keep product engineering advice separate from event eligibility advice. Verify current rules before making definitive claims about hours, prior work or rewards. Label historical information, confirmed current rules and speculation distinctly. Help maintain an honest work log, scope ATLAS Pro to the actual event duration, preserve the user's stated hardware preferences and never guarantee a reward. Official rules and direct organiser clarifications take precedence over AI interpretations.

---

# 32. Additional Core & Pro Feature Decisions

**Last updated:** 2026-11-03  
**Status:** Accepted feature direction; detailed implementation scope and prioritisation remain subject to release planning.

This section records additional product capabilities accepted for consideration in the ATLAS roadmap. Listing a feature here means it is part of the planned product direction; it does not mean it has been implemented or that every item must fit into the first Core or Pro milestone.

## 32.1 ATLAS Core additions

### A. First-run interactive tutorial

ATLAS should provide an interactive onboarding tutorial on first launch. It should introduce the application progressively and help users understand the main workspace.

The tutorial should cover:

- ATLAS's purpose and main navigation.
- Developer Home and dashboard basics.
- Registering, opening and organising projects.
- The Universal App Launcher.
- AI providers and Helper, Developer and Hybrid modes.
- AAP, the Permission Manager and the difference between an AI request and an authorised action.
- File changes, command execution and approval prompts.
- Basic settings and workspace customisation.

Requirements:

- Users may skip the tutorial or individual sections.
- Tutorial progress should be saved so users can resume later.
- The complete tutorial must remain accessible after onboarding from **Settings → Help & Onboarding → Start Tutorial**.
- Tutorial content should be updated when major UI or security workflows change.
- Tutorial examples must not execute real commands, modify files or change settings without a separate user action.
- The tutorial should explain security decisions accurately and must not encourage users to disable protections merely to make a demonstration work.

### B. Project Templates

Provide a Project Templates area for creating projects from reusable starting points.

Initial built-in examples may include:

- Flask application.
- React and TypeScript application.
- Python CLI application.
- Basic HTML, CSS and JavaScript project.
- Docker Compose starter.

Capabilities:

- Preview a template's description, structure, included files and requirements before creation.
- Configure the project name and destination.
- Detect required tools and runtimes before creation.
- Allow optional Git repository initialisation.
- Report generated files and any setup steps that were not completed.
- Support user-created templates from existing projects or explicitly selected directories.
- Let users edit, duplicate, export and remove custom templates.
- Keep template metadata and versions clear.

Creating a project from a template must not silently install dependencies or tools, overwrite existing directories, publish repositories or execute arbitrary setup scripts. Any such operation requires a separate, clearly described and authorised action.

### C. Project Doctor

Project Doctor diagnoses common problems in a selected project.

Potential checks include:

- Missing or incompatible runtimes and developer tools.
- Dependency declaration or installation problems.
- Common configuration errors.
- Missing environment-variable names or required configuration keys, without revealing secret values.
- Git repository problems.
- Conflicting development ports.
- Available build and test failures when the user asks ATLAS to run those checks.

Each finding should include its severity, evidence, confidence and an explanation. Suggested fixes must be distinguishable from verified diagnoses. Applying a fix or running a command must pass through AAP and the Permission Manager.

### D. Project Quick Actions

Projects should expose context-aware, configurable actions based on detected project type and user preferences.

Examples include opening the project in a configured editor, opening a terminal at the project root, inspecting dependencies, viewing Git status, running a known development task or opening documentation.

ATLAS must not assume a universal editor, shell, environment manager or start command. Quick Actions should show what they will do and use the normal AAP authorisation path for operations that execute commands or modify data.

### E. Workspace Snapshots

Allow users to save and restore named development workspace configurations.

A snapshot may include:

- Selected projects and project tabs.
- Applications and launch profiles.
- Workspace layout and dashboard arrangement.
- Relevant terminals or development sessions where safely restorable.
- User-selected workspace preferences.

Snapshots should store configuration and references, not duplicate project contents or capture secret values. Restoring a snapshot must explain unavailable applications, moved projects or changed launch configurations before attempting to restore them. Launching applications or processes should be visible and cancellable.

### F. Activity Timeline

Provide a chronological, searchable view of important ATLAS activity, such as projects opened, applications launched, workflows run, AI-requested operations, files changed through ATLAS and tool-management events.

The Activity Timeline is a usability and history feature. It is not a replacement for the security audit log, and it must not expose secret values. Users should be able to understand which actions were requested by AI, which were authorised by the user or policy, and which actually completed.

## 32.2 Agent Git permissions and repository-push control

ATLAS must provide a user-controlled setting that governs whether an AI agent may initiate pushes to remote Git repositories.

Proposed location: **Settings → AI & Agent → Git Permissions**.

### Master setting

- **Allow agent-initiated pushes:** OFF by default.
- When disabled, AI agents cannot initiate remote push operations through Git, shell execution, a Git integration, a workflow or another supported execution path.
- When enabled, the setting only makes agent-initiated pushes eligible for consideration; it does not automatically approve every push.
- The AI must not be able to enable, disable or modify this setting.
- The setting is enforced by ATLAS's Permission Manager and execution layer, not by trusting the AI system prompt.
- The same policy applies across all AI providers, models and working modes.

### Operation coverage

The policy must cover all supported ways of updating a remote repository, including ordinary branch pushes, new-branch pushes, tag pushes and equivalent Git-provider API operations. ATLAS must not allow an agent to bypass the setting by using a terminal command or an alternate integration.

### Separate high-risk operations

- Force pushes must remain separately restricted and require explicit, per-operation user approval. Enabling ordinary agent-initiated pushes must never implicitly authorise force pushes.
- Remote branch deletion must require explicit, per-operation user approval.
- Changing remotes, repository credentials or Git permission settings must not be treated as ordinary push operations.
- Credentials must remain protected by the Secret Vault and must not be disclosed to the AI.

### Confirmation and transparency

The user should be able to choose whether every otherwise-eligible agent push requires confirmation. The recommended default is to require confirmation before every push, even when agent-initiated pushes are enabled.

Before confirmation, ATLAS should show the target repository and remote, destination branch or ref, commits or tags being pushed, and whether the operation is a normal push or has unusual consequences. The user must be able to cancel. Results must distinguish requested, authorised, attempted and successfully completed operations.

A master setting is a policy boundary, not blanket approval. It must not bypass action-specific validation, repository checks or other security controls.

## 32.3 ATLAS Pro additions

### A. Remote Development Manager

Provide a unified interface for supported remote development environments, potentially including SSH hosts, WSL distributions, remote Linux machines and development VPS instances.

Capabilities may include saved connection profiles, connection testing, remote project discovery, remote terminal access and remote project workflows. Credentials must be handled securely, and remote commands and file operations must follow the same permission and audit principles as local actions.

### B. Environment Profiles

Allow projects to define named development environments such as Development, Testing and Production-like.

Profiles may describe runtime versions, environment-variable names and references to Vault-managed values, service configuration, launch settings and tool requirements. Switching profiles must preview material changes and must not expose secret values or silently overwrite user configuration.

### C. AI Project Memory

Provide persistent, structured project knowledge for AI-assisted work.

Potential memory includes architecture summaries, design decisions, coding conventions, dependency information, important file roles, known issues and unfinished tasks.

Users must be able to inspect, edit, export and delete this memory. ATLAS should record provenance or confidence where practical, distinguish verified facts from AI assumptions, and refresh or revalidate information that may have become stale. Project memory must respect context-sharing and privacy settings.

### D. Build & Test Centre

Unify supported project build and test workflows in one interface.

Capabilities may include discovering build and test commands, running selected checks, displaying structured results, grouping failures, preserving relevant logs and comparing results across runs. ATLAS must show the command or task before execution and apply AAP permission checks. Test coverage should be shown only when supplied by a supported tool.

### E. Dependency Security Centre

Analyse project dependencies for known vulnerabilities, outdated versions and licence information where reliable data sources are available.

Results should show the source and freshness of the data, affected dependency and version, severity, confidence and possible remediation. ATLAS must distinguish confirmed advisories from uncertain or incomplete matches. Updating dependencies requires a reviewed plan and normal authorisation.

### F. Architecture Visualizer

Generate navigable visual representations of project structure, modules, entry points and dependency relationships where they can be reliably detected.

The visualizer should explain the evidence used to infer relationships and distinguish detected relationships from inferred ones. It should not present an incomplete scan as a complete architecture map.

### G. Visual Workflow Builder

Provide a visual editor for creating workflows from triggers, actions, conditions, delays and approval checkpoints.

Workflows must remain inspectable, editable, testable and cancellable. Each action must retain its own permission requirements; a workflow must not acquire unrestricted permissions merely because it is saved or triggered automatically.

### H. AI Task Delegation

Allow a larger development task to be decomposed into smaller tasks and assigned to different AI providers or agents where supported.

The system must manage shared project context, task dependencies, conflicting edits, result review and integration. Each agent remains subject to the same AAP protocol, user settings and Permission Manager. Delegation must not multiply or bypass permissions, and conflicting changes must be surfaced rather than silently overwritten.

### I. Extension ecosystem

Expand the extension system so developers can add integrations, panels, tools and workflow actions.

Extensions must declare their capabilities and permissions, receive only the access granted by the user and be restricted by an enforceable permission boundary. Vault access, unrestricted filesystem access and arbitrary command execution must never be granted by default.

## 32.4 Roadmap guidance

The following is the current placement guidance, not a promise that every feature will fit into a particular event or release:

**Core candidates**
- First-run interactive tutorial, accessible again from Settings.
- Built-in and user-created Project Templates.
- Project Doctor.
- Project Quick Actions.
- Workspace Snapshots.
- Activity Timeline.
- Agent Git permission setting and secure push-policy enforcement.

**Pro candidates**
- Remote Development Manager.
- Environment Profiles.
- AI Project Memory.
- Build & Test Centre.
- Dependency Security Centre.
- Architecture Visualizer.
- Visual Workflow Builder.
- AI Task Delegation.
- Expanded extension ecosystem.

Core should provide working foundations that Pro can extend. For example, Core can provide local project diagnosis while Pro adds deeper build and dependency analysis; Core can provide basic project context while Pro adds persistent AI Project Memory; Core can manage local projects while Pro adds remote development environments.

The roadmap must still prioritise complete, reliable workflows over feature count. These additions do not change the distinction between planned, in-progress, implemented and tested functionality.

