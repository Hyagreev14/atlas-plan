# Agent Git Permissions

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Security and user-controlled authorisation

## 1. Purpose

This feature gives the user an explicit, central setting controlling whether an AI agent may initiate remote Git pushes. It prevents an agent from publishing commits to a remote repository merely because it can run a terminal command or access a Git integration.

## 2. Setting location and default

**Settings → AI & Agent → Git Permissions**

Setting: **Allow agent-initiated pushes**  
Default: **OFF**

The setting must be visible, understandable and controlled only by the user through the ATLAS settings interface. AI models, prompts, plugins, workflows and project files cannot change it.

## 3. Policy semantics

When OFF:
- An AI agent cannot initiate a remote push through any supported route.
- This includes terminal execution, Git Centre, AAP actions, workflows, delegated agents and extensions.
- The user may still perform a push directly through an explicit user-controlled Git operation, subject to normal ATLAS behaviour.
- An AI request to push must be denied or converted into an explanation/instruction for the user; it must not be disguised as another command.

When ON:
- Agent-initiated pushes become eligible for consideration, not automatically authorised.
- The Permission Manager still evaluates the specific operation.
- The recommended default is to ask for confirmation before each push.
- The confirmation must identify repository, remote, destination branch/ref and commits/tags being sent.
- The setting does not grant credentials or relax other security checks.

## 4. Separately restricted operations

Force pushes and remote branch deletion remain separately restricted and require explicit per-operation approval. Enabling agent-initiated pushes must never implicitly enable these operations. Other destructive remote operations should be classified by the Permission Manager.

## 5. Enforcement architecture

The setting is a policy boundary enforced by the central Permission Manager and execution layer, not a prompt instruction or UI-only toggle. Every route to a remote push must call the same policy evaluator. The execution layer must reject an operation when policy denies it, even if an AI provider emits a valid-looking AAP request.

The AI-generated action schema must not contain authoritative fields such as `approved`, `requires_approval`, `trusted` or permission-granting values. The model cannot decide whether confirmation is needed.

## 6. User experience

- Explain the default OFF state and its effect.
- Warn that enabling it allows an agent to request remote publication, but does not remove per-operation checks.
- Display a clear denied reason when an agent push is blocked.
- Show the exact operation details in confirmation UI.
- Make it possible to disable the setting at any time.
- Do not silently toggle the setting as part of onboarding or project setup.

## 7. Audit and accountability

Activity Timeline should record the requesting interface/agent, repository, target remote/ref, policy decision, user decision and final outcome. Do not record credentials or token values. Distinguish blocked, awaiting approval, approved, attempted, failed and completed states.

## 8. Edge cases

- A shell command that invokes `git push` must be detected or restricted by the execution policy; the system must not rely only on a dedicated Git button.
- Aliases, scripts, hooks and workflow steps must not create a bypass.
- If the remote or destination cannot be identified confidently, deny or request clarification rather than guessing.
- A change to the setting must not retroactively approve a previously blocked action.
- Delegated agents inherit the same policy; they do not get a separate permission scope.

## 9. Acceptance criteria

- The setting is OFF on a fresh installation.
- No AI-initiated push succeeds while the setting is OFF.
- Every supported execution path uses the same policy enforcement.
- Turning it ON does not remove per-push confirmation by default.
- Force pushes and remote branch deletion remain separately gated.
- AI cannot modify the setting or approve an operation.
- All decisions and outcomes are auditable without storing secrets.

## 10. Dependencies and related documentation

Depends on AAP, Permission Manager, Git Centre, Activity Timeline, Secret Vault and any terminal/workflow execution service.

- [Git Centre](git-centre.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Activity Timeline](activity-timeline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
