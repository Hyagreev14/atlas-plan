# IPC contract principles

## Purpose

Define a narrow, typed communication boundary between the React renderer and trusted Electron services. The final channel names and schemas should be version-controlled with the application source; this document records design rules before implementation.

## Contract requirements

- Use explicit domain methods such as `projects.list`, `projects.open` or `settings.get`, not arbitrary channel names supplied by the renderer.
- Validate payloads at runtime, even when TypeScript types exist.
- Validate the calling window/frame and reject unexpected senders.
- Return a discriminated result with success data or a safe error code/message.
- Keep long-running operations asynchronous and expose progress/cancellation through deliberate contracts.
- Do not pass executable code, arbitrary shell strings or raw filesystem access across IPC.
- Avoid sending secrets to the renderer unless a specific UI flow requires a short-lived display.

## Suggested response shape

Use a consistent typed result pattern in application code, for example a success branch with data and a failure branch with a stable error code and user-safe message. The exact TypeScript type belongs in the implementation repository.

## Review checklist

- Is this operation genuinely needed by the renderer?
- Is the method narrowly scoped?
- Is input validated and bounded?
- Is authorization enforced in trusted code?
- Can the request be abused through repeated calls?
- Are errors safe and actionable?
- Is sensitive data excluded from logs and unnecessary UI state?
