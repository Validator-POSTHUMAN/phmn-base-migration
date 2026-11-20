# ADR-0003: Claim contract and token on Base

- **Status:** Stub — to be written after ADR-0001 is accepted
- **Parent:** [ADR-0001](0001-phmn-migration-to-base.md)

## Requirements from ADR-0001

- **Token:** ERC-20, fixed supply 131,072, 6 decimals, no mint, no owner; the
  whole supply is sent to the claim contract at deployment.
- **Claim contract:** cumulative merkle root; leaf `(account, totalOwed)`;
  contract stores `claimed[account]` and pays `totalOwed − claimed`.
- New root: proposed by the Safe, active after a delay (24–48 h); guardian can
  cancel a pending root.
- Pause by guardian, unpause by owner; pause blocks claims and root changes.
- Upgradeable (UUPS). Upgrades and owner changes go through a
  `TimelockController` (~7 days, Safe as proposer/executor, guardian as
  canceller). No sweep or rescue function.
- `claimFor(account, ...)` allowed; tokens always go to `account`.
- Events for every root proposal, activation, cancellation and claim.

## To decide

Leaf encoding (match OpenZeppelin `MerkleProof`, double-hash), whether a root
carries an epoch number and the source Hub height/`lock_id`, storage layout,
test plan (Foundry).
