---
title: "Directory index"
description: "A new navigable directory of intentional files gets an index README in the same change set. A missing historical index is not a failed gate."
version: "1.2.0"
status: current
doc_type: rule
related:
  - path: ../RULES.md
  - path: ./path-pattern.md
  - path: ./contracts.md
  - path: ../MARKDOWN-STANDARD.md
last_updated: "2026-11-01"
---

# Directory index

A new navigable directory of intentional files gets an index README in the same change set. A missing historical index is not a failed gate.

**Related:** [RULES](../RULES.md) · [path pattern](./path-pattern.md) · [contracts](./contracts.md) · [markdown](../MARKDOWN-STANDARD.md)

## Directory index

A navigable, versioned directory that contains other intentional files gets `README.md` in the same change set as that directory or an intentional file it contains ([same change set](./contracts.md#same-change-set-rule)).

The table is file to function. The cell shape is the [directory index](../MARKDOWN-STANDARD.md#directory-index) in the markdown standard. The index README uses `doc_type: index` and omits `related` ([doc_type](../MARKDOWN-STANDARD.md#doc_type)).

Copy [template/index.md](template/index.md) to `README.md` in that directory. Retarget the links. Set `doc_type` to `index`, omit `related`, and replace every placeholder. A name that breaks the grammar is [path-pattern.md](./path-pattern.md).

Exclude regenerable output, vendor, `.git/`, secrets, host trees this repository did not create, and language leaves already listed in the parent package README.

The index is forward-only. Root `FILE-CATALOG.md` stays optional. When a whole-repo catalog exists, update it with the listed paths ([authority map](../RULES.md#authority-map)).

A procedure pack uses `SKILL.md` as its index. Do not add `README.md` in that pack directory. The parent directory keeps its own index.

`kit/` is indexed by `kit/RULES.md`. Do not add `kit/README.md`.

## Must not

- Backfill a historical directory.
- Require a whole-repo catalog before `kit/` can be copied in.

## Document history

| Version | Notes |
|---------|--------|
| 1.2.0 | The directory blank lives at `template/index.md`. Copying it is this rule |
| 1.1.3 | An index README uses `doc_type: index` and omits `related` |
| 1.1.2 | A whole-repo catalog is not a requirement for copying `kit/` |
| 1.1.1 | `kit/` is indexed by `kit/RULES.md`. |
| 1.1.0 | This file owns the ban on `README.md` beside `SKILL.md` |
| 1.0.0 | Split from `files.md`. This file owns when an index is required |
