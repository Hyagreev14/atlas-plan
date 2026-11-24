# ATLAS — Your Development Command Centre

A planned local-first desktop workspace for developers. This repository contains ATLAS product planning, UX/UI design, architecture, research, roadmap and quality documentation—not the application source.

## Current direction
- **Stack:** Electron + React + TypeScript + Node.js.
- **Initial platforms:** Windows and Linux.
- **Design:** Figma-first through January 2027; implementation handoff in February.
- **Core target:** mid-March 2027.
- **Pro development:** late March 2027 onward.
- **Distribution:** ready-to-install GitHub Releases; Windows signing remains unresolved.

Dates are targets, not guarantees. Planned features are not implemented features.

## Repository structure

| Directory | Purpose |
|---|---|
| [Design/](Design/README.md) | Figma workflow, design system, screens, components, prototypes and handoff |
| [Architecture/](Architecture/README.md) | Electron architecture, IPC, security, AAP and decision records |
| [Product/](Product/README.md) | Product principles, Core scope and user journeys |
| [Research/](Research/README.md) | Reference-app reviews and research log |
| [Planning/](Planning/README.md) | Roadmap, decisions and risk register |
| [Quality/](Quality/README.md) | Testing, accessibility and usability |
| [Features/](Features/) | Detailed Core and Pro feature specifications |

## Start here
1. [Product overview](Product/README.md)
2. [Master specification](ATLAS_MASTER_SPEC.md)
3. [Core vs Pro](CORE_VS_PRO.md)
4. [Figma-first workflow](Design/FIGMA_WORKFLOW.md)
5. [Architecture overview](Architecture/README.md)
6. [Roadmap](Planning/ROADMAP.md)
7. [Release and signing plan](RELEASE_AND_SIGNING.md)

## Design period
Figma is the visual and interaction specification during planning. The canonical file should contain foundations, reusable components, screen layouts, clickable journeys and documented states. In February, approved designs are handed to React + TypeScript implementation. A Figma prototype simulates interactions; it does not prove backend or platform behaviour.

## Status vocabulary
- **Proposed:** under consideration.
- **Planned:** accepted intent, not implemented.
- **In design:** being specified.
- **In progress:** implementation has started.
- **Implemented:** code exists; testing may remain.
- **Tested:** stated checks passed on a named platform/build.
- **Deferred / rejected:** deliberately postponed or not adopted.

Keep Core and Pro separate. Core must be useful independently. Security, privacy, user consent and honest release communication are non-negotiable.
