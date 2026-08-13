# FAQ

### Is Inazuma EVM compatible?
No. It has its own accounts (Ed25519 / base58) and its own JSON-RPC. Solidity
tooling and EVM wallets do not work; use [inazuma-sdk](https://github.com/inazuma-network/inazuma-sdk)
and the [Inazuma wallet](https://github.com/inazuma-network/inazuma-wallet).

### Can I import my Inazuma key into another wallet?
No, by design. Backups start with `inazkey1` and are rejected elsewhere, and key
derivation is domain-separated so the same words produce a different key here.

### What happens if I lose my 24 words?
The wallet is gone. Nobody — not the validators, not the developers — can restore
it. Write the words on paper and keep them offline.

### How fast is a transaction?
Blocks come every 400 ms, so inclusion is usually under a second. Finality
follows a few blocks later.

### What does a transaction cost?
The minimum fee is 1,000 rai (0.000001 INAZ). Fees rise only when blocks are
consistently full, via a dynamic base fee.

### Do I need special hardware to validate?
No GPU. A modern 4-core VPS with 8 GB RAM and NVMe storage runs comfortably; see
[validator.md](validator.md) for the sizing table.

### Can I lose stake by running a validator?
Yes, if you misbehave provably. Double-signing burns stake and permanently
tombstones the key; extended downtime causes jailing. Honest, online operation
is not slashed. See [staking.md](staking.md).

### Can someone build a rollup or an L2 on Inazuma?
Batch posting and trustless state proofs work today. A full rollup also needs an
on-chain proof verifier, a cheap expiring data-availability lane and a canonical
bridge — those are on the roadmap, not shipped.

### Is Inazuma quantum-safe?
Accounts are already bound to a quantum-resistant ML-DSA-65 key attached to every
transaction, so no migration is needed when enforcement is turned on. Until then,
Ed25519 is what the network verifies.

### Who runs the RPC endpoint?
`https://rpc.inazuma.network` is a public convenience endpoint with shared rate
limits. Anyone can run their own node and get a private, faster endpoint —
see [rpc-node.md](rpc-node.md).

### Is the code open source?
Yes, MIT, across the repos listed in the [README](../README.md).
