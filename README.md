# EFBA26

Rust workspace for DRM research, simulation, benchmarking, packaging/sealing, licensing, demos, and synthesized-data experiments.

## Status

- **Maturity:** architectural prototype / research workspace
- **Default branch:** `main`
- **Primary risk:** research evidence, generated artifacts, demos, and product-grade controls currently share one repository boundary

## Workspace layout

The root `Cargo.toml` declares these members:

- `sim` — simulation work
- `game` — game-facing implementation
- `bench` — benchmark tooling
- `drm` — DRM logic
- `seal-cli` — packaging/sealing command-line surface
- `license` — licensing service or library surface
- `game3d` — 3D demonstration surface
- `synth` — synthesized dataset generation
- `docs/` — architecture and supporting documentation

## Prerequisites

- Stable Rust toolchain with Cargo
- Platform toolchain required by any graphics or system dependencies

## Build and test

```bash
cargo build --workspace
cargo test --workspace
```

For optimized benchmarks or demos:

```bash
cargo build --workspace --release
```

Run package-specific commands from the workspace root with `-p <package>` after confirming the package's documented inputs.

## Development workflow

1. Keep shared contracts in the narrowest reusable crate.
2. Separate benchmarks from claims about production security or performance.
3. Generate datasets deterministically and record generator version, parameters, and seed.
4. Keep generated output out of source control unless it is a deliberately reviewed fixture.
5. Run workspace tests before opening a pull request.

## Evidence and security boundaries

This repository must not imply that a prototype DRM mechanism is production-secure without an explicit threat model and independent review.

- Never commit signing keys, license-service credentials, production secrets, or customer data.
- Document attacker capabilities, trust boundaries, revocation behavior, offline behavior, and failure modes.
- Benchmark results must include hardware, toolchain, build profile, sample size, and reproducible commands.
- Synthesized data must be clearly labeled and must not be mixed with observed production data.

## Release expectations

A releasable artifact requires:

- Pinned toolchain/dependencies
- Reproducible build instructions
- Threat model and known limitations
- Test and benchmark evidence
- Artifact provenance and rollback/revocation plan

## Known limitations

- Broad workspace scope can obscure which components are research, demo, benchmark, or production candidates.
- Generated data and benchmark outputs need stronger provenance discipline.
- A root-level release contract is not yet established.

## Ownership

Kri Zek research and engineering repository. Security-sensitive claims require explicit evidence and review; this README is not a security certification.
