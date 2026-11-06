# Activity Timeline

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Transparency and audit history

## 1. Purpose

Activity Timeline gives users a clear history of important ATLAS events and operations. It should answer: what was requested, what ATLAS understood, what required approval, what actually ran and what happened afterward.

## 2. Events to record

Potential event types include project registration changes, application launches, tool installation attempts, workflow runs, AI action requests, permission decisions, file operations, Git operations, voice sessions and system-task outcomes. The event catalogue should be explicit and versioned.

## 3. Event lifecycle

For actions, represent distinct states rather than collapsing them into one entry:
- Requested: an interface or agent asked for an operation.
- Validated: the request passed schema and parameter checks.
- Awaiting approval: user input is required.
- Approved or denied: the user's decision.
- Started: execution began.
- Completed, failed, cancelled or timed out: final known outcome.

A request that was denied or never executed must never appear as completed. Partial completion should be represented explicitly.

## 4. Event details

Where useful, show timestamp, source interface, active project, action type, target, concise description, policy result, approval decision and final status. Provide a safe detail view with relevant output or error information. Keep event descriptions understandable without hiding important technical details.

## 5. Search and filters

Allow filtering by project, event category, status, date range and source (Chat, Voice, workflow, user action or extension). Search should operate on safe metadata and descriptions. Pagination or bounded loading should keep large histories responsive.

## 6. Privacy and retention

- Never store raw Vault secrets, API keys or credential-bearing URLs.
- Redact sensitive command arguments and environment values.
- Avoid retaining full file contents when a path, diff summary or hash is sufficient.
- Make retention and clearing controls understandable.
- Voice transcripts and raw audio require separate handling; raw recordings should not be retained by default.
- Local activity history should remain local unless the user explicitly chooses an external sync service.

## 7. Integrity and limitations

The timeline is an operational record, not a tamper-proof forensic audit system. If an event cannot be recorded because storage failed, ATLAS should surface that limitation for security-relevant actions. Never fabricate missing events or infer completion from an AI response.

## 8. Acceptance criteria

- Requested, approved, attempted and completed states are distinguishable.
- Users can filter and inspect events.
- Denied and failed actions remain visible with a safe explanation.
- Secret values are redacted.
- Users can clear history according to retention settings.
- A missing log entry is not silently presented as proof that no action occurred.

## 9. Dependencies and open decisions

Consumes structured events from AAP, Permission Manager, Git Centre, Workflow Automation and Voice. Define event schema, retention defaults and export format before implementation.

## 10. Related documentation

- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Agent Git Permissions](agent-git-permissions.md)
- [Voice Essentials](voice-essentials.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
