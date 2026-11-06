# Project Templates

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Project creation

## 1. Purpose

Project Templates lets users create a new project from a built-in or user-created starting structure. It should make repeatable setup easier while showing exactly what will be created and avoiding hidden installation or script execution.

## 2. Template catalogue

A template may define:
- Template name, description and category.
- Supported languages/frameworks and prerequisites.
- A directory/file structure.
- Text-file contents with clearly defined variables.
- Optional setup instructions.
- Optional post-creation commands, disabled until explicitly reviewed.
- Template version and source.

Initial built-in templates should be small and understandable. User-created templates should be supported through a documented format where feasible.

## 3. Creation flow

1. User chooses a template.
2. ATLAS displays its description, requirements and source.
3. User chooses destination and project name.
4. ATLAS resolves template variables and previews the resulting tree.
5. ATLAS checks whether the destination exists and whether files would be overwritten.
6. User confirms creation.
7. ATLAS writes the approved files.
8. ATLAS reports created files and any failures.
9. User may optionally register the new directory in Project Hub.

Do not overwrite a non-empty directory by default. If merge/overwrite support is added, show exact affected files and require a separate approval.

## 4. Setup commands and dependencies

Creating template files must be separate from installing tools or running setup commands. A template may recommend dependencies, but installation requires Developer Tool Manager and explicit user consent. Scripts and post-create commands are executable content and must be reviewed and authorised through AAP.

## 5. Template variables

Support safe substitution for values such as project name and package identifier. Escape values appropriately for the destination file format. Reject invalid values and prevent path traversal through template variables. Do not allow a variable to create files outside the chosen destination.

## 6. Trust and provenance

Identify whether a template is built-in, user-created or imported from an external source. Treat imported templates and scripts as untrusted. Show source and version where known. Do not run template code merely because the user selected the template.

## 7. Acceptance criteria

- Users can preview a template's file tree before creation.
- Destination and overwrite behaviour are explicit.
- File creation is constrained to the chosen destination.
- Tool installation and script execution are separate consent steps.
- Failed creation reports partial results and does not claim full success.
- Created projects can be registered in Project Hub.

## 8. Dependencies and open decisions

Depends on Project Hub, Developer Tool Manager, AAP and file operations. Decide the built-in template list, template manifest format and whether template import ships in Core.

## 9. Related documentation

- [Project Hub](project-hub.md)
- [Developer Tool Manager](developer-tool-manager.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
