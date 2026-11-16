# Repository Standards Kit

`ai-toolkit` is a portable standards kit. Copy `kit/` into a repository. The host files an install may add are `AGENTS.md`, `MEMORY.md`, `WORKBOARD.md`, and `ARCHITECTURE.md`. Replacing `kit/` leaves those four files in place.

## Overview

The kit keeps a repository consistent for any harness. Law stays in `kit/`. Purpose and architectural framework stay in the root `ARCHITECTURE.md`. A framework module under `docs/library/frameworks/` is a copy-paste `ARCHITECTURE.md` a user or a program places on that root path. The kit enforces the root file. It does not write it.

There is no package install. The dependency is git. Source: https://github.com/shainemeister/ai-toolkit. Licensed under MIT — [LICENSE](LICENSE).

```text
ai-toolkit
├── kit/                         swappable module. law, rules, procedures
├── AGENTS.md                    session order
├── MEMORY.md                    agent notepad
├── WORKBOARD.md                 multi-phase work
├── ARCHITECTURE.md              purpose and framework for this repository
└── docs/library/frameworks/     framework modules copied onto a target ARCHITECTURE.md
```

To install, copy `kit/`. Copy `AGENTS.md`, `MEMORY.md`, or `WORKBOARD.md` only when that file is missing. Place an `ARCHITECTURE.md` at the root by copying a framework module or by writing one.

## Operator prompts

Law stays in [kit/RULES.md](kit/RULES.md). Session order stays in [AGENTS.md](AGENTS.md).

1. Open `kit/RULES.md`.
2. Open `ARCHITECTURE.md` before adding a tree or restating purpose.
3. Check existing files before creating one. The path rule is the one `kit/RULES.md` names.
4. Do not edit `AGENTS.md`, `MEMORY.md`, `WORKBOARD.md`, or `ARCHITECTURE.md` in order to replace `kit/`.
5. Do not claim the work done if a check this repository declares was skipped.
