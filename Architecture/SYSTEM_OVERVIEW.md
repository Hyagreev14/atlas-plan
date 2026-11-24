# ATLAS system overview

## Logical layers

### Renderer
React + TypeScript UI: app shell, screens, components, local presentation state and user interaction. It receives only the data and commands explicitly exposed through the preload bridge.

### Preload bridge
A small, typed and reviewed API surface. It translates renderer requests into narrow IPC messages. It must not expose raw `ipcRenderer`, filesystem APIs, arbitrary process execution or generic unrestricted channels.

### Electron main process
Owns the desktop lifecycle, window management, IPC registration, capability checks and orchestration of trusted services. Keep startup work small and defer optional services.

### Application services
Separate modules for projects, application discovery/launch, Git, settings, secret storage, system information, workflows, AI provider adapters and activity records. Each service validates inputs and reports typed outcomes.

### Permission and action layer
Receives structured requests, validates schema and context, checks policy independently of AI output, obtains user approval when required, executes through allowlisted capabilities and records outcomes.

### Platform adapters
Encapsulate Windows- and Linux-specific process, path, shell, credential-store and packaging differences. Avoid leaking platform-specific assumptions throughout feature code.

## Data flow

1. User interacts with the renderer.
2. Renderer calls a specific typed preload method.
3. Preload sends a narrow IPC request.
4. Main process validates sender, payload and capability.
5. Service applies domain validation and permission checks.
6. Operation executes using least privilege.
7. Result is returned as a typed response.
8. UI displays outcome and, where appropriate, activity history records it.

## Performance approach

Measure the full ATLAS process tree rather than one process. Record cold start, idle after a settling period and representative active workloads. Load optional AI, voice, monitoring and integrations only when needed. Distinguish ATLAS memory from separately launched applications such as IDEs, Docker or local models.

## Reliability

Services should return structured errors, support cancellation where practical and avoid leaving partial state after failed operations. Long-running work should expose progress and a safe cancellation path. Do not block the renderer with synchronous work.
