# Security model

## What secures the chain

| Layer | Mechanism |
| --- | --- |
| Accounts | Ed25519 signatures, base58 addresses, per-account nonces |
| Quantum posture | ML-DSA-65 (FIPS 204) co-signature attached to every transaction |
| Consensus | stake-weighted leader election + precommit finality |
| Economics | 1,000 INAZ minimum stake, 300-block unbonding, burn-and-tombstone for equivocation |
| Networking | encrypted P2P channel (X25519 + ChaCha20-Poly1305), peer-id pinning, inbound caps, peer scoring |
| RPC | tiered auth, cost-weighted rate limits, per-account submission throttles |
| State | sparse Merkle commitments so reads are verifiable without trusting a node |

## Activation heights

Some protections turn on at set heights so the network upgrades without a fork
scramble:

| Feature | Active from |
| --- | --- |
| Slashing and jailing enforcement | block 130,000 |
| Sparse Merkle state commitments / proofs | block 200,000 |

## Threats and answers

| Threat | Answer |
| --- | --- |
| Double-signing to fork the chain | Anyone submits evidence; stake burned, key tombstoned |
| Validator goes dark | Jailing removes it from the rotation until it recovers |
| Eclipse / partition attack | Encrypted transport, peer-id pinning, inbound connection caps, scoring |
| Mempool spam | Cost-based RPC metering plus per-account submission caps and fee-based eviction |
| Lying RPC node | State proofs verified client-side |
| Future quantum attacker | Accounts already carry a post-quantum key; enforcement needs no migration |

## Your responsibilities

**Users** — write down the 24 words offline, never share them, verify recipients.
**Validators** — one key on one machine, offline key backups, monitored uptime.
**Developers** — never handle user secrets, verify proofs for anything valuable,
re-read nonces instead of blind retries.

## Reporting a vulnerability

Open a private security advisory on the affected repository
([inazuma-core](https://github.com/inazuma-network/inazuma-core/security/advisories),
[inazuma-wallet](https://github.com/inazuma-network/inazuma-wallet/security/advisories),
[inazuma-sdk](https://github.com/inazuma-network/inazuma-sdk/security/advisories)).
Include reproduction steps, impact and affected versions. Please do not open
public issues for exploitable bugs.
