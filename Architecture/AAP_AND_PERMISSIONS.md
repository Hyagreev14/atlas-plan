# AAP and permission architecture

## Core invariant

**AI requests; ATLAS validates, authorises and executes.**

AAP is the structured protocol through which AI-assisted workflows request supported actions. It is not an authority system and must not let the model set policy.

## Conceptual pipeline

1. Receive a structured request.
2. Parse and validate it against a versioned schema.
3. Check supported action type and required fields.
4. Resolve paths, resources and user context safely.
5. Evaluate policy in trusted ATLAS code.
6. Ask the user for approval when policy requires it.
7. Execute through a narrow service capability.
8. Return a structured result and record the outcome.

## Non-negotiable rules

- No model-provided `requires_approval` or equivalent field may control the permission decision.
- The model cannot approve itself, change policy or grant permissions.
- Unknown actions and unknown schema versions fail closed.
- Destructive or externally visible actions receive clear user-facing descriptions.
- Denial and cancellation are normal outcomes, not errors to be bypassed.
- The permission layer applies equally to chat, voice, workflows and future visual context.
- Secrets are excluded from prompts and action logs.

## Design work

The exact AAP schema, action catalogue, permission tiers and approval UX remain separate design tasks. Record each schema change with compatibility and migration notes. Do not invent a large system prompt before the protocol and permission boundaries are stable.
