---
title: "Path pattern"
description: "A name is a category, a class, a noun, and a verb. Root ARCHITECTURE.md chooses the trees."
version: "2.0.0"
status: current
doc_type: rule
related:
  - path: ../RULES.md
  - path: ./directory-index.md
  - path: ./contracts.md
  - path: ../MARKDOWN-STANDARD.md
last_updated: "2026-11-01"
---

# Path pattern

A name is a category, a class, a noun, and a verb. Root `ARCHITECTURE.md` chooses the trees. This file names a path inside a tree it allows.

**Related:** [RULES](../RULES.md) · [directory index](./directory-index.md) · [contracts](./contracts.md) · [markdown](../MARKDOWN-STANDARD.md)

Open this file when adding, moving, splitting, or naming a path. Do not paste it into `AGENTS.md`.

**Enforcement:** Policy plus the [author checklist](../MARKDOWN-STANDARD.md#author-checklist).

## Grammar

| Term | Names |
|------|--------|
| Category | A tree `ARCHITECTURE.md` allows |
| Class | One noun grouping inside that tree |
| Noun | The file or the module |
| Verb | A function inside the noun, or one procedure name |

A sentence-path narrates its steps, or uses a verb as a noun. Do not use one. The same leaf name may repeat when the directory scopes it (`README.md`, `SECURITY.md`, `SKILL.md`).

## Evidence

Create a path only when one of these holds:

| Evidence | Example |
|----------|---------|
| Surface exists | A public surface already shipping |
| Inventory row | A path listed on the map |
| User asked | An explicit request for the path |
| Module needed | A domain or contract the work requires |

Read `ARCHITECTURE.md` before adding a tree. When it does not name the tree, stop.

New durable markdown gets the frontmatter block in the same change set ([when this applies](../MARKDOWN-STANDARD.md#when-this-applies)).

## One role

A new file is allowed when its role is absent from the directory index. When the role is listed, edit that file. A split removes the role from the old file in the same change set.

A new directory of intentional files is indexed in that same change set ([directory index](./directory-index.md)). A public promise follows [contracts](./contracts.md). This file does not restate `ARCHITECTURE.md`.

## Must not

- Create an empty tree for ceremony.
- Require a root that `ARCHITECTURE.md` does not name.
- Use a sentence-path or a verb-named module.

## Document history

| Version | Notes |
|---------|--------|
| 2.0.0 | The grammar extends `ARCHITECTURE.md`. It does not choose the trees |
| 1.1.0 | This file owns "one task, one skill" and the root `skills/<action>/` exception |
| 1.0.0 | Split from `files.md`. This file owns the path pattern |
