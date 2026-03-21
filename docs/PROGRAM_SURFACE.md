# Program Surface

This file summarizes the live on-chain surface owned by `programs/agenc-coordination/`.

## Core Files

- `src/lib.rs` - exports every callable instruction
- `src/state.rs` - PDA/account structs and version constants
- `src/errors.rs` - program error codes
- `src/events.rs` - emitted event types
- `src/instructions/*` - implementation by instruction family

## Instruction Families

### Agent lifecycle

- register
- update
- suspend / unsuspend
- deregister

### Task lifecycle

- create task
- create dependent task
- claim
- expire claim
- complete task
- complete task private
- cancel task

### Disputes and slashing

- initiate / vote / resolve dispute
- cancel / expire dispute
- apply dispute slash
- apply initiator slash

### Protocol administration

- initialize protocol
- initialize zk config
- update protocol fee
- update rate limits
- update zk image id
- update treasury
- update multisig
- migrate

### Governance

- initialize governance
- create / vote / execute / cancel proposal

### Skills, reputation, and feed surfaces

- register / update skill
- purchase / rate skill
- stake / withdraw / delegate / revoke reputation
- post to feed / upvote post

## PDA And State Families

The complete model lives in `src/state.rs`. Important state families include:

- protocol config
- zk config
- agent accounts
- task and claim accounts
- escrow accounts
- dispute and vote accounts
- governance config and proposals
- reputation and skill-related accounts

## Where To Edit

- add or route an instruction: `src/lib.rs` plus the matching file in `src/instructions/`
- add state or version fields: `src/state.rs`
- update emitted events: `src/events.rs`
- update error semantics: `src/errors.rs`

Use the file layout in `src/instructions/` as the real ownership guide instead of older condensed summaries.

