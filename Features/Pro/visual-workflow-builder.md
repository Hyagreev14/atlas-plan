# Visual Workflow Builder

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Visual automation authoring

## 1. Purpose

Visual Workflow Builder provides a graphical editor for creating and understanding development workflows. It extends Core Workflow Automation with a node/edge interface for triggers, actions, conditions and approval checkpoints.

## 2. Workflow graph

A workflow is a directed graph of typed nodes and connections. Each node declares its inputs, outputs, parameters, permissions, timeout and failure behaviour. Invalid connections or missing required inputs should be shown before the workflow can be saved or run.

## 3. Node categories

Potential nodes include:
- Manual start and supported event triggers.
- Application launch and project navigation.
- File inspection and approved file operations.
- Terminal task execution.
- Git inspection and permitted Git actions.
- Conditions based on explicit task results.
- Wait/delay and notification.
- Approval checkpoint.
- Workflow result/output.

The available node catalogue must remain explicit. Users cannot create arbitrary privileged node types through free-form text.

## 4. Editing experience

Support adding, connecting, moving, configuring, duplicating and deleting nodes. Provide zoom, pan, minimap or equivalent navigation for larger graphs. Include a readable list/outline view for accessibility and keyboard users. Validate the graph continuously and explain errors in context.

## 5. Execution preview

Before running, show the planned execution path, relevant conditions, project/target, commands and actions that may require approval. Dynamic branches should be explained. A graph preview is not a substitute for per-action permission checks.

## 6. Permissions and execution

Every node is independently validated and authorised by AAP and Permission Manager. Approval checkpoints must be explicit but cannot weaken the central policy. A workflow cannot use a harmless-looking node to hide a destructive operation. Agent Git Permissions and Secret Vault rules apply to all nodes.

## 7. Versioning and debugging

Save workflow versions or a clear last-edited record. Provide a run view showing which nodes executed, skipped, failed, awaited approval or were cancelled. Allow users to inspect inputs/outputs with secret redaction. Debugging should support safe dry-run or preview modes where meaningful, without claiming that a dry run proves real execution will succeed.

## 8. Import and sharing

If workflow import/export is supported, validate the file format and display requested capabilities before importing. Imported workflows are untrusted and must not execute on import. Sharing should not include secret values or private project data by default.

## 9. Acceptance criteria

- Users can build a valid workflow from typed nodes.
- Invalid graphs are identified before execution.
- Users can inspect the execution plan.
- Every node passes independent policy checks.
- Runs show node-level status and useful errors.
- Imported workflows do not execute automatically.
- A list/accessible view is available alongside the graph.

## 10. Dependencies and open decisions

Depends on Core Workflow Automation, AAP, Permission Manager, Activity Timeline and Extension Ecosystem's action catalogue. Define the graph schema and supported node types before implementing visual editing.

## 11. Related documentation

- [Workflow Automation](../Core/workflow-automation.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Activity Timeline](../Core/activity-timeline.md)
- [Extension Ecosystem](extension-ecosystem.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
