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
- [Security model](docs/security.md) — threat model, slashing, quantum posture

## Chain facts

| | |
| --- | --- |
| Chain | Inazuma, a sovereign layer-1 (nothing settles to another chain) |
| Coin | `INAZ`, 9 decimals, smallest unit `rai` |
| Block time | 400 ms |
| Minimum fee | 1,000 rai (0.000001 INAZ) |
| Accounts | Ed25519 keys, base58 addresses |
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
