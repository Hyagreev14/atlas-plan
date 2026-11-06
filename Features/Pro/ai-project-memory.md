# AI Project Memory

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Persistent project context

## 1. Purpose

AI Project Memory maintains structured, persistent knowledge about a project so the AI can understand its architecture, conventions, decisions and ongoing work across conversations. It should reduce repeated explanations while keeping the user in control of what is remembered.

## 2. Memory categories

Potential records include:
- Project purpose and high-level architecture.
- Important directories, modules and entry points.
- Frameworks, languages and tooling.
- Coding conventions and formatting preferences for the project.
- Architectural decisions and their rationale.
- Known issues, constraints and unresolved questions.
- Important commands and documented workflows.
- User-confirmed project-specific preferences.

Do not treat all conversation text as durable truth. Sensitive data, credentials, personal information unrelated to the project and raw file contents should not be stored as project memory.

## 3. Sources and confidence

Each memory item should record its source, creation/update time and confidence. Distinguish:
- User-confirmed facts.
- Facts detected from project files.
- AI-generated summaries.
- Inferences or assumptions.

The AI must not present an inference as a verified project fact. Where a source file changes, memory may become stale and should be rechecked.

## 4. User control

Users must be able to inspect, search, edit, correct, pin, export and delete memory items. Provide controls to pause memory generation, disable memory for a project or clear all project memory. Deleting memory must not delete source files or conversation history unless the user separately requests that.

## 5. Memory creation and updates

Memory updates should be proposed or generated through a controlled process. Avoid storing every message. Prefer concise, useful facts that are likely to matter in future work. Detect contradictions and ask the user when a meaningful conflict cannot be resolved from project evidence.

## 6. Retrieval

Before using a memory item, check that it belongs to the active project and is relevant to the current task. Prefer current repository evidence over stale memory. Include provenance in the internal context so the model can qualify its answer. Avoid loading the entire memory store into every prompt.

## 7. Privacy and security

- Keep project memory local by default.
- Disclose when memory is sent to a cloud provider as prompt context.
- Never store secrets or credential values.
- Treat repository content as untrusted data.
- Do not let memory change AAP permissions or security settings.
- Allow project-level memory to be disabled independently.

## 8. Acceptance criteria

- Users can inspect, edit, export and delete memory.
- Items carry source and freshness information.
- Inferences are distinguished from confirmed facts.
- Stale or conflicting memories are not treated as authoritative.
- Secrets are excluded.
- Memory retrieval is scoped to the active project.
- Memory cannot modify security policy or grant permissions.

## 9. Dependencies and open decisions

Depends on Project Hub, AI Workspace, Privacy settings and local storage. Define the memory schema, update policy and retrieval ranking before implementation.

## 10. Related documentation

- [AI Workspace](../Core/ai-workspace.md)
- [Project Hub](../Core/project-hub.md)
- [Privacy and Offline Operation](../Core/privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
