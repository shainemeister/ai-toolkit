---
title: Contracts
description: "Stable promises a repository makes—behavior, shapes, exits, fields—and the rules for keeping them honest."
version: "1.19.0"
status: current
doc_type: rule
related:
  - path: ../RULES.md
  - path: ./versioning-and-git.md
  - path: ./path-pattern.md
  - path: ./git-commit.md
  - path: ../MARKDOWN-STANDARD.md
last_updated: "2026-11-01"
---

# Contracts

Stable promises a repository makes—behavior, shapes, exits, fields—and the rules for keeping them honest.

**Related:** [RULES.md](../RULES.md) · [versioning-and-git.md](./versioning-and-git.md) · [path-pattern.md](./path-pattern.md) · [git-commit.md](./git-commit.md) · [MARKDOWN-STANDARD.md](../MARKDOWN-STANDARD.md)

---

## Summary

| Must | Must not |
|------|----------|
| Give every contract one **canonical** owner (authority map) | Duplicate full contracts across README / guides; fork a second full statement of an owned rule |
| Update canonical docs with behavior in the **same change set**; retarget inbound links if an owned heading/path moves | Silently rename public APIs, CLI fields, or schema columns |
| Cross-link with relative paths and deep anchors; at point of use: one sentence + deep link | Leave contracts empty until “docs later” after behavior ships |
| Keep the last citation of an owner. Frontmatter shape is [MARKDOWN-STANDARD.md](../MARKDOWN-STANDARD.md#frontmatter) | Delete the last citation of an owner |

**Authority map** answers: *which file owns this concern?*  
**This file** answers: *what counts as a contract, when it breaks, and what must move together?*

---

## Contents

1. [What counts as a contract](#what-counts-as-a-contract)
2. [Boundaries](#boundaries)
3. [Ownership rules](#ownership-rules)
4. [Same-change-set rule](#same-change-set-rule)
5. [Cross-reference rules](#cross-reference-rules)
6. [Anti-patterns](#anti-patterns)
7. [Document history](#document-history)

---

## What counts as a contract

| Surface | Typical canonical doc | Examples |
|---------|----------------------|----------|
| CLI / automation | `CLI-GUIDE.md` | verbs, flags, exit codes, JSON stdout |
| Library / API | `API.md` or package README | public functions, types, errors |
| Schema / data | schema path | names, types, nullability |
| Methodology / scoring | `METHODOLOGY.md` | formulas, output columns |
| Security / trust | `SECURITY.md` (when required) | privilege, network, secrets model |
| Fixtures / golden tests | fixtures path | expected rows/outputs |
| Style / SAST gates | The checks the repository declares. Language checks sit outside the kit | Those checks |
| Kit / maintenance policy | [RULES.md](../RULES.md) + [rules/](./) | authority map, baseline, gates |

## Boundaries

Keep packages composable at the workflow layer. A call from one stack into another needs a documented boundary. Prefer a documented entry point over an ad-hoc script as the public surface. Declare the dependency policy. Prefer schema or config over a hard-coded business list buried in an engine. Naming a path follows [path-pattern.md](./path-pattern.md). The trees are the root `ARCHITECTURE.md`.

**Not contracts:**

- `docs/` is working memory. A public promise moves to the authority-map owner.
- `WORKBOARD.md` records open work. An authorized commit updates it before that commit is created, and the update is in that commit. When a phase ships, that update is in the same change set. When the primary program is `—`, the commit does not file the board. When a named program has a phase `open`, `active`, or `blocked`, the update adds one progress line and does not file. When a named program has no phase `open`, `active`, or `blocked`, the update files the copy and restores the blank. The board is not the only copy of a public promise. Its instruct table links the procedure. [RULES.md](../RULES.md#workboard) requires that link.
- `AGENTS.md` is the session order. It is not a second copy of these rules.
- `ARCHITECTURE.md` owns purpose and architectural framework. It is not a second copy of these rules. Replacing `kit/` does not edit it.

---

## Ownership rules

1. **Schema or API owns definitions** (names, types, nullability, display names). **Samples own example rows.** Headers and field names must match the contract.  
2. **Field renames and type changes are breaking.** Update together: schema, samples, default config, fixtures, and affected docs.  
3. **Public automation surfaces** (CLI flags, exit codes, stable output columns, JSON shapes) require guide updates and a version bump when they change.  
4. **Explainability** (if the product scores, ranks, or attributes metrics): keep intermediate audit fields; do not collapse into a single misleading total without documentation.  
5. **Fixtures / golden tests** are contracts. Behavior changes must keep validation green or deliberately refresh expected outputs with a documented reason.  
6. **No real credentials, tokens, regulated personal data, or production dumps** in the repository. Samples are synthetic or non-sensitive illustrations.  
7. **Regenerable output directories** (e.g. `output/`, build artifacts, diagnostics certificates) are workspace only—not source of truth and not versioned.

Owner paths live in the [authority map](../RULES.md#authority-map). When a concern has no row, add one before shipping the surface.

---

## Same-change-set rule

When behavior or a public contract changes, ship together (as applicable):

1. Code (if any)  
2. The **canonical** doc from the authority map  
3. Version bump when a public surface changes

A new path or name follows [path-pattern.md](./path-pattern.md). Versions follow [versioning-and-git.md](./versioning-and-git.md). Done means the checks in [RULES.md](../RULES.md#completion).

---

## Cross-reference rules

Every substantial markdown file should remain navigable for humans and AI agents.

### Mechanisms

| Mechanism | Use when |
|-----------|----------|
| **Authority map** ([hub](../RULES.md#authority-map)) | Establishing *owner path* for a concern |
| Frontmatter **`related:`** | Path net. The shape and the category of each path are [MARKDOWN-STANDARD.md](../MARKDOWN-STANDARD.md#related) |
| In-body **Related:** line **or** lead citations | Human-scannable citations. Not a copy of the `related` list |
| **Relative links** | Always from *this file’s* directory (`./`, `../`) |
| **Deep anchors** | Point at a specific rule (e.g. `#same-change-set-rule`) |
| **One-sentence summary + link** | **Must** at point of use (local consequence + deep link); do not paste another document’s full table |

### Form vs policy

| Doc | Role |
|-----|------|
| **This file** | Policy: when/why to cross-link; what must co-update; incorporation |
| [MARKDOWN-STANDARD.md](../MARKDOWN-STANDARD.md#author-checklist) | Form: frontmatter, the lead, and the author checklist |

### Incorporation

- A **second full statement** of a rule another file owns is **drift**. Cite the owner; do not reprint.  
- Removing the **last citation** of an owner is **context loss**. A reprint may go only if a one-sentence citation + deep link remains.  
- **Inbound same-change-set:** if this file’s owned heading, anchor, or path changes, grep inbound links and retarget in the **same change set**.  
- Frontmatter `related:` is a path net ([related](../MARKDOWN-STANDARD.md#related)). A body citation is not a second copy of that list.  
- **Point of use (Must):** when a foreign rule applies, write one sentence of local consequence and a **deep link** to the owner.

### Do not

- Fork a second full copy of a CLI matrix into the root README  
- Use absolute machine-only paths as the only example  
- Leave bidirectional pairs one-way for critical peers (hub ↔ domain rules; contracts ↔ versioning/verification)

---

## Anti-patterns

| Avoid | Prefer |
|-------|--------|
| README as the only API/CLI contract | Canonical package guide + short README summary |
| Empty `SECURITY.md` for the template | Omit unless the package executes, uses the network, elevates, or handles secrets |
| Code ships, guide “later” | Same change set as the canonical doc |
| Silent public field or API rename | Coordinated contract bump + fixtures + docs |
| Duplicating full matrices into every doc; second-home reprint of an owned rule | Link + short summary (one sentence + deep link) |
| Deleting the last citation of an owner | Keep at least one citation; then drop the reprint |
| A procedure pack restates a rule this file owns | Cite the owner |
| Public API or CLI matrix lives only under `docs/` | Promote it to the package contract |
| Phase marked done only in chat | Update `WORKBOARD.md` in the same change set |
| Commit that leaves the workboard stale | Update the board before that commit is created |
| A second commit whose only change is the workboard filing | File the board in the authorized commit |
| Full `kit/rules/*` pasted into `AGENTS.md` | Point at `kit/RULES.md` |

---

## Document history

| Version | Notes |
|---------|--------|
| 1.19.0 | Style and SAST checks are the ones the repository declares. No kit security baseline |
| 1.18.0 | The board's instruct table links each procedure. This file keeps the filing rule |
| 1.17.0 | Board verbs are assigned in `kit/RULES.md`. This file keeps the filing rule |
| 1.16.0 | The board procedures are the four workboard packs. Each stops when its edit is done |
| 1.15.0 | `related` is a path net. It is not a co-update list |
| 1.14.0 | Purpose stays in `ARCHITECTURE.md`. A release does not require a changelog file |
| 1.13.0 | A named program is filed only when it has no open, active, or blocked phase. A primary program of `—` is not filed |
| 1.12.0 | A new path cites path-pattern.md |
| 1.11.0 | The board update is in the authorized commit, before that commit is created |
| 1.10.0 | A program is filed when no phase is `open`, `active`, or `blocked` |
| 1.9.0 | Every commit updates the workboard before the session closes. A finished program is filed and the blank restored |
| 1.8.0 | A fully done board stays in place for the commit that shipped it. Filing the copy is the next task |
| 1.7.0 | The multi-phase record is root `WORKBOARD.md` |
| 1.6.0 | Style and SAST cite the security baseline. Language checks sit outside the kit |
| 1.5.0 | Boundary rules live here. Architecture file retired. |
| 1.4.2 | Cite files.md for new path/name; ownership and same-change-set unchanged |
| 1.4.1 | Density restyle (kit 2.8.0); unique ownership, same-change-set, and incorporation rules unchanged |
| 1.4.0 | Incorporation + inbound-link duty (kit 2.7.0) |
| 1.3.2 | Operator prompts is not a product contract (kit 2.6.2) |
| 1.3.1 | Habitat L0 is not a contract; anti-patterns for RULES-in-AGENTS and chat-only done (kit 2.6.0) |
| 1.3.0 | Workboard is an execution contract; phase-ship same-change-set (kit 2.4.0) |
| 1.2.0 | AI docs workspace is not a contract; promotion anti-pattern (kit 2.3.0) |
| 1.1.0 | Instruct bridge: packs direct owners; co-maintain + lifecycle pointer (kit 2.2.0) |
| 1.0.1 | Agent Instruct packs are views, not contracts; dual-authority anti-pattern |
| 1.0.0 | New first-class module for kit 2.0; ownership rules from former “Data and contract rules”; cross-reference policy |
