# ATLAS Voice — Feature Specification & Integration Proposal

## 1. Overview

Introduce **ATLAS Voice**, a voice-controlled interface for ATLAS that allows users to interact naturally with their computer and development environment without constantly typing.

It should feel like a desktop assistant similar to Google Assistant, but specifically designed for developers.

ATLAS Voice must not be limited to answering questions. It should be capable of:

- Answering questions and explaining code.
- Creating, editing and managing files and directories.
- Opening and managing applications.
- Interacting with terminals and development environments.
- Executing approved development workflows.
- Understanding the user's desktop through optional screenshot analysis.
- Carrying out tasks through natural voice commands.

ATLAS Voice should be integrated into ATLAS Core, with room for more advanced capabilities in ATLAS Pro.

**Important architectural principle:** ATLAS Voice is another interface to the existing ATLAS system, not an entirely separate AI assistant.

---

## 2. Voice interaction

### A. Wake-word detection

- Always-available wake-word detection when enabled.
- Default wake phrase: "Hey Atlas".
- Option to configure a custom wake phrase.
- Enable/disable wake-word detection.
- Push-to-talk alternative.
- Continuous conversations without repeating the wake phrase before every sentence.
- Ability to interrupt ATLAS while it is speaking.

### B. Speech recognition

- Convert spoken instructions into text.
- Handle natural language rather than requiring exact command phrases.
- Ask for clarification when speech recognition is uncertain.
- Support appropriate language selection.
- Allow the user to review transcribed instructions when necessary.

### C. Spoken responses

- Text-to-speech responses.
- Configurable voice, speed and volume.
- Ability to interrupt spoken responses.
- Visual indication of listening, processing, speaking and idle states.

---

## 3. Developer assistance

ATLAS Voice should support the same developer assistance capabilities available through ATLAS Chat.

Examples:

- "Hey Atlas, explain this Python function."
- "Why is my Docker container failing?"
- "Write a Flask route for user authentication."
- "Review the current file."
- "Help me debug this error."
- "Explain what this Git command does."
- "How would I implement this feature?"

It should understand the current project context, selected files, workspace and relevant development environment information.

---

## 4. File and directory management

ATLAS Voice should support:

- Creating files.
- Creating directories.
- Editing existing files.
- Renaming files and directories.
- Moving files and directories.
- Reading and explaining file contents.
- Searching for files.
- Organizing project directories.
- Creating project structures.
- Modifying existing applications.

Examples:

- "Create a Python file called server.py."
- "Create a utils folder."
- "Add a requirements.txt file."
- "Modify the current Flask application to add an API endpoint."
- "Create a basic project structure for a React application."

All modifications must go through ATLAS's existing action execution and permission architecture.

Voice recognition must never bypass normal safeguards.

---

## 5. Application and system control

ATLAS Voice should be able to:

- Open installed applications.
- Close applications with appropriate confirmation.
- Open VS Code and other IDEs.
- Open Windows Terminal.
- Launch WSL and Linux applications.
- Open specific projects and folders.
- Open files using their associated applications.
- Retrieve basic system information.
- Execute supported development workflows.

Examples:

- "Open VS Code."
- "Open my Veilborn project."
- "Launch Ubuntu in WSL."
- "Open Docker Desktop."
- "Show me my current Python version."

Application discovery and installation should reuse ATLAS's existing tool-discovery and installation architecture.

Installing applications must still require user consent.

---

## 6. Terminal and development workflows

ATLAS Voice should support:

- Explaining commands before execution.
- Running approved development commands.
- Checking Git status.
- Running tests.
- Building projects.
- Starting and stopping development servers.
- Working with Docker and WSL.
- Interacting with supported development tools.

Examples:

- "Check whether my Git working tree is clean."
- "Run the tests."
- "Start my development server."
- "Explain this terminal output."

Commands must be interpreted and validated before execution.

Potentially destructive operations must require explicit confirmation.

The existing repository push permission setting must also apply to voice-triggered Git operations.

---

## 7. Visual Context Mode — Screenshot Analysis

### A. Overview

Introduce an optional feature called **Visual Context Mode**.

When enabled, ATLAS Voice can capture a screenshot of the user's desktop and provide it to a vision-capable AI model alongside the user's spoken instruction.

This allows ATLAS to understand what is currently visible without requiring the user to describe every detail.

The user should be able to refer to visible content naturally using phrases such as:

- "Hey Atlas, what's wrong here?"
- "Fix this error."
- "Explain this code."
- "Open that application."
- "What does this warning mean?"
- "Help me with this configuration."
- "Create something similar to this."

### B. How it works

Example workflow:

