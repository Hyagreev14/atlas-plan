# ATLAS Core vs Pro

This is the current planned release split, not a promise that every feature will fit a fixed schedule.

## ATLAS 0.1 — Core

Core is the first functional foundation. It should be useful on its own and establish the shared architecture that later releases can extend.

| Feature | Purpose |
|---|---|
| [Developer Home](Features/Core/developer-home.md) | Daily dashboard for projects, quick actions, sessions, Git activity and notifications. |
| [Project Hub](Features/Core/project-hub.md) | Register, organise, open and inspect user-selected development projects. |
| [Universal App Launcher](Features/Core/universal-app-launcher.md) | Search and launch installed applications and saved launch groups. |
| [Developer Tool Manager](Features/Core/developer-tool-manager.md) | Detect developer tools and offer user-approved installation workflows. |
| [AI Workspace](Features/Core/ai-workspace.md) | Helper/Tutor, Developer and Hybrid AI modes. |
| [AI Model Manager](Features/Core/ai-model-manager.md) | Manage local models and optional cloud AI providers. |
| [Hardware Profiler](Features/Core/hardware-profiler.md) | Assess hardware and model compatibility. |
| [System Monitor](Features/Core/system-monitor.md) | Monitor system resources and development processes. |
| [Git Centre](Features/Core/git-centre.md) | Inspect and manage local Git repositories. |
| [Workflow Automation](Features/Core/workflow-automation.md) | Create visible, reusable development workflows. |
| [Developer Productivity Tools](Features/Core/developer-productivity-tools.md) | Notes, snippets, search, clipboard and other workspace utilities. |
| [Secret Vault](Features/Core/secret-vault.md) | Protect API keys and credentials locally. |
| [Privacy and Offline Operation](Features/Core/privacy-and-offline.md) | Control external data sharing and local-only operation. |
| [AAP and Safe Execution](Features/Core/aap-and-safe-execution.md) | Structured AI action requests validated and authorised by ATLAS. |
| [ATLAS Voice Essentials](Features/Core/voice-essentials.md) | Push-to-talk, speech recognition, spoken responses and basic ATLAS actions. |
| [First-Run Tutorial](Features/Core/onboarding-tutorial.md) | Skippable onboarding that can be reopened from Settings. |
| [Project Templates](Features/Core/project-templates.md) | Create projects from built-in and custom templates. |
| [Project Doctor](Features/Core/project-doctor.md) | Diagnose common project configuration and dependency issues. |
| [Project Quick Actions](Features/Core/project-quick-actions.md) | Context-aware actions for selected projects. |
| [Workspace Snapshots](Features/Core/workspace-snapshots.md) | Save and restore workspace configurations. |
| [Activity Timeline](Features/Core/activity-timeline.md) | Review important ATLAS activity and action outcomes. |
| [Agent Git Permissions](Features/Core/agent-git-permissions.md) | User-controlled policy for AI-initiated remote Git pushes. |

## ATLAS Pro

Pro builds on Core with deeper automation, remote workflows and advanced AI capabilities.

| Feature | Purpose |
|---|---|
| [Remote Development Manager](Features/Pro/remote-development-manager.md) | Manage SSH, WSL and remote development environments. |
| [Environment Profiles](Features/Pro/environment-profiles.md) | Define named project environments and configuration profiles. |
| [AI Project Memory](Features/Pro/ai-project-memory.md) | Maintain user-controlled persistent project knowledge. |
| [Build & Test Centre](Features/Pro/build-and-test-centre.md) | Run and review project build and test workflows. |
| [Dependency Security Centre](Features/Pro/dependency-security-centre.md) | Review dependency vulnerabilities, updates and licence data. |
| [Architecture Visualizer](Features/Pro/architecture-visualizer.md) | Explore detected project structure and relationships. |
| [Visual Workflow Builder](Features/Pro/visual-workflow-builder.md) | Create workflows using a visual editor. |
| [AI Task Delegation](Features/Pro/ai-task-delegation.md) | Coordinate multi-step tasks across supported AI agents. |
| [Extension Ecosystem](Features/Pro/extension-ecosystem.md) | Add integrations and capabilities through declared permissions. |
| [Advanced Voice](Features/Pro/advanced-voice.md) | Wake-word activation and richer continuous voice workflows. |
| [Visual Context Mode](Features/Pro/visual-context-mode.md) | Optional screenshot context for vision-capable models. |

## Placement principles
- Core must be useful without Pro.
- Pro adds meaningful depth rather than withholding essential Core functionality.
- Both releases share project context, AAP and the Permission Manager.
- Planned does not mean implemented or tested.
