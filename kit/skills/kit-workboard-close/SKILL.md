---
title: Workboard close
description: "Mark a phase done, cancelled, or deferred. Leave the program on the board."
version: "2.1.0"
status: current
doc_type: procedure
related:
  - path: ../../../WORKBOARD.md
  - path: ../../rules/contracts.md
  - path: ../../RULES.md
last_updated: "2026-11-01"
---

# Workboard close

The record is [WORKBOARD.md](../../../WORKBOARD.md). That file stays the owner.

## Must not

- Do the phase's product work in this task.
- File a copy of the board or restore the blank. That is part of the authorized commit [contracts](../../rules/contracts.md#boundaries) names.
- Call the work done when a check this repository declares was skipped ([completion](../../RULES.md#completion)).
- Restate the status meanings. Those stay on the board.

## Procedure

1. Open [WORKBOARD.md](../../../WORKBOARD.md). If no program is registered, stop.
2. Set the phase to `done`, `cancelled`, or `deferred`. Leave this program as the primary program. Do not clear that field.
3. Add one progress line, newest first. Drop the oldest line when the log is over the cap.
4. Stop. This task does not file the board. [Contracts](../../rules/contracts.md#boundaries) owns when the board is filed.
