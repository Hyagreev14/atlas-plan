# Architecture Visualizer

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Project understanding and visualisation

## 1. Purpose

Architecture Visualizer creates navigable visual representations of a project's structure and detected relationships. It should help users understand how a codebase is organised without presenting guesses as verified architecture.

## 2. Visual views

Potential views include:
- Directory and module structure.
- Application entry points and major components.
- Import/dependency relationships.
- Service or package boundaries.
- Configuration and build relationships.
- Selected call or data-flow relationships when a supported analyser can establish them.

The initial implementation should focus on relationships that can be detected reliably. Do not promise complete runtime architecture discovery from static files alone.

## 3. Analysis sources

Use project manifests, source imports, configuration files, build metadata and supported language tooling. Each detected relationship should retain its source evidence. Dynamic imports, reflection, generated code, runtime configuration and external services may be incomplete.

## 4. Confidence and provenance

Differentiate direct file relationships, parser-derived relationships and AI-inferred summaries. Provide a way to inspect why two nodes are connected and which files support the connection. Mark unresolved or ambiguous edges rather than inventing a connection.

## 5. Interaction

Users should be able to zoom, pan, search, filter by language/type, select a node and open its source location. Selecting a node may show a concise summary, dependencies and references. Large graphs should support filtering and progressive loading to remain usable.

## 6. AI integration

AI may summarise selected architecture areas or answer questions using graph evidence. It must distinguish graph facts from generated interpretation. AI-suggested refactors or file changes must go through AAP and normal approval.

## 7. Performance

Analyse incrementally where possible and cache results with timestamps. Recompute affected portions when files change. Provide cancellation and progress for large projects. Avoid repeatedly parsing the entire repository on every view open.

## 8. Privacy and security

Keep analysis local by default. If a cloud model is used to summarise code, disclose which selected files or graph data are sent. Treat source comments and repository documentation as untrusted prompt content.

## 9. Acceptance criteria

- A supported project can be visualised with source-linked nodes.
- Users can inspect evidence for detected relationships.
- Inferences are visibly distinguished from static detections.
- Search and filtering work on larger graphs.
- Stale analysis is identified and refreshable.
- AI summaries do not claim unsupported relationships.

## 10. Dependencies and open decisions

Depends on Project Hub, language parsers/indexers, AI Workspace and possibly AI Project Memory. Select a limited set of languages and graph types for the first version.

## 11. Related documentation

- [Project Hub](../Core/project-hub.md)
- [AI Project Memory](ai-project-memory.md)
- [AI Workspace](../Core/ai-workspace.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
