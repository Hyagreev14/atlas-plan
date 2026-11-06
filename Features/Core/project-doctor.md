# Project Doctor

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Project diagnostics

## 1. Purpose

Project Doctor inspects a selected project and reports common development setup or configuration problems. It should help users understand likely causes and next steps without pretending that static checks can always identify the root cause.

## 2. Diagnostic scope

Initial checks may include:
- Required developer tool missing or incompatible version.
- Recognisable dependency manifest with missing installation state.
- Common configuration-file errors when a reliable parser is available.
- Missing expected project files or entry points.
- Conflicting or unavailable development ports.
- Git repository state that may affect a workflow.
- Environment mismatch between project requirements and selected environment.
- Known build/test command configuration problems.

The supported checks must be explicit. Do not scan arbitrary files or execute project scripts simply to guess what is wrong.

## 3. Findings model

Each finding should include:
- Short title and plain-language explanation.
- Severity (informational, warning or error).
- Evidence and affected file/tool/path.
- Confidence or certainty level.
- Whether it is detected directly or inferred.
- Suggested next step.
- Whether an automated fix is available.

Do not label a suggestion as a verified diagnosis. Distinguish a confirmed parse error from a heuristic warning.

## 4. Safe repair workflow

For a proposed fix, explain what will change and why. Where possible show a diff or command preview. Require approval for file modifications, dependency installation, configuration changes or command execution. Use AAP and the central Permission Manager. Never apply a batch of fixes without showing the scope.

Allow users to dismiss a finding, mark it as understood or rerun the relevant check. Dismissing a warning should not silently modify project files.

## 5. Diagnostics execution

Read-only checks should be preferred. Running build scripts, package managers or project-defined commands can execute arbitrary code and must be treated as an execution action with appropriate review and approval. Set timeouts and provide cancellation where possible.

## 6. Results and history

Show when a scan ran and which checks were performed. Keep previous findings only as long as useful and allow refresh/clear. If a check could not run because a tool is missing, report it as skipped rather than passed.

## 7. Privacy and security

Keep scans scoped to the selected project. Respect exclusions and avoid exposing secret values. Treat project files, scripts and diagnostic output as untrusted. Do not upload project contents to cloud AI unless the user has selected that context and understands the sharing.

## 8. Acceptance criteria

- Scan results show evidence, severity and confidence.
- Unsupported checks are marked unavailable or skipped.
- Suggested fixes include a preview and require appropriate approval.
- Project-defined scripts are never executed as silent diagnostics.
- Users can rerun and dismiss findings.
- A clean scan is not described as proof that the project is secure or bug-free.

## 9. Dependencies and open decisions

Integrates with Project Hub, Developer Tool Manager, System Monitor, Git Centre and AAP. Define a small reliable set of checks for Core and add language-specific diagnostics incrementally.

## 10. Related documentation

- [Project Hub](project-hub.md)
- [Developer Tool Manager](developer-tool-manager.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
