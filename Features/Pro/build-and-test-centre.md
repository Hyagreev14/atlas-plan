# Build & Test Centre

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Build and validation workflows

## 1. Purpose

Build & Test Centre provides a project-aware place to discover, configure and run build, test, lint and related validation workflows. It should make the result and its evidence easy to understand without hiding the underlying command or tool.

## 2. Discovery

Detect likely build/test systems from recognised project manifests and configuration files. Examples may include language-specific test runners, build tools, package scripts and compiler tasks. Detection must be labelled as a suggestion until confirmed by the user.

Do not run discovered scripts automatically. Project scripts can execute arbitrary code.

## 3. Task configuration

A configured task should include name, task type, executable/command definition, arguments, working directory, environment reference, timeout and expected output. Prefer structured executable and argument arrays over arbitrary shell strings. If shell mode is necessary, identify it clearly and apply stricter validation.

## 4. Execution experience

Before running a task, show the command or task definition, project, working directory and any relevant environment profile. Provide start, progress, output, cancellation and final status. Preserve logs for inspection with secret redaction. A task that starts but exits unsuccessfully is not a successful build.

## 5. Results

Show:
- Exit status and duration.
- Build/test task identity.
- Passed, failed, skipped or unavailable tests when the runner reports them.
- Failure summaries and links to relevant output.
- Compiler or test diagnostics when they can be parsed reliably.
- Artifacts produced, where known.

Do not invent test counts, coverage or failure causes. Coverage should only be shown when a supported tool provides it.

## 6. AI assistance

AI may explain errors, summarise logs or suggest fixes. It must receive only the context required and must treat output as untrusted. Any suggested file edit or rerun goes through AAP and Permission Manager. Do not automatically modify code and rerun repeatedly without user visibility.

## 7. Reproducibility

Save named task configurations and record the relevant project/environment references. Show when a task definition changes. Where feasible, include tool version and environment details in run metadata so results can be reproduced.

## 8. Safety and resource controls

Builds and tests may consume substantial CPU, memory, storage and network. Show running state, allow cancellation and set sensible timeouts. Do not run tasks on project open by default. Avoid concurrent duplicate runs unless the user explicitly requests them.

## 9. Acceptance criteria

- Detected tasks are presented as suggestions, not silently executed.
- Users can create and edit task definitions.
- Commands, working directory and environment are visible before execution.
- Results distinguish pass, fail, skipped and cancelled.
- Logs are inspectable and secrets are redacted.
- AI fixes and reruns remain user-controlled and permission-checked.

## 10. Dependencies and open decisions

Depends on Project Hub, Developer Tool Manager, Environment Profiles, AAP, Activity Timeline and System Monitor. Define the first supported task runners and result parsers incrementally.

## 11. Related documentation

- [Project Hub](../Core/project-hub.md)
- [Environment Profiles](environment-profiles.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Dependency Security Centre](dependency-security-centre.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
