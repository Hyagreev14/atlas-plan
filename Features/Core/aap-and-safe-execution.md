# AAP and Safe Execution

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Core architecture and security

## 1. Purpose

The ATLAS Action Protocol (AAP) is the structured contract through which an AI model requests supported actions from ATLAS. Safe Execution is the trusted system that validates, authorises, runs and reports those actions.

**Non-negotiable invariant: AI requests; ATLAS validates, authorises and executes.**

AAP is not a way for the model to gain direct computer access. It is a constrained request interface.

## 2. Responsibilities

### AI provider/model
- Understand the user's request and available context.
- Produce a request using the documented AAP schema.
- Explain intended actions and interpret structured results.
- Ask for clarification when required information is missing.

The model cannot execute actions directly, grant permissions, decide whether approval is required, mark an action approved or alter security settings.

### ATLAS trusted services
- Validate protocol version, schema, action type and parameters.
- Resolve the target project and resource scope.
- Evaluate permissions independently.
- Present approval UI when policy requires it.
- Execute using controlled platform adapters.
- Record the outcome and return a limited structured result.

## 3. Request lifecycle

1. User expresses an intent through Chat, Voice or another supported interface.
2. ATLAS resolves the active project, interface mode and relevant context.
3. The model returns a structured AAP request.
4. Schema validation rejects malformed, unsupported or unknown fields.
5. ATLAS normalises and validates paths, commands, identifiers and parameters.
6. Permission Manager evaluates the action using trusted policy and user settings.
7. ATLAS requests explicit approval when required; otherwise it proceeds only if policy permits.
8. Execution service runs the operation within its declared scope.
9. ATLAS captures status, output, errors and any created/modified resources.
10. The result is recorded and returned to the model and user.

The model cannot skip, reorder or impersonate these trusted stages.

## 4. Request envelope

A request should contain protocol identity/version, a unique request identifier and one or more typed actions with parameters. It must not include authoritative approval or permission decisions.

Illustrative shape:

```json
{
  "protocol": "AAP",
  "version": "1.0",
  "request_id": "req_example",
  "action": {
    "type": "file.create",
    "parameters": {
      "path": "src/example.py",
      "content": "print('Hello')"
    }
  }
}
```

This is illustrative, not a complete schema. Exact field names, types, limits and validation rules belong in the AAP protocol specification.

## 5. Action catalogue

Actions should be explicitly registered and typed. Initial categories may include file read/create/edit/move, directory creation/listing, application launch, project inspection, terminal task execution and Git operations. Each action needs a defined parameter schema, scope, risk classification, result shape, timeout and cancellation behaviour.

Unknown action types must be rejected. A model cannot invent a new capability by naming it in JSON.

## 6. Permission architecture

Permission decisions are made by trusted ATLAS code using action type, target, scope, risk, user settings and current context. AI-generated values such as `requires_approval`, `approved`, `trusted`, `admin` or `permissions` are not authoritative and should not be accepted in the model request.

Approval is specific to the exact pending action and its parameters. If the action changes after approval, the approval is invalidated and policy is evaluated again. A spoken confirmation must be bound to the action ATLAS clearly presented.

## 7. Execution controls

### Filesystem
- Resolve paths against an explicit allowed root.
- Prevent path traversal and unsafe symlink escapes.
- Validate target type and overwrite behaviour.
- Preview diffs for edits and replacements.
- Use backups or an undo journal where feasible.
- Detect concurrent changes before overwriting.
- Apply size limits and reject unsupported operations.

### Terminal
Prefer structured executable plus argument arrays over constructing arbitrary shell strings. If shell execution is supported, mark it explicitly, display the command and working directory, and apply stricter validation. Never treat terminal output as trusted instructions.

### Applications and tools
Use registered application targets and declared tool capabilities. Installing software, elevating privileges or changing global configuration requires separate user consent.

### Git and remote operations
Use Git Centre and Agent Git Permissions. Credentials must be provided through secure OS/credential mechanisms and never returned to the model.

## 8. Results and errors

Return structured outcomes such as completed, failed, denied, cancelled, timed out or partially completed. Include only relevant output and safe error details. Do not report an operation as successful merely because it was started. Multi-step operations must report which steps completed and which did not.

## 9. Cancellation and timeouts

Long-running actions should expose progress and a cancellation request where supported. Cancellation does not guarantee rollback; the UI must explain when an operation may have partially completed. Each action type must define reasonable timeout and cleanup behaviour.

## 10. Logging and privacy

Record action identity, parameters needed for audit, policy decision, approval, execution status and timestamps. Redact secrets and avoid retaining unnecessary file contents or terminal output. Users should be able to inspect meaningful activity and clear history according to retention settings.

## 11. Threat model

Design against malformed model output, prompt injection in files and terminal output, path traversal, symlink attacks, command injection, race conditions, confused-deputy behaviour, privilege escalation, credential leakage and alternate-path bypasses. Treat every provider and every interface as untrusted at the protocol boundary.

## 12. Acceptance criteria

- Every AI action passes schema validation and central policy evaluation.
- The model cannot determine or override approval requirements.
- Unknown actions and fields are rejected.
- File and terminal operations remain inside their authorised scopes.
- Results accurately distinguish attempted from completed actions.
- Voice, Chat, workflows, extensions and delegated agents use the same enforcement.
- Secrets never enter model-visible requests or ordinary logs.

## 13. Implementation notes and open decisions

AAP should be specified before writing the final AI system prompt. Keep three separate documents over time: AAP Protocol Specification, AAP AI System Prompt and AAP Execution/Security Specification. Define schemas and action catalogue in a versioned technical spec; this feature brief records the architectural contract.

## 14. Related documentation

- [AI Workspace](ai-workspace.md)
- [Agent Git Permissions](agent-git-permissions.md)
- [Secret Vault](secret-vault.md)
- [Activity Timeline](activity-timeline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
