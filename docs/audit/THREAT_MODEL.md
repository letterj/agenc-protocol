# Protocol Threat Model

This is the lightweight threat-model reference for the public protocol repo.

## Scope

It exists as the security reference that the fuzz harness points to.

## Core Invariants

- only valid state transitions should mutate protocol-owned accounts
- versioned protocol state must remain forward-migratable under explicit migration control
- private-completion payload fields must stay structurally consistent with the published journal model
- committed artifacts must match the built program surface; stale or hand-edited artifacts are a supply-chain risk

## Fuzz Harness Relationship

`programs/agenc-coordination/fuzz/` should treat this file as the human-readable statement of the invariants it is trying to protect.

