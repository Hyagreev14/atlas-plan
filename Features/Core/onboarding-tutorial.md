# First-Run Tutorial

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Onboarding and discoverability

## 1. Purpose

The First-Run Tutorial introduces ATLAS to a new user through a short, interactive walkthrough. It should demonstrate the main areas of the product without overwhelming the user or requiring them to configure everything immediately.

The tutorial must remain available after onboarding and can be reopened from Settings.

## 2. Entry points and lifecycle

On first launch, ATLAS may offer the tutorial after essential setup. Users can start, skip, pause or exit it. Skipping must not block access to the application. Progress should be saved locally so the user can resume later.

Provide a permanent entry such as **Settings → Help → Reopen Introduction**. Users should also be able to restart the walkthrough from the beginning. Restarting tutorial progress must not reset application settings or delete project data.

## 3. Suggested walkthrough

A concise sequence may introduce:

1. ATLAS Home and navigation.
2. Adding an existing project to Project Hub.
3. Launching an installed application.
4. Finding developer tools and understanding installation consent.
5. Opening AI Workspace and selecting Helper/Tutor, Developer or Hybrid mode.
6. Choosing a provider/model and understanding local versus cloud processing.
7. Understanding AAP, approval prompts and the activity history.
8. Finding settings, privacy controls and help.

The sequence should be modular. Users may skip a section and revisit individual topics later.

## 4. Interactive demonstrations

Where possible, use a safe sample project or simulated example. Tutorial steps must not create, modify, delete, install, publish or execute real resources without a separate explicit user action. A demonstration should be clearly labelled as simulated if it does not perform the real operation.

If a tutorial step offers a real action, show its target and consequences and pass it through the same permission architecture as any other operation.

## 5. Adaptation

Avoid assuming the user has Git, Docker, Python, an IDE or a cloud AI key installed. Explain optional integrations and allow the tutorial to continue when they are unavailable. Tailor only to detected, verified capabilities and let the user skip irrelevant material.

## 6. Accessibility and localisation

Support keyboard navigation, clear progress, readable text and a way to exit at any time. Avoid relying only on colour or animation to communicate status. Keep instructional text concise and link to deeper feature documentation where appropriate.

## 7. Privacy

Tutorial completion state is local. Do not use onboarding as a reason to enable telemetry, cloud providers, microphone access, screenshot capture or automatic tool installation. Any optional feature must be configured separately with informed consent.

## 8. Acceptance criteria

- First launch offers an understandable introduction.
- Users can skip, pause and resume.
- Tutorial can be reopened and restarted from Settings.
- Restarting does not reset unrelated application data.
- Demonstrations do not execute actions without consent.
- Missing optional tools do not block completion.

## 9. Dependencies and open decisions

Depends on navigation, Settings and the first usable Core workflows. Finalise tutorial content after the main UI stabilises so the instructions match the actual product.

## 10. Related documentation

- [Developer Home](developer-home.md)
- [AI Workspace](ai-workspace.md)
- [Developer Tool Manager](developer-tool-manager.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
