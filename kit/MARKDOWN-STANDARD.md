---
title: "Markdown standard"
description: "Landing README, directory-index README, and the minimum frontmatter for a kit document. Purpose stays in ARCHITECTURE.md."
version: "4.1.0"
status: current
doc_type: rule
related:
  - path: RULES.md
  - path: rules/directory-index.md
  - path: rules/contracts.md
last_updated: "2026-11-01"
---

# Markdown standard

Landing README, directory-index README, and the minimum frontmatter for a kit document.

**Related:** [RULES](RULES.md) · [directory index](rules/directory-index.md) · [contracts](rules/contracts.md)

Kit text stays generic. A term that needs a precise meaning gets a short definition. The root `ARCHITECTURE.md` holds this repository's purpose and framework. A kit example is not that description.

## When this applies

Durable markdown carries the block below. These files omit it:

| File | Why |
|------|-----|
| Root `README.md` | Landing shape |
| Root `AGENTS.md` | Session order |
| Root `MEMORY.md` | Agent notepad |
| Root `WORKBOARD.md` | Multi-phase record |
| `ARCHITECTURE.md` | Purpose and framework. A framework module uses this filename and omits frontmatter so a copy stays valid at the root |

## Frontmatter

The block is one YAML document at byte 0. It has no BOM, duplicate keys, anchors, aliases, tags, or YAML 1.1 booleans (`yes`, `no`, `on`, `off`). Keys are exactly the table, in this order. `audience` and `keywords` are not keys.

```yaml
---
title: "Human-readable title"
description: "What this file contains now."
version: "1.0.0"
status: current
doc_type: rule
related:
  - path: rules/contracts.md
last_updated: "YYYY-MM-DD"
---
```

| Field | Required | Rule |
|-------|----------|------|
| `title` | Yes | Matches the H1. |
| `description` | Yes | One sentence is enough. Current contents. Wrong if pasted onto a sibling file. The first sentence is the lead under the H1. |
| `version` | Yes | `N.N.N`. Shape only. A missing bump is not a frontmatter failure. |
| `status` | Yes | `draft`, `current`, or `deprecated`. |
| `doc_type` | Yes | The category of this file. |
| `related` | Substantial docs | 3–7 paths. A thin index omits the key. |
| `last_updated` | Yes | `YYYY-MM-DD`. |

A `template` file may keep `{{PLACEHOLDERS}}` in these fields until it is copied, and it may have fewer than 3 `related` entries.

### doc_type

| Value | File |
|-------|------|
| `index` | A directory `README.md` |
| `rule` | `kit/RULES.md`, a file in `kit/rules/` other than its `README.md`, and this file |
| `procedure` | A `SKILL.md` |
| `template` | A file in a `template/` directory |
| `other` | A durable doc that has no category yet |

`host` is not a value. A `related` path to `AGENTS.md`, `MEMORY.md`, `WORKBOARD.md`, or `ARCHITECTURE.md` is a host file because of that filename.

### related

Each entry is one relative path:

```yaml
related:
  - path: rules/contracts.md
```

The category of the link is the target's `doc_type`. A directory `README.md` is `index`. A path to `kit/RULES.md`, `kit/rules/`, or this file is `rule`. The path resolves. The count is 3–7 on a substantial doc. Updating a neighbor stays a body edit. It is not a reason to rewrite this list.

Refresh `description` when the file's owned facts change.

## Landing README

The root `README.md` has no frontmatter. Two headings, in order: `## Overview`, then `## Operator prompts`.

Overview says what the repository is, who it is for, and one way to start. Operator prompts are the session load path for that repository. They point at `kit/RULES.md`. They do not paste the rules.

## Directory index

A directory README that lists the files in that directory is a table of file to function. Its `doc_type` is `index`, and it omits `related`. The function cell says the role of that file in that folder, in one line. It is not the landing page, and it does not repeat the file's `description` verbatim.

[directory-index.md](rules/directory-index.md) owns when the index is required.

## Author checklist

Before calling a documentation change done:

- One title. Relative links resolve from the file.
- Frontmatter matches this schema, or the file is on the omit list.
- `description` still matches the file.
- A new directory of intentional files has an index README with `doc_type: index`.
- The landing page, when edited, still has Overview and then Operator prompts.
- No second copy of a rule that already has an owner.
- `AGENTS.md`, `MEMORY.md`, and `ARCHITECTURE.md` cite `kit/RULES.md` and no other path under `kit/`. `WORKBOARD.md` may also cite the four procedures in its instruct table.
