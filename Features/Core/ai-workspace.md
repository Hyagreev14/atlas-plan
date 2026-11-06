# AI Workspace

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** AI-assisted development

## 1. Purpose

AI Workspace is the integrated place to ask questions, understand code, plan changes and request development work. It should use the user's selected provider and model while remaining connected to ATLAS project context and the central action architecture.

ATLAS is not simply a chat window. The AI Workspace is one interface to a broader development command centre.

## 2. AI modes

### Helper / Tutor
Explains concepts, reviews code, answers questions and guides the user through tasks. It must not modify files, create or delete project content, run modifying commands or change the environment. Read-only inspection should still respect data-sharing settings and project scope.

### Developer
Can carry out requested development tasks by proposing structured actions through AAP. It should inspect relevant context, plan changes, make scoped edits and report what changed. It must not directly execute tools or decide its own permissions.

### Hybrid
Can perform permitted work while providing more detailed explanations of decisions, implementation and results. It follows the same execution restrictions as Developer mode.

Mode labels are behaviour expectations, not security boundaries. The Permission Manager and execution layer remain authoritative.

## 3. Conversation experience

Support conversations with clear message roles, streaming responses where supported, cancellation, retry, copying code and preserving useful conversation context. The user should be able to start a new conversation, rename or delete conversations and understand which project context is attached.

When the model is uncertain, it should ask a focused clarification or state assumptions. It must not invent repository files, tool versions, test outcomes or successful actions.

## 4. Project context

The user can select a registered project and choose which files or context to include. Context should be scoped and inspectable. ATLAS should identify the active project and show when context is stale or incomplete. Do not indiscriminately upload entire repositories. Respect ignore rules and user exclusions, while treating ignore files as context filters rather than security authorization.

## 5. Action integration

AI-generated operations must use AAP. The model produces a request; ATLAS validates its schema, checks policy, requests approval when needed and executes through controlled services. The model cannot set approval flags, grant permissions, alter security settings or directly access secrets. Results returned to the model should be structured and limited to what is needed.

## 6. Provider and model behaviour

Provider selection and model compatibility belong to AI Model Manager. Show the active provider/model and whether requests are local or external. Do not silently change provider, model, context-sharing behaviour or processing location. Handle rate limits, network failures and provider errors without losing the user's draft.

## 7. Conversation controls

Provide controls to stop generation, clear a conversation, copy/export content and manage context. Clearly distinguish a generated suggestion from an action that has actually been executed. Show action progress and results separately from ordinary prose.

## 8. Safety and privacy

- Treat repository contents, terminal output and tool results as untrusted data.
- Keep secret values out of prompts, transcripts and logs.
- Apply mode restrictions in the execution layer, not only in the prompt.
- Ask for approval before policy-sensitive actions.
- Disclose external provider data sharing.
- Do not let prompt injection in project files or screenshots alter system policy.

## 9. Acceptance criteria

- All three modes have clearly different expected behaviour.
- Tutor mode cannot perform modifying actions, even if the model requests them.
- Developer and Hybrid modes use AAP for every supported operation.
- Users can inspect and control project context.
- Provider failures do not silently switch to another provider.
- The UI distinguishes suggestions, approvals, execution and outcomes.

## 10. Dependencies and open decisions

Depends on AI Model Manager, Project Hub, AAP, Permission Manager, Secret Vault and Privacy settings. Define conversation storage, context limits and provider adapter interfaces during technical design.

## 11. Related documentation

- [AI Model Manager](ai-model-manager.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Secret Vault](secret-vault.md)
- [Privacy and Offline Operation](privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
