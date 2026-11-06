# Agent Git Permissions

**Release:** ATLAS Core  
**Status:** Planned

## Purpose

A user-controlled policy for whether AI agents may initiate remote Git pushes.

## Boundaries

- OFF by default.
- Enforce the policy centrally across terminal commands, Git integrations and workflows.
- Enabling agent-initiated pushes is not blanket approval; confirmation and operation-specific checks still apply.
- Force pushes and remote branch deletion remain separately restricted.
- The AI cannot change this setting or access repository credentials.

## Related documentation
- [Master specification](../../ATLAS_MASTER_SPEC.md)
- [Core vs Pro](../../CORE_VS_PRO.md)
