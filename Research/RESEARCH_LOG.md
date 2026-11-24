# ATLAS research log

Use newest entries first. Keep observations factual and concise; link detailed evaluations where useful.

## 2026-11-24 — Figma-first design decision

**Decision:** Use Figma as the primary interface design and prototyping tool during planning through January 2027. Prepare implementation handoff in February.

**Why:** It allows the visual system, screens, reusable components and user flows to be explored before the React/Electron implementation begins.

**Boundary:** Figma prototypes simulate interaction. They do not prove filesystem, process, AI, permission or platform behaviour.

## 2026-11-24 — DevAtlas launch blocked by SmartScreen

**Observation:** The DevAtlas release the project attempted to launch was unsigned and Windows SmartScreen blocked/warned about it. The application was not treated as a successfully tested reference.

**ATLAS implications:**
- First-launch trust is part of product distribution quality.
- Do not ask users to bypass security warnings as a normal installation path.
- Investigate signing and publisher identity before the Core release.
- If an unsigned build must be published, disclose that clearly and provide verifiable source and checksums.
- Continue reference research using official documentation, screenshots and other safe materials.

**Status:** Research observation; no signing provider selected. See [release and signing plan](../RELEASE_AND_SIGNING.md).

## Entry template

### YYYY-MM-DD — Topic
- **Context/platform/version:**
- **Direct observations:**
- **Interpretation:**
- **Potential ATLAS requirement:**
- **Open questions:**
- **Evidence/links:**
- **Follow-up:**
