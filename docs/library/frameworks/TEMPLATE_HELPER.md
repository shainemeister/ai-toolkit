---
title: "Template helper"
description: "Before a new architecture, match the repository to a module already listed in the frameworks indexes."
version: "1.15.0"
status: current
doc_type: other
related:
  - path: ../../../ARCHITECTURE.md
  - path: ../../../kit/RULES.md
  - path: README.md
  - path: dev/general/README.md
last_updated: "2026-11-01"
---

# Template helper

#### AGENT INSTRUCTION

Before a new architecture, match the repository to a module already listed in the frameworks indexes.

1. Name the repository.
2. Read [frameworks/README.md](README.md). Open every directory it lists and read that directory's `README.md`. Follow every directory row in each index and read that `README.md`, until the rows name files.
3. Match the repository to a [catalog](#catalog) class. The class index uses the catalog domain name. When a child row matches the language or the theme, its `ARCHITECTURE.md` is the candidate. When no child matches, the child whose function is the blank for that class is the candidate.
4. When a module matches, show that `ARCHITECTURE.md` and ask the user to authorize copying it to the repository root. Stop. Do not ask the questions below. Do not start the [order of operation](#order-of-operation).
5. When no module matches, continue below to [AGENT QUESTION USER](#agent-question-user).

#### AGENT QUESTION USER

When the repository already has documents, draft the architecture from their theme and ask the user to authorize it. When it has no documents, the first question still names a recommended class from the catalog. A software repository uses the Developer class, `dev/`. The user does not choose headings, tables, or directories.

1. I see your {repository_name} has a similar theme to {catalog}. It is recommended that we build an `ARCHITECTURE.md` per `./kit/RULES.md`, so the repository stays continuous as it grows. Shall we continue?
2. Can you give me your thoughts on what you want to do or expand on with {repository_name}?
3. To finalize, I have put together a complete candidate `ARCHITECTURE.md`. Can you review it in `docs/research` and tell me what you think? If you approve and authorize it, I will add it under `docs/library/frameworks` in its seat and copy it to the repository root.

A yes to the first question starts the order of operation. The second answer fills the summary. The third question is [Verify and Action](#verify-and-action). The candidate stays in `docs/research` until the user authorizes it. When no seat fits, say so, add a catalog row, and stop after the opening and a one-line summary.

Apply [Decisions](#decisions) to every answer.

## Decisions

Use these three classes before a file is copied or placed. They apply to a matched module and to a new draft.

| Class | When it applies | Decision |
|-------|-----------------|----------|
| Consent | The user has been asked to authorize a file | Move or place the file only after the user says they approve and authorize it. Any other answer waits. The candidate stays in `docs/research`. |
| Scope | The user adds wishes beyond the matched module, or beyond the agreed directories | Copy a matched `ARCHITECTURE.md` unchanged. On a new draft, keep the agreed directories. Extra words go in the summary sentence only. |
| One class | The user describes more than one catalog class | Recommend the closest class. Name the others as separate seats. Continue with the one class the user accepts. |

## Order of operation

Draft the file in this order. [Verify and Action](#verify-and-action) places a certified file in the frameworks library, then copies it to the repository root. The catalog stays in this note.

1. [Schema](#schema). Carry these fields on the row.
2. [Catalog](#catalog). Choose one seat.
3. [Agreed fills](#agreed-fills). Copy the fields for that seat. When the seat has no fills row, stop after the opening and a one-line summary. `dev/<language>/` has no fills row and continues to the chain.
4. [Layout](#layout). Put the copied fields into this file shape.
5. [Chain of Thought](#chain-of-thought). Write the root file from those fields.
   - [Summary](#summary)
   - [Workspace Map](#workspace-map)
   - [Gate](#gate)
   - [Release](#release)
   - [Materials](#materials)
   - [Placement](#placement)
6. [Verify and Action](#verify-and-action). After the user confirms and certifies the draft, place it under `docs/library/frameworks/`, then copy it to the repository root.

## Schema

Step 1 of the [order of operation](#order-of-operation). Next: [Catalog](#catalog).

A framework module fills one row. Empty cells are omitted from the copied root file.

| Field | What it fixes |
|-------|----------------|
| `record` | The item that counts |
| `support` | Working material bound to the record |
| `trace` | The link required before the record is kept |
| `issue` | The delivered form of the record |
| `means` | The materials used to make or keep it |
| `seat` | The domain category where that theme sits |

The seat is the domain category. The record names the item inside that seat. A class is the first directory of a seat and the directory under `docs/library/frameworks/`. The catalog domain name and that directory's index use the same word.

## Catalog

Step 2 of the [order of operation](#order-of-operation). Next: [Agreed fills](#agreed-fills).

Records marked proposed are a starting fill so the row stays complete. A seat stays its own row when the record changes. The nearby column records that difference. A proposed row has no agreed fills yet.

A catalog row is a class. The class index holds the modules. Match the class name first, then a child row. Start a new file only when that search finds nothing.

| Name | What it is |
|------|------------|
| Class | The directory under `docs/library/frameworks/`, and the word on that directory's index |
| Record | The item that counts inside the class |
| Seat | The class, or a child under it when a language or a finished module exists |

| Domain | record | seat | Record status | Nearby |
|--------|--------|------|---------------|--------|
| Research | claim | `research/` | agreed | `data/` is the set. `analysis/` is a result drawn from a set |
| Household | obligation | `household/` | agreed | |
| Legal practice | matter | `legal/` | agreed | |
| Curriculum | outcome | `curriculum/` | agreed | `education/` holds a learner's standing across a program |
| Education | standing | `education/` | record proposed | `curriculum/` holds one course's outcomes |
| Career | appointment | `career/` | record proposed | |
| Business | entity | `business/` | record proposed | `ledger/` is a closed period |
| Newsroom | piece | `news/` | agreed | |
| Construction | drawing set and specification | `construction/` | agreed | |
| Ledger | closed period | `ledger/` | agreed | `business/` is the entity that keeps those books |
| Art | work | `art/` | record proposed | `collection/` is an object in custody |
| Recorded music | master | `music/record/` | agreed | `production/` is the performance call |
| Stage production | call | `production/` | agreed | `music/record/` is the released master |
| Collection care | object | `collection/` | agreed | `art/` is the work being made |
| Data | set | `data/` | record proposed | `analysis/` is a result drawn from a set. `research/` is the claim |
| Analysis | result | `analysis/` | record proposed | `data/` is the set. `research/` is the claim |
| Developer | domain | `dev/` | agreed | Coding. A language seat is `dev/<language>/` |

Developer is the class `dev/`. Its index is [dev/](dev/README.md), and the function line there uses the word Developer. A child row whose function matches the language is the module. When no language row matches, the child whose function is the blank for this class is the module. The copied map keeps `{{app}}/` at the top.

## Agreed fills

Step 3 of the [order of operation](#order-of-operation). Next: [Layout](#layout).

Copy the row for the chosen seat. These cells are the directories, the four headings, the check, the act, the destination, the target, the package, and the material rows. They are not derived again from the record, the seat, and the nearby note. A seat with no row here stops after the opening and a one-line summary, with no further headings. `dev/<language>/` has no row here and continues to the [chain](#chain-of-thought).

| Seat | Record directory | Support directories | Gate | Release | Materials | Placement |
|------|------------------|---------------------|------|---------|-----------|-----------|
| `research/` | `claims/` | `notes/`, `sources/`, `figures/` | Evidence | Publication | Sources | Custody |
| `household/` | `obligations/` | `correspondence/` | Proof | Binder | Documents | Obligations |
| `legal/` | `matters/` | `notes/`, `drafts/`, `authority/` | Docket | Filing | Authorities | Matters |
| `curriculum/` | `outcomes/` | `readings/`, `slides/`, `assessments/` | Assessment | Packet | Readings | Outcomes |
| `news/` | `pieces/` | `notes/`, `cuts/`, `documents/` | Review | Edition | Desk | Pieces |
| `construction/` | `issued/` | `sketches/`, `references/`, `model/` | Review | Issue | References | Drawings |
| `ledger/` | `close/` | `source/`, `entries/`, `reconciliations/` | Reconciliation | Statement | Books | Close |
| `music/record/` | `masters/` | `scores/`, `sessions/`, `edits/` | Credits | Release | Sessions | Masters |
| `production/` | `calls/` | `script/`, `design/`, `rehearsal/` | Cue | Opening | Script | Calls |
| `collection/` | `objects/` | `condition/`, `images/`, `loans/` | Identity | Loan | Register | Objects |

| Seat | Check | Act | Destination | Target | Package |
|------|-------|-----|-------------|--------|---------|
| `research/` | A figure or citation resolves to a file in `sources/` | Resolve each figure and citation to a file in `sources/` | Preprint and the version of record | The citable claim | Manuscript |
| `household/` | An obligation names its owner, its due date, and the document that proves it | Match the obligation to its owner, due date, and proof in `correspondence/` | The household record | The year | Annual binder |
| `legal/` | A document names the matter, the client, and the privilege label | Match the document to the matter, the client, and the privilege label | The matter file | The client | Filing or client letter |
| `curriculum/` | An assessment maps to an outcome | Match each assessment in `assessments/` to an outcome in `outcomes/` | The term | The learners | Term packet |
| `news/` | An editor and a source are named for each factual claim | Name the editor and the source in `documents/` for each factual claim | The public record | The edition date | The piece as published |
| `construction/` | The sheet index matches the model, and review comments are closed | Match the sheet index to `model/` and close each review comment | The project | Construction | Issued set |
| `ledger/` | An entry points at its source, and the period reconciles | Point each entry at a file in `source/` and reconcile the period | The period | The filing | Statement or return |
| `music/record/` | Credits match the takes used | Match the credits to the takes in `sessions/` | The distributor | The release | Distributor archive |
| `production/` | The promptbook matches the script, and each cue names an operator | Match the promptbook to `script/` and name an operator for each cue | The company | Opening | Opening call |
| `collection/` | The object has one identifier, and each loan or image names that object | Assign one identifier and match each loan and image to that object | The catalog | The borrower, when a loan exists | Catalog record and loan agreement |

| Seat | Name | Description |
|------|------|-------------|
| `research/` | Notebook | Working notes bound to a claim |
| `research/` | Primary sources | Sources a figure or citation resolves to |
| `household/` | Issuer documents | Documents that prove the obligation |
| `legal/` | Forms | Forms used for a filing or client letter |
| `legal/` | Authority | Authority cited for the matter |
| `curriculum/` | Readings | Readings mapped to an outcome |
| `curriculum/` | Question bank | Assessments that map to an outcome |
| `news/` | Style guide | The desk standard for a piece |
| `news/` | Document desk | Documents that source a factual claim |
| `construction/` | Survey | Site survey for the issued set |
| `construction/` | Codes | Codes the issued set meets |
| `construction/` | Product data | Product data named by the issued set |
| `ledger/` | Chart of accounts | Accounts the closed period uses |
| `ledger/` | Statements | Institution statements the entries point at |
| `music/record/` | Score | Score for the master |
| `music/record/` | Session recordings | Takes the credits name |
| `production/` | Script | Script the promptbook matches |
| `production/` | Design packet | Design the call follows |
| `collection/` | Accession register | Register that gives the object its identifier |
| `collection/` | Photography | Images that name the object |

## Layout

Step 4 of the [order of operation](#order-of-operation). Next: [Chain of Thought](#chain-of-thought).

Every written root file uses this shape. `Summary` and `Workspace Map` keep those headings. The four sections after the map use the headings from [agreed fills](#agreed-fills), in this order. For a `dev/<language>/` seat those headings are the `dev/` column, as named in [general/](dev/general/ARCHITECTURE.md).

```text
# Architecture

<what this repository is>. Law: [kit/RULES.md](kit/RULES.md). Replacing `kit/` does not edit this file.

## Summary
## Workspace Map          ← one fenced directory tree
## <gate>
## <release>
## <materials>
## <placement>
```

The opening states the record and the seat, then cites `kit/RULES.md`. For a seat in the agreed fills, that seat is the top of the Workspace Map. For `dev/<language>/`, the Workspace Map is the tree in `dev/general`, and `{{app}}/` stays the top of that tree.

| Order | Slot | Schema field | Shape | `dev/` heading |
|-------|------|--------------|-------|----------------|
| 1 | [Summary](#summary) | `record` | Prose | Summary |
| 2 | [Workspace Map](#workspace-map) | `seat` | One fenced directory tree | Workspace Map |
| 3 | [Gate](#gate) | `trace` | Check, act, purpose | Verification Pipeline |
| 4 | [Release](#release) | `issue` | Destination, target, package | Platform Targets |
| 5 | [Materials](#materials) | `means` | Name, description | Foundational Libraries |
| 6 | [Placement](#placement) | `support` | Name, owning layer, forbidden in, rationale | Library Positions & Boundaries |

The written file uses these table shapes. The [Research](#research) block lists the values for one seat. It is not a second file shape.

## Chain of Thought

Step 5 of the [order of operation](#order-of-operation). Next: [Verify and Action](#verify-and-action).

Each [catalog](#catalog) row fills one [layout](#layout). Copy the record, the seat, and the nearby note from the catalog. Copy the directories, headings, check, act, destination, target, package, and material rows from [agreed fills](#agreed-fills). Write one draft `ARCHITECTURE.md`.

`dev/<language>/` has no fills row and does not stop at step 3. Copy the tree and the four headings from [general/](dev/general/ARCHITECTURE.md). When the language is Rust, start from [rust_app/](dev/rust_app/ARCHITECTURE.md). The opening still states the record, the seat, and the law cite.

Any other catalog row with no agreed-fills row takes the opening and a one-line summary. It takes no gate, release, materials, or placement headings, and it takes no tree. [Research](#research) is one agreed row.

### Summary

Write the opening first. Then write the Summary prose: the record, the seat, and the nearby note.

### Workspace Map

Put the seat at the top of one fenced tree. Under it, place the record directory and the support directories from the agreed fills. Nearby seats are not folders inside this tree. A `dev/<language>/` seat uses the general tree instead, with `{{app}}/` at the top.

### Gate

Use the Gate heading, the check, and the act from the agreed fills. The section is a lead plus one check table. The purpose cell is `The record stays unkept until the check passes.`

### Release

Use the Release heading, the destination, the target, and the package from the agreed fills. The section is one destination table. Copy those three cells.

### Materials

Use the Materials heading. Copy each name-and-description row for that seat from the agreed fills. The section is that table.

### Placement

Use the Placement heading from the agreed fills. Write one row per directory. The record directory's owning layer is the seat, its forbidden-in cell lists the support directories, and its rationale is `Holds the record.` Each support directory's owning layer is support, its forbidden-in cell is the record directory, and its rationale is `Stays support.`

### Research

Values for `research/`, copied from the catalog and the agreed fills:

```text
# Architecture

<The record is the claim. It sits in research/.> Law: [kit/RULES.md](kit/RULES.md). Replacing `kit/` does not edit this file.

## Summary
## Workspace Map          ← one fenced directory tree
## Evidence
## Publication
## Sources
## Custody
```

| Slot | Filling |
|------|---------|
| Summary | The record is the claim. It sits in `research/`. `data/` holds the set. `analysis/` holds a result drawn from a set. |
| Workspace Map | `research/` with `claims/`, `notes/`, `sources/`, and `figures/` |

Evidence:

| Check | Act | Purpose |
|-------|-----|---------|
| A figure or citation resolves to a file in `sources/` | Resolve each figure and citation to a file in `sources/` | The record stays unkept until the check passes |

Publication:

| Destination | Target | Package |
|-------------|--------|---------|
| Preprint and the version of record | The citable claim | Manuscript |

Sources:

| Name | Description |
|------|-------------|
| Notebook | Working notes bound to a claim |
| Primary sources | Sources a figure or citation resolves to |

Custody:

| Name | Owning layer | Forbidden in | Rationale |
|------|--------------|--------------|-----------|
| `claims/` | `research/` | `notes/`, `sources/`, `figures/` | Holds the record |
| `notes/` | support | `claims/` | Stays support |
| `sources/` | support | `claims/` | Stays support |
| `figures/` | support | `claims/` | Stays support |

These four tables are the bodies of Evidence, Publication, Sources, and Custody. Copy them into the draft.

## Verify and Action

Step 6 of the [order of operation](#order-of-operation).

The user confirms the [catalog](#catalog) row and the [agreed fills](#agreed-fills), then certifies the drafted `ARCHITECTURE.md` by saying they approve and authorize it. Apply [Decisions](#decisions). A proposed record is not certified. It stays in the catalog until it has an agreed-fills row and a full draft.

1. Place the certified file at `docs/library/frameworks/<seat>/ARCHITECTURE.md`. The seat is the catalog path, so `music/record/` stays nested. A `dev/<language>/` seat is placed at `docs/library/frameworks/dev/<language>/ARCHITECTURE.md`.
2. Add that directory to the [frameworks](README.md) index. A seat under `dev/` is added to [dev/](dev/README.md).
3. Copy that file to the repository root as `ARCHITECTURE.md`.

A new domain is appended to the [catalog](#catalog) as domain, record, and seat. It is not certified until its fills and its draft exist.
