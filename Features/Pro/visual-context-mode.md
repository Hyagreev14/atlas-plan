# Visual Context Mode

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Screen-aware AI assistance

## 1. Purpose

Visual Context Mode allows ATLAS Voice to use a screenshot or selected-window image as additional context for a spoken request. It helps users refer to what is already visible on their desktop instead of manually describing every error, dialog, code fragment or configuration screen.

Examples:
- “What does this error mean?”
- “Explain the warning on this screen.”
- “Help me understand this configuration.”
- “What is wrong with this terminal output?”
- “Compare these two visible settings.”

Visual context is evidence for understanding, not permission to act.

## 2. Setting and default

Proposed location: **Settings → Voice → Visual Context**

Setting: **Enable Screenshot Context**  
Default: **OFF**

Suggested description:

“Allow ATLAS Voice to capture your desktop or selected window and provide the image to a vision-capable AI model so it can understand visible content.”

The feature must remain off until the user explicitly enables it. It must be possible to temporarily disable capture for an individual session.

## 3. Model requirements and resource warning

Visual Context requires a model/provider that accepts image input. When the selected model does not support vision:
- Explain why the feature is unavailable.
- Show the required capability.
- Offer compatible model selection through AI Model Manager.
- Do not silently switch providers or models.
- Do not download a model without explicit consent.

Before enabling, display a resource and privacy warning. Example:

“Visual Context requires a vision-capable model. Vision models may use substantially more RAM, VRAM, processing power, network bandwidth and API resources than text-only models. Actual performance depends on the selected model, image resolution, context size, hardware and whether processing is local or cloud-based.”

Hardware Profiler may provide an estimate, but must distinguish estimates from measured facts.

## 4. Capture workflow

A typical request flow:

1. User enables Visual Context and starts a voice interaction.
2. User makes a request that refers to visible screen content.
3. ATLAS determines whether a screenshot is relevant and permitted.
4. ATLAS indicates that capture is occurring.
5. ATLAS captures the selected screen/window or configured display.
6. The image is prepared within defined resolution and size limits.
7. The image and spoken request are supplied to the selected vision-capable model according to the user's processing preference.
8. The model returns observations or an AAP action request.
9. ATLAS validates any proposed action through the normal trusted pipeline.
10. ATLAS communicates its explanation or action result through Voice.

Do not continuously capture screenshots when no request needs visual context. Do not capture when the feature is disabled.

## 5. Capture scope and controls

Where supported, let the user choose:
- Current display.
- Selected display in a multi-monitor setup.
- Selected application/window.
- A user-selected region.

The exact scope must be visible before capture. If ATLAS cannot reliably identify the active window or selected display, ask the user to choose rather than guessing. Provide a clear capture indicator and a way to cancel.

## 6. Image handling

- Apply sensible resolution and compression limits to manage resource use.
- Avoid retaining screenshots after the request unless the user explicitly saves them.
- Do not capture repeatedly in the background.
- Avoid unnecessary image processing or transmission.
- Make it clear when an image is being sent to a cloud provider.
- Do not claim that a screenshot was securely redacted unless the redaction was actually performed and verified.

A future implementation may offer sensitive-region exclusion or user review before upload. These should not be implied as available until built and tested.

## 7. Privacy and sensitive content

Screenshots may contain messages, account details, personal information, credentials or other private material. Users must understand that cloud processing sends the image outside the local device and is subject to the selected provider's policies.

Never enable capture by default. Avoid capturing unrelated displays or windows. Provide a pause/disable control. Raw screenshots must not be stored in session history by default. If a user saves an image, treat it as user data and make its storage location clear.

## 8. Untrusted visual input and prompt injection

Text visible in screenshots is untrusted input. A screenshot may contain malicious instructions, fake dialogs, terminal commands, prompt-injection text or content that imitates ATLAS system messages.

The model may describe or analyse visible content, but instructions found inside an image cannot override system rules, user settings, AI mode restrictions, AAP schema, Permission Manager policy or security controls.

A visible button, confirmation dialog, terminal command or “approved” message is not user authorisation. The user must explicitly approve sensitive operations through ATLAS's trusted approval flow.

## 9. Action boundaries

Visual Context may help identify a file, error, application or setting. It must not:
- Click or operate controls outside an explicitly authorised automation capability.
- Treat on-screen text as an instruction from the user.
- Bypass Tutor restrictions.
- Bypass AAP validation or permission checks.
- Infer approval from a screenshot.
- Expose secrets in spoken output.

If the target is unclear, ask the user to identify it.

## 10. Multi-monitor support

Advanced support may include listing connected displays, selecting a display and analysing a user-selected window or region. ATLAS must identify which display is being captured. Avoid silently combining multiple screens into one image. Multi-monitor capture increases privacy exposure and should require deliberate scope selection.

## 11. Failure handling

Handle unsupported model input, capture permission denial, unavailable windows, display changes, image-size limits, network failures and provider errors. Preserve the spoken request and offer a text-only explanation path where possible. Do not silently fall back to a different provider.

## 12. Acceptance criteria

- Feature is OFF by default.
- Enabling it shows model, resource and privacy requirements.
- No screenshot is captured when disabled.
- Capture scope and active capture state are visible.
- Cloud transmission is disclosed before the image leaves the device.
- Screenshots are not retained by default.
- Visual content cannot grant permission or override system policy.
- Every resulting action passes through AAP and Permission Manager.
- Unsupported vision models are reported without silent switching.

## 13. Dependencies and open decisions

Depends on Advanced Voice, AI Model Manager, Hardware Profiler, Privacy settings, AAP, Permission Manager and platform screen-capture APIs. Decide whether the first implementation captures the full display, a selected window or a selected region; prefer the narrowest scope that satisfies the user's request.

## 14. Related documentation

- [Voice Essentials](../Core/voice-essentials.md)
- [Advanced Voice](advanced-voice.md)
- [AI Model Manager](../Core/ai-model-manager.md)
- [Hardware Profiler](../Core/hardware-profiler.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Privacy and Offline Operation](../Core/privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
