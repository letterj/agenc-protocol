# Artifact Pipeline

This file describes how protocol artifacts move from local build output to committed and published surfaces.

## Canonical Flow

```text
anchor build
  -> local target/ output
  -> scripts/sync-anchor-artifacts.mjs
  -> artifacts/anchor/*
  -> scripts/sync-package-protocol-assets.mjs
  -> packages/protocol/src/generated/*
  -> npm package build / dist
```

## Rules

- `target/` is local build output, not the public contract
- `artifacts/anchor/*` is the committed canonical public artifact surface
- `packages/protocol/src/generated/*` is a derived copy used to publish `@tetsuo-ai/protocol`
- `scripts/idl/verifier_router.json` is repo-owned verifier-router support data and belongs in the committed public surface

## Commands

After a successful `anchor build`:

```bash
npm run artifacts:refresh
```

To verify that committed artifacts still match the current build and package copies:

```bash
npm run artifacts:check
```

## Consumer Guidance

Downstream repos should consume released protocol artifacts from:

- this repo's committed artifact surface, or
- the published `@tetsuo-ai/protocol` package

They should not treat local `target/` files or vendored copies in other repos as canonical.