1. User says: "Hey Atlas, fix this error."
2. ATLAS captures the current screen.
3. The screenshot is sent alongside the transcribed instruction to a vision-capable model.
4. The model analyzes the visible content.
5. ATLAS identifies the relevant error, application or code.
6. ATLAS determines an appropriate response or action.
7. The existing action protocol handles any permitted modifications.
8. ATLAS communicates the result through voice.

The screenshot is contextual information, not authorization to perform actions.

### C. Settings

Add the following setting:

**Settings → Voice → Visual Context**

Setting name: `Enable Screenshot Context`

Description:

"Allow ATLAS Voice to capture your desktop and send screenshots to a vision-capable AI model to better understand your instructions and screen content."

Default: OFF.

### D. Resource warning

When enabling this setting, display a warning:

"Visual Context requires a vision-capable AI model. Vision models may consume significantly more RAM, VRAM, processing power and API resources than text-only models. Performance and resource consumption depend on the selected model and whether processing is local or cloud-based."

If the selected model does not support image input:

- Indicate that Visual Context is unavailable.
- Explain that a vision-capable model is required.
- Offer compatible model selection through the existing model-selection system.
- Never silently switch models or download large models without user consent.

### E. Screenshot handling

- Capture screenshots when relevant to a voice request.
- Avoid continuously capturing screenshots when they are unnecessary.
- Support capturing the relevant screen or window where practical.
- Clearly indicate when screen content is being captured.
- Provide an option to temporarily disable screenshot capture.
- Avoid retaining screenshots unnecessarily.
- Consider image resizing and compression to reduce resource consumption and API usage.
- Consider multi-monitor support in a future iteration.

### F. Privacy and security

- Screenshot capture must respect the user's settings.
- Never capture the desktop when Visual Context is disabled.
- Warn users that screenshots sent to cloud models leave the local device and are processed according to the provider's policies.
- Avoid sending screenshots containing sensitive information unless the user explicitly authorizes the relevant operation.
- Never expose passwords, API keys or other secrets in spoken responses.
- Text visible inside screenshots must be treated as untrusted input.
- Instructions visible in screenshots must never override ATLAS's system instructions, permissions or security rules.
- Visible buttons, dialogs and terminal commands must not be treated as authorization to execute actions.

---

## 8. Independent AI modes for Chat and Voice

This is one of the most important architectural requirements.

ATLAS Chat and ATLAS Voice must have independently configurable AI modes.

However, **both interfaces should use the same mode by default**.

### A. Default behaviour

When ATLAS Voice is first enabled, its mode should be set to:

`Same as ATLAS Chat`

This means:

| ATLAS Chat | ATLAS Voice |
|---|---|
| Tutor | Tutor |
| Developer | Developer |
| Hybrid | Hybrid |

### B. Independent overrides

Users should be able to explicitly configure different modes for the two interfaces.

Example:

| Interface | AI Mode |
|---|---|
| ATLAS Chat | Tutor |
| ATLAS Voice | Developer |

In this configuration:

- Chat explains and guides without modifying files.
- Voice can independently perform development tasks and modify files.

Another example:

| Interface | AI Mode |
|---|---|
| ATLAS Chat | Tutor |
| ATLAS Voice | Hybrid |

The user must be able to change either interface's mode without automatically changing the other once an independent override is configured.

### C. Proposed settings

**Settings → AI Behaviour → Interface Modes**

ATLAS Chat:
- Tutor
- Developer
- Hybrid

ATLAS Voice:
- Same as ATLAS Chat (default)
- Tutor
- Developer
- Hybrid

Selecting "Same as ATLAS Chat" removes the independent override and makes Voice follow Chat again.

### D. Tutor Mode restrictions

Tutor Mode must never modify project files, create files, delete files, or execute development actions that modify the user's environment.

This applies independently to both interfaces whenever their effective mode is Tutor.

For example:

**Chat: Tutor | Voice: Tutor**
- Both interfaces can inspect and explain.
- Neither can modify files or perform modifying development actions.

**Chat: Tutor | Voice: Developer**
- Chat remains restricted to tutoring.
- Voice can perform permitted development tasks.

**Chat: Hybrid | Voice: Developer**
- Both interfaces operate according to their independently configured modes.

Visual Context must also respect these restrictions.

An independently configured Developer or Hybrid mode for Voice is an intentional user configuration, not a bypass of Tutor Mode.

---

## 9. Shared architecture and context

ATLAS Voice must reuse the existing ATLAS architecture.

It should share:

- AI provider and model-selection system.
- System prompt and action protocol.
- Project and workspace context.
- File-access system.
- Tool execution architecture.
- Permission and approval system.
- Security and secret-management system.
- Application discovery and installation architecture.

