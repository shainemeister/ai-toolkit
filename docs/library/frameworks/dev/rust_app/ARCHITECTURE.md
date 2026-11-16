# Architecture

Copy this file onto the repository root as `ARCHITECTURE.md`. Law at that root is `kit/RULES.md`. `kit/` enforces the root file and does not rewrite it.

## Summary

An architectural map for Rust application development, scoped to native desktop applications on Windows, macOS, and Linux. It outlines a layered workspace that keeps domain logic at the center, adapters and user-facing surfaces at the edges, and a single composition root that assembles them, alongside the foundational libraries and tooling the layout builds on and where each typically fits.

`{{app}}` stands for the project name. Folder names stay as shown (`core/`, `macros/`, …), while package names take the form `{{app}}-<crate>` (for example `{{app}}-core`), since a plain `core` clashes with Rust's built-in `core` crate.

## Workspace Map

```text
{{app}}/
├── Cargo.toml              # virtual [workspace], resolver = "3", members = ["crates/*", "xtask"], exclude = ["fuzz"], [workspace.package] edition = "2024", rust-version = "1.85", [workspace.dependencies] (tokio, serde, tracing, thiserror, anyhow, egui/eframe, clap), shared lints (clippy)/profiles
├── Cargo.lock              # committed
├── rust-toolchain.toml     # pinned stable toolchain + per-OS targets (see Platform Targets); clippy + rustfmt components
├── .cargo/config.toml      # cargo alias: xtask = "run --package xtask --", so `cargo xtask ci` works the same everywhere
├── .github/workflows/      # thin CI matrix (Windows, macOS, Linux runners): installs the pinned toolchain plus cargo-deny and cargo-audit, then runs `cargo xtask ci`; the final, independent run of the local pass
├── crates/
│   ├── macros/             # proc-macro crate: derives + attributes; no runtime deps, no std I/O
│   ├── core/               # domain: entities, rules, ports (traits). No I/O. serde types (derive only, no serializer calls), thiserror errors
│   ├── services/           # use cases orchestrating core + ports; pure async fn, no spawning or runtime; tracing spans, thiserror errors
│   ├── platform/           # OS adapters implementing ports; per-OS modules (windows.rs, macos.rs, linux.rs) behind cfg(target_os); per-OS deps under [target.'cfg(...)'.dependencies]; unique OS APIs (keychain, clipboard); thiserror errors
│   ├── infra/              # uniform adapters: network, storage, config, telemetry; implements core ports; thiserror errors
│   ├── ui/                 # egui/eframe views + view-state; no business rules; talks to services only through the handle app injects
│   ├── cli/                # clap command tree -> services; thin I/O wrapper; data on stdout, logs on stderr, nonzero exit on error; human/JSON output formatting
│   ├── app/                # composition root: separate GUI and CLI binaries (only the GUI sets windows_subsystem = "windows"); tokio runtime init, tracing init, anyhow at the edge, wiring
│   ├── e2e/                # end-to-end integration tests across crates (workspace member)
│   └── benches/            # criterion benchmarks (workspace member)
├── fuzz/                   # cargo-fuzz targets (parsers, deserialization, domain invariants); excluded from workspace, run with cargo +nightly fuzz
├── examples/               # runnable demos, smoke-tested in CI
├── assets/                 # icons, schemas, fonts (bundled via include_bytes! or build.rs; paths built from CARGO_MANIFEST_DIR)
├── packaging/              # per-OS installer metadata, consumed by xtask
│   ├── windows/            # MSI definition, icon, code-signing config
│   ├── macos/              # Info.plist, entitlements, signing + notarization config
│   └── linux/              # .desktop entry, AppStream metadata, .deb / AppImage config
└── xtask/                  # repo automation: `cargo xtask ci` (fmt, clippy, test, cargo-deny, cargo-audit; one pass, locally and in CI), per-OS packaging + signing, codegen, release
```

## Verification Pipeline

The checks every change passes before it is pushed, defined once in `xtask` and run the same way on a local machine and in CI. The local run is the everyday gate and needs no cloud service; the CI run repeats the identical pass on each target OS as an independent final check.

| Check | Command (inside `cargo xtask ci`) | Purpose |
|---|---|---|
| Format | `cargo fmt --all --check` | Consistent formatting, no diffs |
| Lint | `cargo clippy --workspace --all-targets -- -D warnings` | Correctness, style, and performance lints treated as errors |
| Test | `cargo test --workspace` | Unit, integration, and `e2e` tests |
| Dependency policy | `cargo deny check` | Advisories, licenses, bans, sources |
| Security audit | `cargo audit` | Known vulnerabilities from the RustSec database |

