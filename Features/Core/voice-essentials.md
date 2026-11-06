# ATLAS Voice Essentials

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Voice interface and accessibility

## 1. Purpose

ATLAS Voice Essentials adds a natural spoken interface to the ATLAS development command centre. Users should be able to ask questions, discuss code, open projects and applications, and request supported development actions without typing every instruction.

**Architectural rule: Voice is another interface to ATLAS, not a separate assistant.** It shares the same AI providers, project context, AAP, Permission Manager, Secret Vault and execution services as Chat.

## 2. Core interaction model

Core should provide push-to-talk as a first-class mode. The user activates a keyboard shortcut or visible control, speaks, and releases or toggles the control to submit. The interface shows when it is listening, processing, speaking or idle.

Voice should support:
- Speech-to-text for user instructions.
- Spoken responses using text-to-speech.
- Text transcript review where useful.
- Interrupting spoken output.
- Clarification when speech recognition is uncertain.
- Configurable microphone, language, voice, speed and volume where supported.
- A clear mute/disable control.

Wake-word detection and continuous always-available listening are advanced capabilities and belong in Pro unless the release split is deliberately revised.

## 3. Developer assistance

Voice uses the same AI Workspace capabilities and active project context. Example intents include asking for an explanation, discussing an error, reviewing a selected file, requesting a code change, opening a project, launching an installed application or asking for a Git status summary.

Speech is an input method, not a command language. Users should be able to speak naturally. If a project, file, application or action target is ambiguous, ask a concise clarification rather than guessing.

## 4. Action execution

Voice-triggered file, terminal, application, workflow and Git actions must be represented through AAP and the same trusted execution path used by Chat. Speech recognition does not grant permission. A spoken instruction cannot bypass Tutor mode, Git policy, file boundaries or approval requirements.

For sensitive or potentially destructive operations, ATLAS should read back the understood target and action, then obtain the approval required by Permission Manager. A confirmation must apply only to the exact pending action ATLAS presented. If recognition is uncertain, ask again or cancel.

## 5. AI mode relationship

Voice mode defaults to **Same as ATLAS Chat**. In this state, Voice follows the effective Chat mode: Helper/Tutor, Developer or Hybrid. The user may choose an independent Voice override in Settings. Once overridden, changing Chat mode must not unexpectedly change Voice mode. Selecting Same as Chat restores inheritance.

Tutor restrictions are enforced by ATLAS, not the model prompt: no file modifications, creation/deletion or modifying environment actions while the effective mode is Tutor.

## 6. Voice safety and privacy

### Microphone state
Show a clear indicator whenever microphone capture is active. Distinguish idle, listening, processing and speaking. Provide an immediate mute/stop control. Never imply the microphone is off while audio is being captured.

### Push-to-talk
Push-to-talk should capture speech only during the user-initiated session. The user can configure a shortcut and should be able to use a visible button as an alternative.

### Read-back and confirmation
Repeat the important action details—such as project, file, command or Git target—before sensitive operations. Read-back supplements but never replaces Permission Manager approval.

### Speech processing location
Explain whether speech recognition and synthesis run locally or use an external service. Do not silently switch between local and cloud speech services. Offline recognition may be offered when a suitable engine is available, with clear model/resource requirements.

### Session history
Provide a reviewable voice session history where practical, distinguishing recognized transcript, AI response, requested action, approval and execution result. Raw microphone recordings must not be retained by default. Users should be able to clear transcript history.

## 7. Settings

Proposed location: **Settings → Voice**. Include enable/disable, push-to-talk shortcut, microphone selection, output voice, speech language, speed/volume, interruption behaviour, speech processing location and Voice AI mode. Settings must not silently enable wake-word detection or screenshot capture.

## 8. Core scope and exclusions

Core includes push-to-talk, speech recognition, spoken responses, basic conversation, shared project context, independent/inherited Voice mode setting, interruption and basic ATLAS actions through AAP.

Always-on wake-word detection, custom wake phrases, richer continuous conversations, advanced voice workflows and screen-aware interaction are Pro features. Screenshot analysis is specified separately in [Visual Context Mode](../Pro/visual-context-mode.md).

## 9. Failure handling

Handle unavailable microphones, denied OS permission, recognition errors, unsupported languages, speech-service failures and TTS failures. Keep a text input fallback available. Do not claim that a voice command was understood or executed if the service did not confirm it.

## 10. Acceptance criteria

- User can start and stop a push-to-talk session.
- Microphone state is always visible while capture is active.
- Spoken requests use the same project context and AI mode rules as Chat.
- Voice actions pass through AAP and Permission Manager.
- Tutor mode cannot perform modifying actions.
- Sensitive actions use exact-target read-back and required approval.
- Raw audio is not retained by default.
- Text interaction remains available when voice hardware/services fail.

## 11. Dependencies and open decisions

Depends on AI Workspace, AI Model Manager, AAP, Permission Manager, Secret Vault, Activity Timeline and OS audio APIs. Choose speech engines only after testing latency, supported languages, offline behaviour and hardware impact.

## 12. Related documentation

- [Advanced Voice](../Pro/advanced-voice.md)
- [Visual Context Mode](../Pro/visual-context-mode.md)
- [AI Workspace](ai-workspace.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Privacy and Offline Operation](privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
