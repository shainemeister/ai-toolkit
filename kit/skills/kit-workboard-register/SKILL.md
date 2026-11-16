---
title: Workboard register
description: "Open one program on the workboard before phased work starts."
version: "2.1.0"
status: current
doc_type: procedure
related:
  - path: ../../../WORKBOARD.md
  - path: ../../rules/contracts.md
  - path: ../../RULES.md
last_updated: "2026-11-01"
---

# Workboard register

The record is [WORKBOARD.md](../../../WORKBOARD.md). That file stays the owner.

## Must not

- Replace a program that is already primary.
- Paste the live phase table into another file.
- Do the phase's product work in this task.
- Restate the status meanings. Those stay on the board.

## Procedure

1. Open [WORKBOARD.md](../../../WORKBOARD.md). If it is missing, copy the fenced body of [template/workboard.md](template/workboard.md) to the repository root and remove the fence. The root file has no frontmatter.
2. If the primary program is not `—`, stop.
3. If this work has no phases, stop. Do not open a program.
4. Write one program: goal, base, decisions, and every step in the phase table. One phase is `active` only when that phase is the work about to start. The others stay `open`. The File cell is a relative link to the file that phase edits, or `—` when it edits no file. The Draft cell is the phase document, a relative link to `docs/plan/<program>/<id>-<verb>.md`, or `—` when that phase has no draft. Notes do not repeat either path. The blank owns the columns. Write the draft the Draft cell names, with that phase's working text, in the same change set as the row. Do not create a draft that has no body.
5. Add one progress line.
6. Stop.
