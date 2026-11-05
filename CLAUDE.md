# Project Instructions

## Git Commits

- Never add a `Co-Authored-By` trailer (or any Claude/Anthropic attribution) to commit messages in this repository.

## Cross-Repo Access (Sibling Repos)

From this repo, an AI agent may access these sibling repos (located alongside this one under `SharedExpense Tracker All/`): `shared-expense-api`, `shared-expense-mobile`.

- **Read**: allowed in the repos listed above, EXCEPT `.env` files or any other files containing sensitive data (secrets, credentials, keys, tokens). Do not access files outside these listed repos.
- **Write**: ask the user for permission once per session before writing any file/folder in a given sibling repo (e.g., ask once before the first write to `shared-expense-api`; subsequent writes in that repo within the same session don't need to ask again).
- **Before writing anything to any repo**: first read that repo's own context/rules file (`CLAUDE.md`, `.cursorrules`, `.cursor/rules/*`, or equivalent) if one exists, and follow it.
- **Git operations**: always ask the user for permission before any git operation (commit, push, branch, etc.) in any of these sibling repos, every time.

This policy applies to every AI agent operating from this repo. The same rule is mirrored in `.cursor/rules/cross-repo-access.mdc`.

**Cursor complement:** this repo’s `.cursorignore` (plus each sibling’s own `.cursorignore` when present) keeps sibling `.env`/secrets out of Agent indexing and file tools.
