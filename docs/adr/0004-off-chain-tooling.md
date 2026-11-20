# ADR-0004: Off-chain tooling

- **Status:** Stub — to be written after ADR-0001 is accepted
- **Parent:** [ADR-0001](0001-phmn-migration-to-base.md)

## Requirements from ADR-0001

- **Builder:** reads all locks from the lock contract, aggregates by Base
  address into cumulative totals, builds the merkle tree deterministically,
  outputs the root, all proofs and a Safe Transaction Builder JSON.
- **Checker:** run by every signer before signing; rebuilds the tree
  independently from Cosmos Hub data and fails if the root differs, if any
  wallet's total decreased versus the previous root, or if the tree total
  differs from the total locked.
- **Publishing:** proofs on IPFS and GitHub for every root; the build script is
  open so anyone can reproduce them.
- **Monitor:** alerts on any change of PHMN supply on Cosmos Hub, on the lock
  contract balance and on pending roots/upgrades on Base.
- **Frontend:** lock page (Keplr/Leap; Base address from the connected EVM
  wallet; binding check before signing; irreversibility confirmation) and claim
  page (owed / pending / claimed).

## To decide

Epoch length, hosting, stack, CI.
