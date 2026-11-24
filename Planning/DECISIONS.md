# Project decisions and open questions

## Accepted decisions
| Date | Decision | Rationale |
|---|---|---|
| 2026-11-24 | Electron + React + TypeScript + Node.js | Predictable bundled Chromium rendering and productive desktop ecosystem |
| 2026-11-24 | Windows and Linux initial targets | Explicit initial platform scope |
| 2026-11-24 | Figma-first through January; February handoff | Resolve UX before implementation |
| 2026-11-24 | Core target mid-March 2027 | Current milestone |

## Open decisions
| Topic | Current position | Needed before |
|---|---|---|
| Open-source licence | Not selected | Signing application/public source release |
| Windows signing provider | Unknown; investigate SignPath and alternatives | Public Windows release |
| Windows packaging | NSIS EXE first direction; MSIX/Store later option | Packaging implementation |
| Linux formats | AppImage and DEB under consideration | Release packaging |
| Update mechanism | Not selected | Stable release |
| Minimum OS versions | Not selected | Platform validation |
| AI provider priority/fallback | Local-first preference; exact policy needed | AI implementation |
| Data persistence/migrations | Needs specification | Core implementation |
| Core voice scope | Feasibility/priority need validation | Scope freeze |

Record problem, options, evidence, choice, consequences and revisit conditions. Suggestions are not accepted decisions until explicitly chosen.
