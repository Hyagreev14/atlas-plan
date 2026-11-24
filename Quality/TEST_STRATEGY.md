# ATLAS test strategy

## Test layers
- **Unit:** domain logic, schema validation, permission policy, path handling and provider adapters.
- **Integration:** service interactions, persistence, IPC validation and platform adapters.
- **End-to-end:** first launch, project registration/opening, tool launch request, AI action proposal, permission denial/approval and settings.
- **Platform smoke:** Windows/Linux launch, window behaviour, filesystem, process launching, Git, packaging and uninstall.

## Security-focused tests
Reject malformed/unknown IPC and unexpected senders; prevent path traversal and unsafe links; validate command arguments; prove AI cannot approve actions or change policy; prove denied/cancelled actions do not execute; verify secrets do not leak into prompts, renderer state or logs.

## Performance
Measure full ATLAS process tree at cold start, settled idle after five minutes and representative active workloads. Record machine, OS, version and method. Separate ATLAS from independently launched IDEs, Docker and model runtimes.

## Release evidence
Record build revision, test environment, checks run, known failures, installer verification and checksums. A test not run must not be reported as passed.
