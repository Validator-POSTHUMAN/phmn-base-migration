# ADR-0002: Lock contract on Cosmos Hub

- **Status:** Stub — to be written after ADR-0001 is accepted
- **Parent:** [ADR-0001](0001-phmn-migration-to-base.md)

## Requirements from ADR-0001

- Accepts only `factory/cosmos146s5j3t7gh2g37ywm47dp8avhesu2htvjjaxq7z55e7xj0rq0k8q5qnjjy/PHMN`
  (6 decimals). Minimum lock amount.
- Lock records: monotonic `lock_id`, sender, Base address, amount, height, time.
- Base address validated as `0x` + 40 hex, non-zero, stored lowercase.
- First lock from a sender binds its Base address; a later lock with a
  different address is rejected (`EvmAddressMismatch { bound }`). Several
  senders may bind the same Base address. No reset.
- Irreversible: no refund path.
- `WithdrawForBurn` for the owner only; the SubDAO calls it together with
  `MsgBurn` in one proposal (`burn-from` is disabled on the Hub).
- Pause of new locks by the owner.
- Queries: config, lock by id, binding by Cosmos address, paginated locks from
  `lock_id`, totals (locked, withdrawn for burn).
- Owner and wasm-admin: Strategic Treasury SubDAO.

## To decide

Storage layout, minimum amount, event format, test plan (cw-multi-test).
