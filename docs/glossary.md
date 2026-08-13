# Glossary

Plain-English definitions. No prior blockchain knowledge assumed.

| Term | Meaning |
| --- | --- |
| **Address** | Your public account name, e.g. `7Fh2…kQ9`. Safe to share. It is your Ed25519 public key written in base58. |
| **Base58** | A way of writing bytes as letters and digits that avoids look-alike characters (no `0`, `O`, `I`, `l`). |
| **Block** | A batch of transactions agreed by the network. Inazuma makes one every 400 ms. |
| **Block reward** | New INAZ paid to the validator that produced a block. |
| **Ed25519** | The signature system Inazuma accounts use. Small, fast, well studied. |
| **Epoch** | A fixed window of blocks used for validator-set and reward bookkeeping. |
| **Faucet** | A service that gives out small amounts of INAZ for testing. |
| **Fee** | What you pay to have a transaction included. Minimum 1,000 rai. |
| **Finality** | The point where a block can no longer be reversed. Inazuma reaches it via validator precommits. |
| **Genesis** | Block zero: the agreed starting state of the chain. |
| **INAZ** | The native coin. Pays fees, earns rewards, secures the chain. |
| **Jailing** | Temporarily removing a validator from block production, usually for being offline. |
| **Mempool** | The waiting room for transactions that have been submitted but not yet included in a block. |
| **ML-DSA-65** | A quantum-resistant signature standard (FIPS 204). Inazuma attaches it alongside Ed25519. |
| **Nonce** | A per-account counter that stops a transaction from being replayed. Each transaction uses the next number. |
| **Precommit** | A validator's vote that a block is valid; enough precommits finalize it. |
| **rai** | The smallest unit of INAZ. 1 INAZ = 1,000,000,000 rai. |
| **Replica / RPC node** | A node that stays in sync and answers queries but does not produce blocks. |
| **RPC** | The API apps use to read the chain and submit transactions. |
| **Slashing** | Burning part of a validator's stake as a penalty for provable misbehaviour. |
| **Sparse Merkle tree** | The structure that lets anyone prove a single account's state without downloading the chain. |
| **Stake** | INAZ locked by a validator (or delegated to one) as collateral for honest behaviour. |
| **State root** | A single hash summarizing all account state at a block. |
| **Tombstoning** | Permanently banning a validator key after a serious offence such as double-signing. |
| **Unbonding** | The waiting period (300 blocks) before unstaked INAZ becomes spendable. |
| **Validator** | A computer that produces and votes on blocks, backed by stake. |
| **WASM** | WebAssembly — the format smart contracts are compiled to. |
