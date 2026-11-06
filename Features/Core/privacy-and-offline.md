# Privacy and Offline Operation

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Privacy and data control

## 1. Purpose

Privacy and Offline Operation defines how ATLAS handles local data, external AI providers, optional integrations and network-dependent features. Users should understand what stays on their computer, what may leave it and how to disable external processing.

## 2. Local-first baseline

Basic desktop functionality such as project registration, application launching, local notes and local settings should work without an ATLAS-hosted account or cloud backend. A network connection may be needed for optional provider APIs, downloads, updates or remote services; this must not be confused with a requirement for an ATLAS account.

## 3. Data categories

Document the handling of:
- Application settings and UI preferences.
- Project names, paths and metadata.
- File contents or selected code context.
- AI prompts, responses and conversation history.
- Voice audio and speech transcripts.
- Screenshots and visual context.
- API credentials and other secrets.
- Activity records and diagnostic logs.
- Provider configuration and usage metadata.

For each category, define storage location, whether it can be transmitted, retention behaviour and user controls.

## 4. External provider disclosure

Before sending content to a cloud AI provider, make the provider and relevant data category clear. Explain that provider policies govern processing after transmission. Do not silently change from local to cloud processing, enable a new provider or send more project context than the user selected.

A provider failure must not cause an automatic fallback that sends content elsewhere. If an alternative is available, ask the user.

## 5. Offline behaviour

When offline, local features should remain available where their dependencies are installed. Cloud AI, online package discovery, remote Git operations and update checks may be unavailable. Show which feature is unavailable and why. Do not imply that an offline model exists unless one is configured and ready.

## 6. Data minimisation

- Include only context needed for the current task.
- Respect user-selected exclusions and project scope.
- Avoid whole-repository uploads by default.
- Do not send secrets or raw credential values to models.
- Avoid collecting unnecessary device identifiers.
- Do not retain screenshots or raw microphone audio by default.
- Keep diagnostic logs useful but redacted.

## 7. User controls

Provide clear controls to inspect provider settings, choose local/cloud processing, manage project context, clear conversation/activity history, disable optional network features and remove stored local data. Explain the effect of each control. A setting should not claim to erase data already transmitted to an external provider.

## 8. Updates and telemetry

If update checks or telemetry are introduced, disclose the endpoint, purpose and data sent. Telemetry should be optional and minimised. Updates must come from a trusted source and should not silently change security preferences or install unrelated tools.

## 9. Acceptance criteria

- Users can identify local versus cloud features.
- External data sharing is disclosed before transmission.
- Provider fallback never happens silently.
- Core local features remain usable offline when dependencies are present.
- Secret values are excluded from prompts and logs.
- Retention and deletion controls are available and accurately described.

## 10. Dependencies and open decisions

Cross-cutting requirement for AI Workspace, AI Model Manager, Secret Vault, Voice, Visual Context Mode and Activity Timeline. Define a data-flow inventory and privacy review before implementation.

## 11. Related documentation

- [AI Workspace](ai-workspace.md)
- [AI Model Manager](ai-model-manager.md)
- [Secret Vault](secret-vault.md)
- [Voice Essentials](voice-essentials.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
