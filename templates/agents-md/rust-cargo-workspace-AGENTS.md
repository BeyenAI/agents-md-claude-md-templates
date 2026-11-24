# AGENTS.md — Rust Cargo Workspace
<!-- Generated & linted with https://findaitier.com/agents-md-generator/ (Codex 32 KiB budget: ~1.4 KiB / 4.3%) -->

## Build, Lint & Test Commands
- **Fast compile check**: `cargo check --workspace --all-targets`
- **Run single crate tests (preferred)**: `cargo test -p <crate_name> -- <test_filter>`
- **Strict lint**: `cargo clippy --workspace --all-targets --all-features -- -D warnings`
- **Format check**: `cargo fmt --all -- --check`

## Workspace Layout
- `crates/core/` — Domain types, traits, and deterministic state machine (no network or filesystem I/O).
- `crates/server/` — Axum HTTP/gRPC server and Tokio runtime wiring.
- `crates/storage/` — SQLx Postgres repository implementations.

## Rust Conventions
- Never use `.unwrap()` or `.expect()` in production crate paths (`crates/*/src/`); propagate typed errors with `thiserror` in libraries and `anyhow::Context` in binary entrypoints.
- Keep `crates/core` free of Tokio runtime dependencies so unit tests execute synchronously in milliseconds.
- Every bug fix must include a regression test in the affected crate and pass `cargo clippy --workspace --all-targets -- -D warnings`.
