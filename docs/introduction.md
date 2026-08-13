# What is Inazuma?

Inazuma is a layer-1 blockchain: its own network of computers that agree, several
times per second, on one shared ledger. It is written from scratch in Rust — its
own block format, state machine, consensus, networking and JSON-RPC. It does not
run on top of another chain, and it is not an EVM clone.

## What that means in practice

- **Fast** — a new block every 400 ms, so a payment feels instant.
- **Cheap** — the minimum fee is 1,000 rai, i.e. 0.000001 INAZ.
- **Sovereign** — INAZ pays fees and secures the chain; no other chain's token is needed.
- **Its own accounts** — an address is an Ed25519 public key in base58. Keys from
  other networks do not work here, and Inazuma keys do not work there. That is
  deliberate: one secret cannot be leaked across ecosystems by accident.

## Key numbers

| | |
| --- | --- |
| Coin | INAZ, 9 decimals (smallest unit: rai) |
| Block time | 400 ms, up to 5,000 transactions per block |
| Finality | precommit finality from the validator set, a few blocks behind the tip |
| Measured throughput | ~2,500 tx/s sustained ingestion; 20,000–36,000 tx/s execution |
| Minimum stake to validate | 1,000 INAZ, 300-block unbonding |
| Contracts | WebAssembly (WASM) |

## What Inazuma is not

- Not a rollup or sidechain — there is no parent chain to fall back on.
- Not EVM compatible — Solidity tooling and MetaMask do not apply.
- Not finished — see [security model](security.md) for what is enforced today
  versus scheduled by activation height.

## Where to go next

- Hold and move INAZ: [Wallet](wallet.md)
- Help secure the chain: [Run a validator](validator.md)
- Build something: [Build on Inazuma](build.md)
- Understand the machinery: [Architecture](architecture.md)
