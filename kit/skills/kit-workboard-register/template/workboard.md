---
title: "Workboard blank"
description: "Blank for root WORKBOARD.md. Copy the fenced body when that file is missing, and when a finished program is archived."
version: "1.3.0"
status: current
doc_type: template
related:
  - path: ../../../RULES.md
  - path: ../../../rules/contracts.md
  - path: ../../../rules/path-pattern.md
  - path: ../../../rules/directory-index.md
  - path: ../../../../WORKBOARD.md
last_updated: "2026-11-01"
---

# Workboard blank

Blank for root WORKBOARD.md. Copy the fenced body when that file is missing, and when a finished program is archived.

**Related:** [RULES](../../../RULES.md) · [contracts](../../../rules/contracts.md) · [path pattern](../../../rules/path-pattern.md) · [directory index](../../../rules/directory-index.md) · [live board](../../../../WORKBOARD.md)

The fence is the root file. Remove the fence when you copy it. Links inside the fence are written for that root file.

## Body

```markdown
# Workboard

Open multi-phase work. One program is active at a time.

**Updated:** —
**Primary program:** —
**Rules:** [kit/RULES.md](kit/RULES.md)

| Status | Meaning |
|--------|---------|
| `open` | Not started |
| `active` | Current phase (prefer exactly one) |
| `blocked` | Waiting on a decision |
| `done` | Finished |
| `cancelled` | Dropped |
| `deferred` | Parked |

Primary program `—` means no program is registered.

An authorized commit updates this file before that commit is created, and files it only for a named program with no phase `open`, `active`, or `blocked`. The boundary rule is the one [kit/RULES.md](kit/RULES.md) names.

## Instruct

| When | Procedure |
|------|-----------|
| No program is registered, and the work has phases | [register](kit/skills/kit-workboard-register/SKILL.md) |
| A phase is the work about to start | [advance](kit/skills/kit-workboard-advance/SKILL.md) |
| A phase is finished, dropped, or parked | [close](kit/skills/kit-workboard-close/SKILL.md) |
| An authorized commit is about to be created | [archive](kit/skills/kit-workboard-archive/SKILL.md) |

Open the procedure that row links. It does that edit and stops. [kit/RULES.md](kit/RULES.md) requires these links.

## Active program

| Field | Value |
|-------|--------|
| **Goal** | — |
| **Base** | — |
| **Docs** | — |
| **Annex** | — |
| **Checks** | — |

### Decisions

| Rule | Owner |
|------|--------|
| — | — |

### Phases

| ID | Work | File | Draft | Status | Notes |
|----|------|------|-------|--------|-------|
| — | — | — | — | — | — |

The File cell is the product file. The Draft cell is the phase document at `docs/plan/<program>/<id>-<verb>.md`. Notes do not repeat either path.

### Progress log (newest first, max ~15 lines)

- —

## Deferred

| ID | Note |
|----|------|
| — | — |

## Not on this board

| Concern | Where |
|---------|--------|
| Session order | `AGENTS.md` |
| Agent notepad | `MEMORY.md` |
| Purpose and framework | `ARCHITECTURE.md` |
| Kit law | `kit/RULES.md` |

Check a phase off by setting its status. A registered program replaces the `—` rows.
```
