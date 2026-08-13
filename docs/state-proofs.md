# State proofs and light clients

## The problem

If your app asks an RPC node for a balance and simply believes the answer, that
node can lie. State proofs remove the trust.

## How it works

Account state lives in a sparse Merkle tree of depth 128. Each block commits to a
single **state root**. A proof is the account's leaf plus the sibling hashes on the
path to that root — anyone can recompute the root and compare.

| Call | Purpose |
| --- | --- |
| `inaz_stateRoot` | The committed root at a height |
| `inaz_getProof` | Leaf + path for an account |
| `inaz_verifyProof` | Server-side check (convenience) |

Verify locally instead — the point is not to trust the server:

```ts
import { fetchAndVerifyProof } from "@inazuma/sdk";

const { value, valid } = await fetchAndVerifyProof(client, address);
if (!valid) throw new Error("RPC node served an invalid proof");
```

Sparse-Merkle commitments activate at block **200,000**; proofs are unavailable
for earlier heights.

## What this enables

- **Light clients** — verify specific accounts while tracking only block headers.
- **Bridges** — a contract on another chain can accept Inazuma state without
  trusting an operator, given the header.
- **Auditable frontends** — show users a verified badge instead of "the API said so".

## Not yet available

On-chain verification of *other* chains' proofs (a ZK verifier precompile) and a
cheap expiring data-availability lane are roadmap items, not shipped. Full rollups
settling to Inazuma need both.
