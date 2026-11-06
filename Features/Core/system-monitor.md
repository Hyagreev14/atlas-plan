# System Monitor

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Runtime visibility

## 1. Purpose

System Monitor provides a lightweight view of system resources and development-related activity. It should help users understand what is running and identify resource pressure without becoming a full operating-system task manager.

## 2. Core information

Where supported, display CPU utilisation, memory use, storage information and GPU activity. Show the measurement time and explain that values may be sampled or unavailable on some platforms. Do not combine incompatible metrics into a misleading single score.

## 3. Development process view

Provide a focused list of processes and tasks that ATLAS can reliably associate with development work, such as registered project servers, build/test processes and workflows started through ATLAS. Include process name, associated project when known, start time and current state.

Do not assume every process using a common port belongs to a particular project. Port-to-process information should be labelled with its detection source.

## 4. Process controls

The initial experience should prioritise inspection. If process stop/termination controls are supported, show the exact process, project and impact before requesting confirmation. Never terminate a process merely because it consumes resources or appears unresponsive. Do not force-kill by default; offer graceful shutdown first where supported.

## 5. Alerts

Potential alerts include unusually high resource usage, a development server that exited, a port conflict or a long-running task. Alerts should be configurable, explain the evidence and avoid noisy thresholds. A notification is not proof of root cause.

## 6. History and charts

Short-lived local history may help show trends. Make retention and sampling behaviour clear. Avoid storing detailed process history indefinitely. Users should be able to clear the collected history.

## 7. Performance and platform support

Monitoring must be lightweight, avoid excessive polling and tolerate unavailable platform counters. Use platform-specific adapters and document limitations. WSL, containers and host processes should be distinguished rather than presented as one unified process space when the source cannot establish that relationship.

## 8. Privacy and security

Do not expose command-line arguments that may contain credentials. Redact sensitive environment values. Do not upload process lists or resource history to cloud providers without disclosure and consent.

## 9. Acceptance criteria

- Resource readings show units and last-updated time.
- Unsupported readings are shown as unavailable, not fabricated.
- Development tasks can be associated with projects only when evidence supports it.
- Any stop action names its target and requires appropriate approval.
- Monitoring can be paused or disabled.
- The feature remains useful when some OS metrics are unavailable.

## 10. Dependencies and open decisions

Integrates with Developer Home, Workflow Automation, Hardware Profiler and Activity Timeline. Define the minimal metrics and sampling interval for Core before implementation.

## 11. Related documentation

- [Hardware Profiler](hardware-profiler.md)
- [Developer Home](developer-home.md)
- [Workflow Automation](workflow-automation.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
