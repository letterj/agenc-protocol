# Protocol Codebase Map

This file maps the full `agenc-protocol` repo for developers and AI agents.

## Top-Level Layout

```text
agenc-protocol/
  programs/agenc-coordination/   Anchor program source of truth
  artifacts/anchor/              committed canonical IDL, types, and manifest
  packages/protocol/             published npm artifact package
  migrations/                    migration notes and helpers
  scripts/                       artifact sync and verifier-router support
  zkvm/guest/                    public zkVM journal helper crate
  docs/                          repo-level developer docs
  .github/workflows/             CI automation
  README.md
  package.json
  Anchor.toml
```

## Path Ownership

### Program surface

- `programs/agenc-coordination/src/lib.rs` - instruction entrypoints
- `programs/agenc-coordination/src/state.rs` - PDA/account model and version constants
- `programs/agenc-coordination/src/events.rs` - emitted events
- `programs/agenc-coordination/src/errors.rs` - protocol error codes
- `programs/agenc-coordination/src/instructions/` - instruction handlers and helpers
- `programs/agenc-coordination/src/utils/` - shared utilities
- `programs/agenc-coordination/fuzz/` - property/invariant harness

### Canonical artifacts

- `artifacts/anchor/idl/agenc_coordination.json`
- `artifacts/anchor/types/agenc_coordination.ts`
- `artifacts/anchor/manifest.json`
- `scripts/idl/verifier_router.json`

### Published package

- `packages/protocol/src/index.ts` - package barrel
- `packages/protocol/src/generated/` - generated copies synced from the canonical artifacts

### Migration and zk surfaces

- `migrations/` - migration notes and helpers
- `zkvm/guest/src/lib.rs` - canonical journal field layout for private completion

### Automation

- `scripts/sync-anchor-artifacts.mjs` - `target/` to committed artifact sync
- `scripts/sync-package-protocol-assets.mjs` - committed artifacts to npm package sync
- `.github/workflows/ci.yml` - formatting, artifact verification, package build, typecheck, and pack smoke

## Ownership Boundaries

- This repo owns the public protocol source of truth.
- Runtime/product implementation belongs in `agenc-core`.
- SDK consumer helpers belong in `agenc-sdk`.
- Plugin ABI belongs in `agenc-plugin-kit`.
- Proving server and private admin tools belong in `agenc-prover`.

## Start Here By Change Type

- New instruction or PDA change: `programs/agenc-coordination/src/` and [PROGRAM_SURFACE.md](./PROGRAM_SURFACE.md)
- IDL or package artifact change: [ARTIFACT_PIPELINE.md](./ARTIFACT_PIPELINE.md)
- ZK or private-completion change: [ZK_PRIVATE_FLOW.md](./ZK_PRIVATE_FLOW.md)
- CI/toolchain change: [VALIDATION.md](./VALIDATION.md)

