# Git Centre

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** Version-control workspace

## 1. Purpose

Git Centre provides a visual, project-aware interface for inspecting local Git repositories and performing common version-control operations. It should make Git state easier to understand while preserving the user's ability to use their normal Git tools.

## 2. Repository overview

For a registered project containing a Git repository, show the repository root, current branch, working-tree state, upstream information when available and the most recent commit. Distinguish staged, unstaged and untracked changes. If Git is unavailable or the directory is not a repository, explain why.

## 3. Changes and diffs

Provide file lists for changed, staged, untracked and conflicted files. Show textual diffs with additions and removals clearly distinguished. Binary or unsupported files should be identified without pretending their contents can be reviewed as text.

Before staging or discarding changes, show the affected paths. Discarding changes can destroy user work and must require explicit approval. Do not automatically stage all files without the user's instruction.

## 4. Common operations

Potential Core operations include status, diff, stage selected files, unstage, commit, branch listing/creation/switching and history inspection. Each operation should show its target and expected effect. Commit creation requires the user to review the staged changes and commit message.

Merge, rebase, reset, cherry-pick, stash, conflict resolution and remote operations should be added only with explicit scope and careful previews. Do not hide Git's underlying semantics behind vague labels.

## 5. Remote operations

Fetch, pull and push affect remote state and should be clearly distinguished from local operations. Push behaviour must obey [Agent Git Permissions](agent-git-permissions.md). The setting that allows agent-initiated pushes is OFF by default; enabling it is not blanket approval. Confirmation and operation-specific policy still apply. Force push and remote branch deletion remain separately restricted.

## 6. AI integration

AI may explain status, summarise diffs or request Git actions through AAP. The model must not receive repository credentials, approve its own actions or bypass Git permissions. AI-generated commit messages are suggestions for user review, not automatically trusted descriptions.

## 7. Error handling

Explain common errors such as detached HEAD, unresolved conflicts, missing identity, rejected push, authentication failure and non-fast-forward updates. Preserve raw Git output in a detail view where useful, with secrets redacted.

## 8. Safety and privacy

- Confirm destructive operations and show exact affected paths/refs.
- Never silently discard or overwrite changes.
- Keep credentials in the OS credential manager or Secret Vault.
- Do not log tokens or credential-bearing remote URLs.
- Treat hooks and repository scripts as untrusted executable content.
- Avoid modifying global Git configuration without explicit user action.

## 9. Acceptance criteria

- Users can inspect status, branches, history and diffs.
- Staging is selectable and transparent.
- Destructive operations show a clear preview and require approval.
- Remote push policy is centrally enforced across UI, AI, terminal and workflows.
- Errors are reported without claiming success.
- The repository remains usable through ordinary Git tools outside ATLAS.

## 10. Dependencies and open decisions

Depends on Project Hub, Git executable availability, AAP, Permission Manager, Secret Vault and Agent Git Permissions. Decide whether Core uses the system Git CLI, a library or a hybrid approach after platform testing.

## 11. Related documentation

- [Agent Git Permissions](agent-git-permissions.md)
- [AAP and Safe Execution](aap-and-safe-execution.md)
- [Project Hub](project-hub.md)
- [Secret Vault](secret-vault.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
