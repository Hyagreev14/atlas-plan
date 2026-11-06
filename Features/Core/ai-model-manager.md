# AI Model Manager

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** AI providers and model lifecycle

## 1. Purpose

AI Model Manager gives users control over which AI providers and models ATLAS uses. It should support local models where suitable and optional cloud APIs where configured, while making compatibility, resource requirements, privacy and costs understandable.

## 2. Provider catalogue

Represent providers through adapters with declared capabilities, configuration requirements and processing location. A provider may be local, cloud-hosted or self-hosted. Do not imply that a model is local merely because its API is accessed from the user's computer.

For each configured provider/model, show its name, source, availability, context capability where known, supported modalities, tool/action compatibility and last connection status. Clearly label unknown or unverified capabilities.

## 3. Model selection

Users can choose a default model and optionally configure task-specific choices if supported. Show which model will handle a request before sending when the choice is not obvious. Chat and Voice may have separate interface modes, but provider/model policy should be consistent and visible.

Do not silently switch models when a request fails or requires a capability the selected model lacks. Explain the limitation and offer a user-controlled alternative.

## 4. Local model management

For local models, show model size, quantization, expected disk use and estimated RAM/VRAM needs when reliable information is available. Explain that estimates vary by runtime, context length, offloading and concurrent applications.

Downloading a model requires explicit consent and a review of storage and resource impact. Support cancellation and cleanup of incomplete downloads. Do not delete a model currently in use without confirmation.

## 5. Hardware compatibility

Integrate with Hardware Profiler to compare the model's requirements with detected CPU, RAM, GPU, available memory and storage. Distinguish measured system facts from estimates. Provide a warning when a model may be slow or exceed available resources, but do not falsely guarantee performance.

A user may choose to continue after seeing a warning. ATLAS should not conceal the warning or repeatedly pressure the user.

## 6. API configuration and costs

Allow users to configure provider credentials through Secret Vault or a provider-supported secure authentication flow. Never display full API keys after saving. Explain whether usage may incur provider charges and show pricing only when current and reliably sourced; otherwise link users to the provider's current pricing information.

## 7. Capability matching

Before a task, determine whether the selected model supports required inputs such as images or tool use. If unsupported, explain the mismatch. Never silently change to a vision-capable model, download a model or send content to another provider.

## 8. Reliability

Handle unavailable local runtimes, invalid credentials, quota limits, network errors and model-not-found errors with actionable messages. Preserve user input during failures. Provide a connection test that does not expose credentials.

## 9. Privacy and security

- Make local versus cloud processing explicit.
- Do not send project context to a provider without the user's configured consent.
- Keep credentials in Secret Vault, never model context.
- Do not log authorization headers or full secrets.
- Do not silently enable telemetry or provider fallback.

## 10. Acceptance criteria

- Users can add, test, select and remove provider configurations.
- Local model downloads require consent and show resource estimates.
- Unsupported capabilities are explained before content is sent.
- Provider switching never happens silently.
- API credentials are stored and used without being exposed to the model.
- Hardware warnings distinguish estimates from verified facts.

## 11. Dependencies and open decisions

Depends on Hardware Profiler, Secret Vault, Privacy settings and AI Workspace. Select initial provider adapters and local runtime support after validating the target platforms and laptop-class hardware constraints.

## 12. Related documentation

- [Hardware Profiler](hardware-profiler.md)
- [Secret Vault](secret-vault.md)
- [AI Workspace](ai-workspace.md)
- [Privacy and Offline Operation](privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
