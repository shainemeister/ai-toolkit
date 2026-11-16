---
title: "Versioning and git"
description: "Document and project versions, and what git tracks. Commit messages live in the kit-commit procedure."
version: "2.3.1"
status: current
doc_type: rule
related:
  - path: ../RULES.md
  - path: ../skills/kit-commit/SKILL.md
  - path: ./contracts.md
last_updated: "2026-11-04"
---

# Versioning and git

Document and project versions, and what git tracks. Commit messages live in the kit-commit procedure.

**Related:** [RULES](../RULES.md) · [commits](../skills/kit-commit/SKILL.md) · [contracts](./contracts.md)

## Versions

| Surface | What it is | Where it lives |
|---------|------------|----------------|
| Document version | One file | That file's `version` and `last_updated`. The shape is checked. A missing bump is not a frontmatter failure |
| Project version | The repository's product | That repository's packaging metadata |

Replacing `kit/` does not bump the project version. Bump the project version when public behavior or a contract changes. A subject with `!` before the colon, or a `BREAKING CHANGE:` footer, is that kind of change ([breaking change](../skills/kit-commit/SKILL.md#type)).

## What git tracks

Track source, schema, fixtures, and docs. Do not track secrets, environment files, or regenerable build output. Respect `.gitignore`.

Do not rewrite published history on a shared branch without an explicit decision to do so.

Commit messages, including the AI trailers, are owned by [kit-commit](../skills/kit-commit/SKILL.md).
