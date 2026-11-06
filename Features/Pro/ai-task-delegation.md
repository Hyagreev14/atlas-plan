# AI Task Delegation

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Multi-step AI coordination

## 1. Purpose

AI Task Delegation allows ATLAS to break a larger development request into smaller, trackable subtasks and coordinate supported AI providers or agents. The goal is to manage complex work transparently, not to create uncontrolled autonomous agents.

## 2. Task planning

For a complex request, ATLAS may produce a plan containing:
- Overall goal and expected outcome.
- Subtasks and dependencies.
- Required project context and tools.
- Proposed provider/model for each subtask, where supported.
- Expected files or resources affected.
- Risks, assumptions and unknowns.
- Validation steps.

The user should be able to inspect and revise the plan before execution begins. A plan is not permission to execute every step.

## 3. Delegation model

Each subtask has a clear owner/agent, input context, expected output, status and dependency state. Delegated agents should receive only the context needed for their task. They should return proposals, code changes or structured results through the ATLAS coordinator.

## 4. Shared workspace and conflicts

ATLAS must manage concurrent edits carefully. Prefer isolated workspaces, branches or staged patches where practical. Before combining changes, detect overlapping file modifications and present conflicts. Never silently overwrite another agent's or the user's changes.

## 5. Permission inheritance

Delegation does not multiply permissions. Every agent and subtask uses the same central AAP validation and Permission Manager. A delegated agent cannot approve its own operation, change the user's settings, access raw Vault secrets or bypass Tutor restrictions. Git push policy applies across all delegated agents and execution routes.

## 6. Provider and resource selection

Show which provider/model handles each task and whether it is local or cloud-based. Disclose data sharing and possible API usage costs. Do not silently move project context to another provider because one agent is unavailable. Ask before changing provider or processing location.

## 7. Progress and cancellation

Provide a task board or timeline with queued, running, awaiting approval, blocked, completed, failed and cancelled states. Show dependencies and useful progress information without inventing completion percentages. Users can cancel the overall task or an individual subtask. Cancellation should stop future work and request cancellation of active operations where supported.

## 8. Validation and final review

Delegated output is not automatically correct. The coordinator should collect changes, run only approved validation tasks and present a final summary with files changed, tests actually run, unresolved issues and decisions requiring the user. Never claim tests passed if they were not run.

## 9. Acceptance criteria

- Large requests can be decomposed into inspectable subtasks.
- Dependencies and ownership are visible.
- Conflicting edits are detected or isolated.
- Provider changes require disclosure and user control.
- Permissions are enforced per action across every agent.
- Users can cancel tasks and inspect partial results.
- Final reports distinguish generated work from validated work.

## 10. Dependencies and open decisions

Depends on AI Workspace, AAP, Permission Manager, Project Hub, Activity Timeline and Build & Test Centre. Decide whether initial delegation uses one provider with multiple task roles or multiple independent providers.

## 11. Related documentation

- [AI Workspace](../Core/ai-workspace.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Build & Test Centre](build-and-test-centre.md)
- [Activity Timeline](../Core/activity-timeline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
