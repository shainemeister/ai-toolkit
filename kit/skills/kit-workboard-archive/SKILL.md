---
title: Workboard archive
description: "Update the workboard for an authorized commit. File a finished program and restore the blank."
version: "2.1.0"
status: current
doc_type: procedure
related:
  - path: ../../../WORKBOARD.md
  - path: ../../rules/contracts.md
  - path: ../../rules/directory-index.md
  - path: ../../rules/path-pattern.md
last_updated: "2026-11-01"
---

# Workboard archive

The record is [WORKBOARD.md](../../../WORKBOARD.md). The blank is [template/workboard.md](../kit-workboard-register/template/workboard.md). Those paths follow [path-pattern.md](../../rules/path-pattern.md). [Contracts](../../rules/contracts.md#boundaries) owns when this update files the board. Do this before that commit is created. This task does not create the commit.

## Must not

- File the board or restore the blank while a phase is `open`, `active`, or `blocked`.
- Add a second plan-index row for a program that already has one.
- Edit `MEMORY.md`, `AGENTS.md`, or `ARCHITECTURE.md`.
- Commit.
- Restate the status meanings. Those stay on the board.

## Procedure

1. Open [WORKBOARD.md](../../../WORKBOARD.md).
2. If the primary program is `—`, stop.
3. If any phase is `open`, `active`, or `blocked`, add one progress line for the commit, newest first. Drop the oldest line when the log is over the cap. Stop.
4. Copy the file to `docs/plan/archive/<program>/WORKBOARD.md`. The directory name is the primary program. When `docs/plan/<program>/` exists, move its files into that archive directory and rewrite relative links in those files. Do not create `docs/plan/<program>/` when it is absent. Rewrite each relative link, and each `related:` path, so it resolves from the archive file to the same target. When that directory is new, follow [directory-index.md](../../rules/directory-index.md). When the archive directory already has a README that lists the snapshot, leave that row. Add one row on [docs/plan/README.md](../../../docs/plan/README.md) only when that program has no row there.
5. Replace root `WORKBOARD.md` with the fenced body of [the blank](../kit-workboard-register/template/workboard.md). Remove the fence. The root file has no frontmatter.
6. Stop. Do not commit. Do not open another skill.
