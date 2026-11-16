---
title: Commit
description: "Follow the procedure to write the commit."
version: "2.2.1"
status: current
doc_type: procedure
related:
  - path: ../../rules/git-commit.md
  - path: ../../RULES.md
  - path: ../../rules/versioning-and-git.md
  - path: ../../rules/contracts.md
last_updated: "2026-11-04"
---

# Commit

Follow the [procedure](#procedure) to write the commit.

## Procedure

1. Review `git status` and `git diff`.
2. Stage one logical surface. Leave out anything [versioning-and-git.md](../../rules/versioning-and-git.md#what-git-tracks) excludes.
3. Follow format and structure as outlined in [Message Structure](#message-structure).
4. Create the commit with that message.

## Message Structure

```text
{type}({scope}){!}: {short description}

{body}

{trailer}
```

**Core Rules**:

| Element | Rule |
|---|---|
| [type](#type) | (**required**) One value from the type table. |
| ([scope](#scope)) | (**required**) A noun in parentheses for the affected area, for example `{type}(parser):`. |
| `!` | (**optional**) After the scope, marks a breaking change, for example `{type}({scope})!: {short description}`. |
| `short description` | (**required**) After the colon and a space. Imperative, lowercase, about 72 characters, no trailing period. |
| [body](#body) | (**required**) One blank line after the description. Each point is a `-` bullet. |
| [trailer](#trailer) | (**required**) One blank line after the body. Each line is `Token: value`. Tokens use `-` instead of spaces, except `BREAKING CHANGE`. |

### `type`

| Type | Definition | Version Impact |
|---|---|---|
| `feat` | A new feature for the application or library. | MINOR bump |
| `fix` | A bug fix for the application. | PATCH bump |
| `docs` | Documentation only, for example `docs(rules): update the ref docs`. | None |
| `style` | Formatting only. The meaning stays the same. | None |
| `refactor` | Restructuring with no bug fix and no new feature. | None |
| `perf` | A change that improves performance. | None |
| `test` | Tests only. No production code changes. | None |
| `build` | The build system or external dependencies. | None |
| `ci` | CI configuration and scripts. | None |
| `chore` | Routine maintenance that does not change source or tests. | None |
| `revert` | Reverts a previous commit. | None |
| `!` or `BREAKING CHANGE` footer | A breaking change. This is not a type prefix. | MAJOR bump |

### `scope`

A noun for the area, such as `rules`, `markdown`, or a package name.

### `body`

One blank line after the short description. Each point is a `-` bullet. State what changed. A why or a migration note may follow. Do not paste a diff.

### `trailer`

Place this block after the body, with a blank line before it. Keep it out of the subject.

| Field | Resolution |
|---|---|
| `Assisted-by` | `{AI_MAKE} ({AI_MODEL})` for the AI that did this commit. Do not copy a vendor from a doc. |
| `Compliance` | The rules file that governed the change. Typically [RULES.md](../../RULES.md). |
| `Instructed-by` | `git config user.name` when it is non-empty. When no name can be obtained, use `user.undefined`. |

**Example**:
```text
{type}({scope}){!}: {short description}

{body}

Assisted-by: {AI_MAKE} ({AI_MODEL})
Compliance: {RULE}
Instructed-by: {user.name}
```
