# ATLAS project risk register

| Risk | Impact | Mitigation | Status |
|---|---|---|---|
| Windows installer unsigned | SmartScreen friction and reduced trust | Research signing early; ask Hack Club; disclose status | Open |
| SignPath eligibility uncertain | Signing route unavailable | Verify current criteria/licence; keep alternatives | Open |
| Core scope grows | Mid-March target slips | Prioritise vertical workflows; defer breadth | Open |
| Electron resource use high | Poor experience on modest hardware | Lazy-load and measure whole process tree | Monitor |
| IPC boundary too broad | Security exposure | Narrow preload API, runtime validation, tests | Requirement |
| AI controls permissions | Unsafe actions | Trusted permission policy; denial/bypass tests | Requirement |
| Windows/Linux divergence | Inconsistent behaviour | Platform adapters and separate testing | Open |
| Prototype overstates behaviour | Misleading expectations | Label simulations and backend dependencies | Open |
| Limited development time | Milestone slip | Treat dates as targets; cut scope transparently | Monitor |

Review at milestones. Add likelihood, severity, owner and due date when implementation planning begins.