## Platform Targets

The desktop targets the workspace builds, tests, and ships on. An OS counts as supported when it runs in the CI matrix.

| OS | Typical Targets | Package |
|---|---|---|
| Windows | `x86_64-pc-windows-msvc`, `aarch64-pc-windows-msvc` | Signed MSI |
| macOS | `aarch64-apple-darwin`, `x86_64-apple-darwin` | Signed and notarized `.app` in a `.dmg` |
| Linux | `x86_64-unknown-linux-gnu`, `aarch64-unknown-linux-gnu` | `.deb` and AppImage |

## Foundational Libraries

The core libraries and tools every crate in the workspace builds on. Each one is a deliberate default for its concern.

| Library | Description |
|---|---|
| `tokio` | Async runtime: task scheduling, I/O, timers, channels (runtime initialized only in `app`) |
| `serde` | Serialization and deserialization framework (derives allowed in `core`, execution in `infra` and `cli`) |
| `tracing` | Structured, span-aware observability and logging |
| `thiserror` | Typed, matchable error enums for library crates (`core`, `services`, `platform`, `infra`) |
| `anyhow` | Flexible, context-rich error type for binaries (`app`, `cli`, `xtask`) |
| `egui` / `eframe` | Immediate-mode UI framework and its native app shell |
| `clap` | Command-line argument parsing (derive-based) |
| `criterion` | Statistical benchmarking harness (wrapped in `crates/benches`) |
| `cargo-fuzz` | Coverage-guided fuzz testing (libFuzzer) |
| `rustfmt` | Standard Rust code formatter |
| `clippy` | Rust linter for correctness, style, and performance |
| `cargo-deny` | Dependency policy checks: advisories, licenses, bans, sources |
| `cargo-audit` | Security audit of dependencies against the RustSec advisory database |

## Library Positions & Boundaries

Where each foundational library sits in the workspace map. **Owning Layer** indicates where it is permitted, and a crate not listed there should not depend on it directly. **Forbidden In** highlights where it must never appear to prevent architectural drift.

| Library | Owning Layer | Forbidden In | Rationale |
|---|---|---|---|
| `tokio` | `crates/app` (runtime), `crates/services` (sync types only), `crates/infra` (I/O clients, no runtime) | `crates/core`, `crates/platform`, `crates/macros` | Runtime is created once, at the edge in `app`. |
| `serde` | `crates/core` (derives), `crates/infra` (execution), `crates/cli` (output formatting) | `crates/ui` | Core defines shapes; infra and cli perform serialization. UI never serializes directly. |
| `tracing` | `crates/services`, `crates/infra`, `crates/app` | `crates/core` | Core logic stays silent; instrumentation happens at use cases and adapters. |
| `thiserror` | `crates/core`, `crates/services`, `crates/platform`, `crates/infra` | `crates/app` | Libraries use typed errors; binaries wrap them in `anyhow` at the boundary. |
| `anyhow` | `crates/app`, `crates/cli`, `xtask` | `crates/core`, `crates/services` | Libraries keep matchable errors; rich context is added at the CLI/UI edge. |
| `egui` / `eframe` | `crates/ui`, `crates/app` (window launch only) | `crates/core`, `crates/services` | UI framework never leaks into business logic or ports; app only starts the window. |
| `clap` | `crates/cli` | `crates/core`, `crates/ui` | Argument parsing is strictly a CLI concern. |
| `criterion` | `crates/benches` | All others | Benchmarks are isolated to keep production builds lean. |
| `cargo-fuzz` | `fuzz/` | All others | Fuzz targets sit outside the standard build graph. |
| `rustfmt` | `rust-toolchain.toml` (component), `xtask` | N/A | Run by `cargo xtask ci`, locally and in CI. |
| `clippy` | `Cargo.toml` (config), `xtask` | N/A | Run by `cargo xtask ci`, locally and in CI; not a code dependency. |
| `cargo-deny` | `xtask` | N/A | Run by `cargo xtask ci`; dependency policy is checked, not linked. |
| `cargo-audit` | `xtask` | N/A | Run by `cargo xtask ci`; security audits are external checks, not runtime deps. |
