# Advanced Voice

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Advanced voice interaction

## 1. Purpose

Advanced Voice extends the push-to-talk voice foundation in ATLAS Core with hands-free activation, richer conversation continuity and advanced spoken development workflows. It must extend the same ATLAS Voice pipeline rather than introduce a second assistant or a separate permission system.

## 2. Core dependency

This feature requires [ATLAS Voice Essentials](../Core/voice-essentials.md). Core must remain useful without wake-word detection or continuous listening. Advanced Voice adds optional interaction modes; it must not make microphone access mandatory for using ATLAS.

## 3. Wake-word detection

Potential capabilities:
- Enable or disable wake-word detection.
- Default phrase: **“Hey Atlas”**.
- Optional custom wake phrase where technically supported.
- Clear indication of the wake-word listening state.
- Configurable sensitivity or activation behaviour where supported.
- A visible and immediate way to disable listening.
- Push-to-talk remains available as an alternative.

Wake-word detection should preferably use a local lightweight detector when practical. If any audio is transmitted externally, ATLAS must clearly disclose this before activation. Do not claim that wake-word processing is fully local unless the actual implementation supports it.

## 4. Continuous conversations

After activation, allow a configurable conversation window so the user can continue speaking without repeating the wake phrase for every turn. The UI must show when the conversation is active and when ATLAS returns to idle.

Provide controls for session timeout, end conversation, mute and interrupt. Continuous conversation must not become indefinite recording. A session should end predictably after inactivity or explicit user action.

## 5. Speech and response quality

Pro may add more speech engines, voice options, language choices, pronunciation handling and response controls. Show which features are supported by the selected speech provider. Do not imply that a voice model or language is available if it is not installed or configured.

Users should be able to interrupt spoken output immediately. The transcript should remain available if speech playback is stopped. TTS failure should not prevent the user from reading the response.

## 6. Advanced developer workflows

Advanced Voice may support longer spoken task sequences, multi-step project operations and richer context handoff. Example requests include asking ATLAS to open a project, inspect a visible issue, explain it, propose a fix and then carry out the approved change.

Complex requests must be decomposed into explicit actions. ATLAS should summarise the intended sequence and ask clarifying questions when targets or scope are unclear. It must not treat one broad spoken request as blanket approval for every future step.

## 7. Sensitive action confirmation

Use read-back for consequential actions. The spoken confirmation must identify the exact pending operation and relevant target. A confirmation token or response must be bound to that pending action, expire appropriately and be invalidated if its parameters change.

Permission Manager remains authoritative. Wake-word activation, familiar voice, speaker recognition or a prior approval must never grant permissions by themselves. Git pushes remain subject to Agent Git Permissions and separate per-operation policy.

## 8. Settings

Proposed settings under **Settings → Voice → Advanced**:
- Wake-word detection on/off.
- Wake phrase and custom phrase where supported.
- Continuous conversation on/off.
- Conversation inactivity timeout.
- Speech engine and language.
- Voice output selection and speaking style.
- Interrupt behaviour.
- Local/cloud processing preference.
- Startup behaviour, default OFF for automatic microphone listening.
- Microphone indicator and privacy controls.

Each setting must describe its effect. Do not silently turn on wake-word detection after an update.

## 9. Privacy, security and reliability

- Provide a persistent, accurate microphone-state indicator.
- Offer an immediate mute/disable action.
- Disclose local versus cloud audio processing.
- Avoid retaining raw audio by default.
- Keep session transcripts under user-controlled retention.
- Ask again when speech recognition confidence is low.
- Distinguish background noise or ambiguous audio from an intentional command.
- Do not allow audio played by the computer to trigger privileged actions without a deliberate confirmation path.
- Keep Voice activity in Activity Timeline without storing unnecessary audio.

## 10. Resource impact

Show expected resource implications of local speech models and wake-word processing when reliable data is available. Local speech recognition may consume CPU/RAM; cloud services may add latency and usage costs. Do not silently download speech models or change processing location.

## 11. Acceptance criteria

- Wake-word detection is optional and can be disabled immediately.
- Push-to-talk remains available.
- Continuous sessions have visible state and predictable timeout.
- Users can interrupt speech and end a session.
- Sensitive actions require exact read-back and Permission Manager approval.
- Voice features never bypass Tutor mode, AAP or Git restrictions.
- Audio retention is opt-in rather than default.
- Failure of advanced voice features does not break Core text or push-to-talk interaction.

## 12. Dependencies and open decisions

Depends on Voice Essentials, AI Workspace, AI Model Manager, AAP, Permission Manager, Activity Timeline and platform audio services. Evaluate wake-word accuracy, false activations, offline operation and supported languages before choosing an implementation.

## 13. Related documentation

- [Voice Essentials](../Core/voice-essentials.md)
- [Visual Context Mode](visual-context-mode.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Privacy and Offline Operation](../Core/privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
