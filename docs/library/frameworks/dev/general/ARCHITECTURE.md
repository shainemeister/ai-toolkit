# Architecture

Copy this file onto the repository root as `ARCHITECTURE.md`. Law at that root is `kit/RULES.md`. `kit/` enforces the root file and does not rewrite it.

## Summary

An architectural map for {{product_kind}}. It outlines a layered workspace that keeps domain logic at the center, adapters and user-facing surfaces at the edges, and a single composition root that assembles them, alongside the foundational libraries and tooling the layout builds on and where each typically fits.

`{{app}}` stands for the project name. Directory names stay as shown. Package or module names take the form `{{app}}-<unit>`.

## Workspace Map

```text
{{app}}/
├── {{manifest}}            # workspace members and shared policy
├── {{lockfile}}            # committed
├── {{toolchain_pin}}       # pinned toolchain and per-platform targets
├── {{task_config}}         # alias so the gate command is the same everywhere
├── {{ci}}/                 # thin matrix over supported platforms; runs the automation gate
├── modules/
│   ├── codegen/            # compile-time generation; no runtime, no I/O
│   ├── domain/             # entities, rules, ports; no I/O
│   ├── application/        # use cases over the domain and its ports; no runtime ownership
│   ├── platform/           # OS adapters for the ports; one module per OS
│   ├── infrastructure/     # shared adapters: network, storage, config, telemetry
│   ├── ui/                 # views and view-state; no business rules; reaches use cases through the handle app injects
│   ├── cli/                # command tree over the use cases; thin I/O wrapper; data on stdout, logs on stderr, nonzero exit on failure
│   ├── app/                # composition root: separate graphical and command entry points; the graphical entry is a windowed program; runtime start, observability start, wiring
│   ├── e2e/                # tests that cross module boundaries
│   └── benches/            # benchmarks, outside production builds
├── fuzz/                   # outside the default build; parsers, decoding, domain invariants
├── examples/               # runnable demos, smoke-checked with the gate
├── assets/                 # icons, schemas, fonts bundled with the build
├── packaging/              # installer metadata per platform, consumed by automation
│   ├── {{platform_a}}/
│   ├── {{platform_b}}/
│   └── {{platform_c}}/
└── automation/             # one verification pass, packaging, signing, generation, release
```

## Verification Pipeline

The checks every change passes before it is pushed, defined once in automation and run the same way on a local machine and in CI. The local run is the everyday gate and needs no cloud service. The CI run repeats the identical pass on each target platform as an independent final check.

| Check | Command (inside the automation gate) | Purpose |
|---|---|---|
| Format | `{{format_command}}` | Consistent formatting, no diffs |
| Lint | `{{lint_command}}` | Correctness, style, and performance lints treated as errors |
| Test | `{{test_command}}` | Unit, integration, and end-to-end tests |
| Dependency policy | `{{policy_command}}` | Advisories, licenses, bans, sources |
| Security audit | `{{audit_command}}` | Known vulnerabilities in dependencies |

## Platform Targets

The platforms the workspace builds, tests, and ships on. A platform counts as supported when it runs in the CI matrix.

| Platform | Typical targets | Package |
|---|---|---|
| {{platform_a}} | {{targets_a}} | {{package_a}} |
| {{platform_b}} | {{targets_b}} | {{package_b}} |
| {{platform_c}} | {{targets_c}} | {{package_c}} |

## Foundational Libraries

The libraries and tools the workspace builds on. Each row is a deliberate default for its concern.

| Library | Description |
|---|---|
| `{{runtime}}` | Task scheduling, I/O, timers, and channels. The runtime is initialized only in `modules/app`. |
| `{{serialization}}` | Serialization and deserialization. Shapes are declared in `modules/domain`. Execution sits in `modules/infrastructure` and `modules/cli`. |
| `{{observability}}` | Structured, span-aware observability and logging. |
| `{{typed_errors}}` | Typed, matchable errors for `modules/domain`, `modules/application`, `modules/platform`, and `modules/infrastructure`. |
| `{{contextual_errors}}` | Context-rich errors for entry points: `modules/app`, `modules/cli`, and `automation`. |
| `{{ui_toolkit}}` | Presentation framework and its native window shell. |
| `{{argument_parser}}` | Command-line argument parsing. |
| `{{benchmark_harness}}` | Benchmark harness, wrapped in `modules/benches`. |
| `{{fuzzer}}` | Coverage-guided fuzz testing. |
| `{{formatter}}` | Source formatter. |
| `{{linter}}` | Linter for correctness, style, and performance. |
| `{{dependency_policy}}` | Dependency policy: advisories, licenses, bans, sources. |
| `{{security_audit}}` | Audit of dependencies for known vulnerabilities. |

## Library Positions & Boundaries

Where each foundational library sits in the workspace map. **Owning layer** indicates where it is permitted, and a module not listed there should not depend on it directly. **Forbidden in** highlights where it must never appear to prevent architectural drift.

| Library | Owning layer | Forbidden in | Rationale |
|---|---|---|---|
| `{{runtime}}` | `modules/app` (runtime), `modules/application` (synchronization types), `modules/infrastructure` (I/O clients) | `modules/domain`, `modules/platform`, `modules/codegen` | The runtime is created once, at the edge in `app`. |
| `{{serialization}}` | `modules/domain` (shapes), `modules/infrastructure` (execution), `modules/cli` (output) | `modules/ui` | The domain defines shapes. Infrastructure and the command-line surface perform serialization. The view layer does not serialize. |
| `{{observability}}` | `modules/application`, `modules/infrastructure`, `modules/app` | `modules/domain` | Domain logic stays silent. Instrumentation sits on use cases and adapters. |
| `{{typed_errors}}` | `modules/domain`, `modules/application`, `modules/platform`, `modules/infrastructure` | `modules/app` | Libraries expose typed errors. Entry points wrap them at the boundary. |
| `{{contextual_errors}}` | `modules/app`, `modules/cli`, `automation` | `modules/domain`, `modules/application` | Libraries keep matchable errors. Context is added at the command-line and window edge. |
| `{{ui_toolkit}}` | `modules/ui`, `modules/app` (window launch) | `modules/domain`, `modules/application` | The presentation toolkit stays out of business logic and ports. `app` starts the window. |
| `{{argument_parser}}` | `modules/cli` | `modules/domain`, `modules/ui` | Argument parsing stays a command-line concern. |
| `{{benchmark_harness}}` | `modules/benches` | All others | Benchmarks stay isolated so production builds stay lean. |
| `{{fuzzer}}` | `fuzz/` | All others | Fuzz targets sit outside the default build. |
| `{{formatter}}` | `{{toolchain_pin}}`, `automation` | N/A | The automation gate runs it, locally and in CI. |
| `{{linter}}` | `{{manifest}}`, `automation` | N/A | The automation gate runs it, locally and in CI. |
| `{{dependency_policy}}` | `automation` | N/A | The automation gate checks policy. The product graph does not link it. |
| `{{security_audit}}` | `automation` | N/A | The automation gate audits dependencies. The product graph does not link it. |
