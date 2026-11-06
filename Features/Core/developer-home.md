# Developer Home

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Navigation and daily workspace

## 1. Purpose

Developer Home is the default landing page and daily starting point for ATLAS. It should give the user a useful overview of their development workspace and provide fast access to the projects, tools and activities they are likely to need next. It is a command centre, not a replacement for a full project-management application.

## 2. User problems

- Development work is spread across IDEs, terminals, repositories and utility applications.
- Users repeatedly navigate to the same projects and tools.
- It can be difficult to remember which development servers or tasks are still running.
- Important project warnings and recent activity are easy to overlook.

## 3. Main experience

The home page should be composed of clear, independently configurable sections. The initial layout should favour useful information and quick actions over decorative statistics.

### Suggested sections

- **Pinned projects:** user-selected projects with name, path, detected project type and last-opened information.
- **Recent projects:** recently opened projects, with a way to clear or disable recent history.
- **Quick launch:** favourite applications, IDEs, terminals and saved launch groups.
- **Recent activity:** concise links to recent ATLAS actions, Git activity and workflow outcomes.
- **Running development tasks:** known servers, terminals or workflows started or registered through ATLAS.
- **Project health:** selected warnings from Project Doctor, with severity and a route to inspect details.
- **Quick actions:** create/open a project, open a terminal, search tools or start a saved workflow.
- **Getting started:** onboarding progress or helpful links for a new installation; dismissible after setup.

Not every section must be visible. Users should be able to hide, reorder or restore supported sections.

## 4. Interactions

- Selecting a project opens its project workspace or configured default action.
- Context menus provide actions relevant to the selected item.
- Search should find projects, applications and available actions without forcing the user to navigate several pages.
- Empty states should explain how to add or discover the first project/tool.
- Failed actions should show a useful reason and a retry path rather than silently doing nothing.
- Dashboard refresh should be lightweight; expensive scans must be user-triggered or clearly indicated.

## 5. Personalisation and settings

Provide controls for pinned items, visible sections, section order, recent-item behaviour and the default landing page. Preferences should persist locally. A reset-to-default option should restore the standard layout without deleting projects or application data.

## 6. Data and integrations

Use Project Hub as the source of registered project information, Universal App Launcher for launchable applications, System Monitor for supported process information, Git Centre for repository summaries, and Activity Timeline for recorded events. Avoid maintaining competing copies of the same data.

## 7. Privacy and performance

- Recent history must be clearable and optionally disabled.
- Do not display secret values, environment variable values or credential contents.
- Do not continuously scan the whole disk just to populate the dashboard.
- Load secondary sections lazily where practical.
- Show when information is stale or unavailable instead of presenting old values as current.

## 8. Acceptance criteria

- A user can reach a pinned project or favourite application from the home page.
- Sections can be hidden and restored.
- Recent items can be cleared or disabled.
- The page remains useful when optional integrations are unavailable.
- Loading or failing one section does not make the entire home page unusable.
- No destructive operation is triggered by merely opening or refreshing the dashboard.

## 9. Dependencies and open decisions

Depends on Project Hub, Universal App Launcher and Activity Timeline. Decide later which sections ship in the first Core iteration and which are deferred. Avoid committing to exact dashboard widgets before testing a usable layout.

## 10. Related documentation

- [Project Hub](project-hub.md)
- [Universal App Launcher](universal-app-launcher.md)
- [System Monitor](system-monitor.md)
- [Activity Timeline](activity-timeline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