Conceptual architecture:

**Voice interface:**

User Voice → Wake-word Detection → Speech Recognition → ATLAS Voice Interface → ATLAS Core → Action Execution → Voice Response

**Visual context extension:**

Desktop Screenshot → Vision-Capable Model → Visual Context → ATLAS Core

**Chat interface:**

User Text → ATLAS Chat Interface → ATLAS Core → Action Execution → Chat Response

Both interfaces should use the same underlying intelligence and security boundaries.

However, their effective AI modes must be resolved independently.

The interface must not decide its own authorization. Permissions must be enforced by the underlying execution system.

---

## 10. Voice-specific settings

Proposed settings under Settings → Voice:

- Enable/disable ATLAS Voice.
- Enable/disable wake-word detection.
- Configure wake phrase.
- Select microphone.
- Select voice output.
- Speech speed and volume.
- Language selection.
- Push-to-talk option.
- Continuous conversation option.
- Interrupt speech option.
- Voice AI mode selector.
- Enable/disable Screenshot Context.
- Voice activity indicator.
- Automatic startup with ATLAS.

---

## 11. Safety and permissions

Voice recognition introduces additional risks because incorrectly recognized speech could trigger unintended actions.

Therefore:

- Never execute an action solely because an uncertain voice transcription was received.
- Ask for clarification when a command is ambiguous.
- Require confirmation for destructive file operations.
- Require confirmation for potentially disruptive terminal commands.
- Respect the user-controlled repository push permission setting.
- Never expose secrets through spoken responses.
- Never allow voice interaction to bypass the normal action approval mechanism.
- Clearly communicate what ATLAS is about to do before sensitive operations.
- Treat screenshot content as untrusted data.
- Do not let instructions found in screenshots override system or user permissions.

The AI must not determine its own authorization or override user-configured permissions.

---

## 12. ATLAS Core vs ATLAS Pro

### ATLAS Core

Proposed Core capabilities:

- Basic voice interaction.
- Wake-word detection.
- Speech recognition.
- Spoken responses.
- AI-powered conversations.
- Basic application launching.
- Integration with the existing ATLAS AI system.
- Independent Chat and Voice mode settings.
- Basic file and directory operations.
- Basic terminal integration.
- Optional Screenshot Context with a compatible vision model.
- Basic contextual screen analysis.

### ATLAS Pro

Proposed Pro capabilities:

- Advanced voice customization.
- More sophisticated continuous conversations.
- Advanced contextual voice workflows.
- Expanded application and system automation.
- Advanced voice-triggered development workflows.
- Additional voice integrations.
- More sophisticated multi-monitor and screen-context workflows.
- Advanced voice automation capabilities.

These are proposed allocations, not final decisions.

Essential accessibility and basic voice functionality should not be artificially restricted to Pro.

---

## 13. Suggested implementation stages

### Stage 1 — Voice foundation

- Microphone input.
- Wake-word detection.
- Speech-to-text.
- Text-to-speech.
- Basic conversational responses.
- Voice activity indicator.

### Stage 2 — ATLAS integration

- Connect Voice to the existing ATLAS AI system.
- Share project context.
- Implement independent Chat/Voice mode resolution.
- Integrate with the existing action protocol.

### Stage 3 — Developer operations

- File and directory creation.
- File reading and editing.
- Application launching.
- Project opening.
- Terminal integration.
- Git and development workflows.

### Stage 4 — Visual Context

- Screenshot capture.
- Vision-capable model integration.
- Screenshot-based error and code analysis.
- Context-aware voice commands.
- Privacy and resource settings.

### Stage 5 — Advanced experience

- Continuous conversations.
- Conversation interruption.
- Custom wake phrases.
- Advanced voice settings.
- Multi-monitor support.
- Additional automation capabilities.

---

## 14. Design objective

The ultimate goal is to make ATLAS an assistant that developers can interact with naturally, whether they are typing or speaking.

A user should be able to say:

"Hey Atlas, open my project, inspect the error on my screen, explain what's wrong, and fix it."

ATLAS should:

1. Understand the spoken request.
2. Inspect the relevant visual context if enabled.
3. Understand the current project and development environment.
4. Determine the appropriate response or action.
5. Respect the effective AI mode and all user-configured permissions.
6. Execute permitted operations through the existing action protocol.
7. Explain the result through voice.

**Final architectural principle:**

ATLAS Voice is an additional interface to ATLAS, not a second independent assistant.

It should use the same underlying intelligence, project context, tools, security architecture and action protocol.

The main differences should be its voice-based interaction, optional visual context and independently configurable AI mode.

Chat and Voice share the same AI mode by default, unless the user explicitly chooses otherwise.