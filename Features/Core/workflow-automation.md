# Workflow Automation

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Repeatable development workflows

## 1. Purpose

Workflow Automation lets users create and run visible, reusable sequences of development actions. It should make common routines repeatable without hiding what ATLAS will do or turning a workflow into an unrestricted background script engine.

## 2. Workflow model

A workflow consists of a name, description, optional project scope, trigger, ordered steps, conditions and failure behaviour. Each step must have a declared action type and parameters. The workflow should be inspectable in human-readable form before it is saved or run.

Core should prioritise manually started workflows. Automatic triggers and complex branching should be limited until the security and reliability model is proven.

## 3. Example workflows

- Open a project, launch its IDE and open a terminal at the project root.
- Check Git status, then show changed files.
- Run a user-approved development server command.
- Execute a sequence of read-only project checks.
- Open a set of documentation pages and tools for a project.

Examples are templates for user configuration, not permission to execute commands automatically.

## 4. Step types

Potential step categories include application launch, project navigation, file inspection, approved file operations, terminal task, Git operation, wait, condition and notification. Each step type must define inputs, output, timeout, cancellation behaviour and permission classification.

## 5. Execution and permissions

Every step passes through AAP validation and the Permission Manager. A workflow cannot bundle actions into one blanket approval if the underlying actions require separate approval. Approval is tied to the exact step and its parameters. Agent Git Permissions apply to pushes inside workflows. Secret Vault values are not exposed to workflow definitions or AI context.

## 6. Failure and recovery

Define whether a workflow stops, skips an optional step or continues after a failure. Show the step that failed and its output. Do not automatically retry destructive operations. Cancellation should stop future steps and request cancellation of the current step where supported. Explain when partial effects may remain.

## 7. Editing and versioning

Users can create, rename, duplicate, edit and delete workflows. Before a workflow changes, show its steps and any permission-impacting changes. A saved workflow should retain a version or last-edited timestamp so the user can identify stale configurations.

## 8. Scheduling and background operation

Scheduling is not required for the first Core version. If added later, it must be explicitly enabled, display when it will run and provide a clear pause/disable control. A scheduled workflow must not bypass approval requirements or silently execute a newly changed step.

## 9. Acceptance criteria

- Users can create and manually run a simple multi-step workflow.
- Each step is visible before execution.
- Every step receives independent validation and policy checks.
- Failures, cancellation and partial completion are accurately shown.
- Git push restrictions apply inside workflows.
- Workflows can be edited, duplicated, paused and deleted.

## 10. Dependencies and open decisions

Depends on AAP, Permission Manager, Activity Timeline, Project Hub, Git Centre and Universal App Launcher. Define a small step catalogue and workflow storage schema before adding triggers or complex branching.

## 11. Related documentation

- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Activity Timeline](activity-timeline.md)
- [Agent Git Permissions](agent-git-permissions.md)
- [Project Quick Actions](project-quick-actions.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
