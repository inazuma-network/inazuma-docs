# Run an RPC node

An RPC node stays in sync with the chain and answers queries. It produces no
blocks, needs no stake, and can be run by anyone — for your own app, or as a
service for others.

## Why run one

- No shared rate limits, and latency measured in single-digit milliseconds.
- Full history and indexes under your control.
- Private mempool submission, so your transactions are not queued behind strangers.

## Requirements

| | Minimum | Comfortable |
| --- | --- | --- |
| CPU | 4 cores | 8 cores |
| RAM | 8 GB | 16 GB |
| Disk | 100 GB NVMe | 500 GB NVMe |
| Network | 100 Mbps | 1 Gbps, unmetered |

## Install

Use the same installer as a validator and answer *no* when it offers to stake:

```bash
curl -fsSL https://raw.githubusercontent.com/inazuma-network/inazuma-core/main/scripts/install-validator.sh | bash
```

Or start the binary directly in replica mode, which syncs and serves RPC without
producing blocks:

```bash
inazuma-core --replica --rpc-addr 0.0.0.0:9933 --ws-addr 0.0.0.0:9944
```

Full flags and systemd units: [validator.md](validator.md).

## Serving traffic

- Put a reverse proxy in front for TLS and per-IP limits.
- Run at least two replicas behind a load balancer so restarts are invisible.
- Cache hot read methods (`inaz_chainInfo`, `inaz_blockNumber`) for a few hundred ms.
- Use the WebSocket endpoint for `heads`, `finality`, `mempool` and `logs` instead of polling.

## Rate limiting and tiers

The node meters requests by cost, not just count:

| Tier | How | Budget |
| --- | --- | --- |
| Anonymous | no header | Shared, development-sized |
| Key | `x-api-key` | Higher, per key |
| Stake-weighted | bonded stake attached to the key | Scales with stake, up to 8x |
| Admin | admin key | Unmetered, node-local methods |

Accounts are separately throttled on transaction submission so one sender cannot
flood the mempool. Read your live budget with `inaz_rpcLimits`.

## Health checks

```bash
curl -s http://127.0.0.1:9933 -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"inaz_nodeStatus","params":[]}'
```

Alert when the height stops advancing for more than a few seconds, when peer count
drops to zero, or when the gap between the tip and finalized height keeps growing.
