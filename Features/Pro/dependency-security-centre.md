# Dependency Security Centre

**Release:** ATLAS Pro  
**Status:** Planned  
**Category:** Dependency risk awareness

## 1. Purpose

Dependency Security Centre helps users understand the third-party packages their projects rely on. It may identify known vulnerability advisories, outdated dependencies, licence metadata and dependency-tree information using reliable ecosystem sources.

It is an assistance and visibility tool, not a guarantee that a project is secure.

## 2. Dependency inventory

Read supported manifests and lockfiles to identify direct and transitive dependencies where possible. Show package name, resolved version, ecosystem, direct/transitive status and source file. If the dependency graph cannot be fully resolved, state the limitation.

## 3. Vulnerability matching

Match dependencies against recognised advisory sources. For each result, show affected package/version range, advisory identifier, severity as defined by the source, publication/update date and source link. Distinguish confirmed matches from uncertain package-name or version matches.

Show source freshness and last successful check. If the service is offline or a database is stale, label the result accordingly.

## 4. Updates and remediation

Offer explanations and possible remediation paths, such as updating a dependency or reviewing an upstream advisory. Do not automatically upgrade packages, rewrite lockfiles or run package-manager commands. Before a remediation, show the proposed version changes, compatibility uncertainty and files affected.

Dependency updates may introduce breaking changes or execute package scripts. They require explicit approval and must use Developer Tool Manager/AAP execution controls.

## 5. Licence information

Where reliable metadata is available, show declared licence identifiers and source. Do not provide legal conclusions or claim that a package is legally compatible without sufficient evidence. Unknown or conflicting licence metadata must be labelled.

## 6. Supply-chain considerations

Future checks may include package provenance, maintainer changes, suspicious release signals or typosquatting indicators, but only when supported by trustworthy data. Avoid alarmist claims from weak signals. Explain the evidence and confidence.

## 7. Privacy and network use

Dependency names and versions may be sent to external advisory services. Disclose the service and data sent. Avoid uploading source code by default. Keep local manifests and analysis local unless the user chooses otherwise.

## 8. Acceptance criteria

- Supported manifests and lockfiles produce an inspectable inventory.
- Vulnerability matches include advisory source and affected version range.
- Stale/offline data is clearly identified.
- Confirmed and uncertain matches are distinguished.
- Remediation previews changes and requires approval.
- Licence metadata is sourced and not presented as legal advice.

## 9. Dependencies and open decisions

Depends on Project Hub, package ecosystem parsers, network/advisory providers, Build & Test Centre and AAP. Choose supported ecosystems and advisory sources based on freshness, licensing and API availability.

## 10. Related documentation

- [Project Hub](../Core/project-hub.md)
- [Build & Test Centre](build-and-test-centre.md)
- [Developer Tool Manager](../Core/developer-tool-manager.md)
- [AAP and Safe Execution](../Core/aap-and-safe-execution.md)
- [Privacy and Offline Operation](../Core/privacy-and-offline.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
