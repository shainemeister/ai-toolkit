---
title: Repository maintenance rules
description: Authority map for a repository. Detail lives in the linked file.
version: "4.2.1"
status: current
doc_type: rule
related:
  - path: ../AGENTS.md
  - path: ../ARCHITECTURE.md
  - path: ../WORKBOARD.md
  - path: MARKDOWN-STANDARD.md
  - path: rules/path-pattern.md
  - path: rules/contracts.md
last_updated: "2026-11-04"
---

# Repository maintenance rules

Authority map for a repository. Detail lives in the linked file.

**Related:** [AGENTS](../AGENTS.md) · [architecture](../ARCHITECTURE.md) · [workboard](../WORKBOARD.md) · [markdown](MARKDOWN-STANDARD.md) · [path pattern](rules/path-pattern.md) · [contracts](rules/contracts.md)

## Summary

| Must |
|------|
| Give each concern one owner. Cite that file. Do not restate it. |
| Keep standards in `kit/`. Keep the project outside it. |
| Extend the file that already holds a role. Do not add a second file for the same role. |
| Read root `ARCHITECTURE.md` before adding a tree or restating purpose. |
| Leave `AGENTS.md`, `MEMORY.md`, `WORKBOARD.md`, and `ARCHITECTURE.md` in place when `kit/` is replaced. |
| Do not claim the work done if a check this repository declares was skipped. |

## Authority map

| Concern | Owner |
|---------|--------|
| Path pattern | [path-pattern.md](rules/path-pattern.md) |
| Directory index | [directory-index.md](rules/directory-index.md) |
| Contracts and boundaries | [contracts.md](rules/contracts.md) |
| Commit messages | [kit-commit](skills/kit-commit/SKILL.md) |
| Versions and what git tracks | [versioning-and-git.md](rules/versioning-and-git.md) |
| README shape and frontmatter | [MARKDOWN-STANDARD.md](MARKDOWN-STANDARD.md) |
| Procedures | [skills/README.md](skills/README.md) |
| Session order | [AGENTS.md](../AGENTS.md) |
| Agent notepad | [MEMORY.md](../MEMORY.md) |
| Multi-phase work | [WORKBOARD.md](../WORKBOARD.md) |
| Purpose and architectural framework | [ARCHITECTURE.md](../ARCHITECTURE.md) |

Kit text stays generic. Purpose and framework stay in the root `ARCHITECTURE.md`.

## Workboard

Open the procedure the root `WORKBOARD.md` instruct table links for this edit. Do that edit and stop. Do not choose a different procedure.

## Install

Copy `kit/` into the repository. Leave the directory whole.

If `AGENTS.md`, `MEMORY.md`, or `WORKBOARD.md` is missing, copy that file from the kit source. If the file exists, leave it.

Root `ARCHITECTURE.md` is required. Copy a framework module onto that path, or write the file. A framework module is an `ARCHITECTURE.md` a user or a program keeps outside `kit/` and copies onto the root. This kit does not choose the module.

`AGENTS.md`, `MEMORY.md`, and `ARCHITECTURE.md` cite `kit/RULES.md` and no other path under `kit/`. `WORKBOARD.md` cites `kit/RULES.md` and the four procedures in its instruct table. Replacing `kit/` does not edit them. There is no adopt pass and no upgrade pass.

## Architecture

Open the root `ARCHITECTURE.md` before adding a tree or restating what the repository is for. A new path that the file forbids does not land. Do not copy its body into `kit/` or into `AGENTS.md`.

When the root file is missing, stop. The next task is to place one. Do not infer a framework from the tree and write that inference into another file.

## Completion

Do not claim the work done if a check this repository declares was skipped. A docs-only repository uses the [author checklist](MARKDOWN-STANDARD.md#author-checklist). A change that adds a tree or restates purpose also follows the root `ARCHITECTURE.md`.
