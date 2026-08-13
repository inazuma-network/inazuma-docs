<h1 align="center">Inazuma Documentation</h1>

<p align="center">
  Every written guide for the <b>Inazuma</b> layer-1 blockchain, in one place.<br/>
  Start with your role, not with our architecture.
</p>

---

## Pick your path

| I am… | Start here | Time |
| --- | --- | --- |
| **New to Inazuma** | [What is Inazuma?](docs/introduction.md) | 4 min |
| **A user** with a wallet | [Wallet & first transaction](docs/wallet.md) | 10 min |
| **A validator** running a node | [Run a validator](docs/validator.md) | 30 min |
| **A developer** building an app | [Build on Inazuma](docs/build.md) | 15 min |
| **Staking INAZ** | [Staking, rewards & slashing](docs/staking.md) | 8 min |
| **Worried about quantum computers** | [Quantum resistance](docs/quantum.md) | 6 min |
| **Confused by a word** | [Glossary](docs/glossary.md) | — |

## All guides

**Basics**
- [Introduction](docs/introduction.md) — what the chain is, what it is not, key numbers
- [Glossary](docs/glossary.md) — every term in plain English
- [FAQ](docs/faq.md) — the questions people actually ask

**Using the network**
- [Wallet](docs/wallet.md) — install, back up, send, receive, recover
- [Faucet](docs/faucet.md) — get test INAZ
- [Staking](docs/staking.md) — delegation, rewards, unbonding, slashing risk

**Running infrastructure**
- [Run a validator](docs/validator.md) — hardware, install, keys, systemd, monitoring
- [Run an RPC node](docs/rpc-node.md) — replicas, caching, WebSockets, rate tiers

**Building**
- [Build on Inazuma](docs/build.md) — SDK quick start, reading state, sending transactions
- [RPC reference](docs/rpc.md) — every method, parameters, subscriptions, limits
- [Smart contracts](docs/contracts.md) — the WASM VM and how to deploy
- [State proofs](docs/state-proofs.md) — trustless reads and light clients

**Internals**
- [Architecture](docs/architecture.md) — blocks, consensus, state, networking
- [Security model](docs/security.md) — threat model, slashing, key hygiene
- [Quantum resistance](docs/quantum.md) — the ML-DSA-65 layer, what is live and what is staged

## Chain facts

| | |
| --- | --- |
| Chain | Inazuma, a sovereign layer-1 (nothing settles to another chain) |
| Coin | `INAZ`, 9 decimals, smallest unit `rai` |
| Block time | 400 ms |
| Minimum fee | 1,000 rai (0.000001 INAZ) |
| Accounts | Ed25519 keys, base58 addresses, ML-DSA-65 quantum co-signatures |
| Consensus | stake-weighted leader election with precommit finality |
| Contracts | WASM |
| Public RPC | `https://rpc.inazuma.network` · WS `wss://rpc.inazuma.network/ws` |

## Ecosystem

| Repo | Purpose |
| --- | --- |
| [inazuma-core](https://github.com/inazuma-network/inazuma-core) | The Rust L1 node: consensus, state, P2P, RPC |
| [inazuma-sdk](https://github.com/inazuma-network/inazuma-sdk) | TypeScript SDK for apps |
| [inazuma-wallet](https://github.com/inazuma-network/inazuma-wallet) | Wallet extension + injected provider |
| [inazuma-docs](https://github.com/inazuma-network/inazuma-docs) | These docs |
| [inazuma-faucet](https://github.com/inazuma-network/inazuma-faucet) | Test-INAZ faucet service |
| [inazuma-contracts](https://github.com/inazuma-network/inazuma-contracts) | WASM contract examples & tooling |

## Contributing

Docs live as plain Markdown under `docs/`. Fix anything unclear: open a pull
request, or an issue describing what confused you and where. Rules of the house —
short sentences, no jargon without a definition, every command copy-pasteable,
and every claim true of the current release.

MIT licensed.

---

## Why Inazuma exists

Inazuma is a sovereign layer 1 — our own consensus, state machine, networking and VM, not
a rollup or a fork. The goal is narrow and deliberate: **be the home chain for memes,
NFTs, collectibles, games and communities.**

That use case is high volume and low value per transaction. A 500-piece mint, a game
writing a move a second, a community handing out collectibles — none of them can pay
dollars in fees or wait seconds for a confirmation. So the whole design is bent around
being fast and near-free:

| | |
| --- | --- |
| Block time | 400 ms, finalised in the same block |
| Transfer fee | ~0.000001 INAZ — fractions of a cent |
| Throughput | ~2,500 tx/s ingest; 20k-36k tx/s execution in bench |
| Tokens & NFTs | first-class chain records — no contract needed to mint |
| Contracts | gas-metered WASM |
| Accounts | Ed25519, base58 addresses, optional ML-DSA-65 co-signature |
| Light clients | sparse Merkle state proofs |

Getting to top-tier means three things, in this order: enough independent validators that
nobody can stop the chain, tooling good enough that a first-time builder ships in an
afternoon, and fees that stay boring even when a collection goes viral. Every repo below
is one part of that.

## The Inazuma repos

| Repo | What's in it |
| --- | --- |
| [inazuma-core](https://github.com/inazuma-network/inazuma-core) | The Rust L1: consensus, state, staking, P2P, JSON-RPC, WASM VM |
| [inazuma-validator](https://github.com/inazuma-network/inazuma-validator) | Node operators: one-command installer, systemd units, health checks, full guide |
| [inazuma-sdk](https://github.com/inazuma-network/inazuma-sdk) | TypeScript client: RPC, keys, signing, sign-in, state proofs |
| [inazuma-wallet](https://github.com/inazuma-network/inazuma-wallet) | Self-custody wallet: browser extension, web and Android |
| [inazuma-contracts](https://github.com/inazuma-network/inazuma-contracts) | WASM contract examples, host ABI and deploy scripts |
| [inazuma-faucet](https://github.com/inazuma-network/inazuma-faucet) | Test-token faucet service |
| **inazuma-docs** (here) | All written guides, organised by role |
| [inazuma-improvement-proposals](https://github.com/inazuma-network/inazuma-improvement-proposals) | INAZIPs — how the chain changes |

## Getting started, whoever you are

| I want to… | Go to |
| --- | --- |
| Use a wallet and send INAZ | [inazuma-wallet](https://github.com/inazuma-network/inazuma-wallet) |
| Get test INAZ | [inazuma-faucet](https://github.com/inazuma-network/inazuma-faucet) |
| Build an app | [inazuma-sdk](https://github.com/inazuma-network/inazuma-sdk) · [inazuma-contracts](https://github.com/inazuma-network/inazuma-contracts) |
| Run a node or stake | [inazuma-validator](https://github.com/inazuma-network/inazuma-validator) |
| Understand the internals | [inazuma-core](https://github.com/inazuma-network/inazuma-core) |
| Propose a protocol change | [INAZIPs](https://github.com/inazuma-network/inazuma-improvement-proposals) |
