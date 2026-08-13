# Build on Inazuma

## 1. Install the SDK

```bash
bun add github:inazuma-network/inazuma-sdk
```

Browser, Node 18+, Bun and edge runtimes are all supported; only `fetch` is required.

## 2. Read the chain

```ts
import { InazumaClient, formatInaz } from "@inazuma/sdk";

const inaz = new InazumaClient();                  // https://rpc.inazuma.network
const info = await inaz.chainInfo();
const rai  = await inaz.getBalance(address);
console.log(info.height, formatInaz(BigInt(rai)));
```

Amounts are always in **rai**. `1 INAZ = 1e9 rai`. Use `parseInaz("1.5")` to build
and `formatInaz(bigint)` to display — never floats.

## 3. Let users connect a wallet

Prefer the extension so your app never touches keys:

```ts
const { address } = await window.inazuma.connect();
```

Fall back to an in-page wallet with `createKeypair()` when the extension is absent.
Provider details: [inazuma-wallet/docs/provider-api.md](https://github.com/inazuma-network/inazuma-wallet/blob/main/docs/provider-api.md).

## 4. Sign users in without gas

Issue a nonce server-side, build the message with `buildSignInMessage`, have the
wallet sign it, then verify with `verifySignInSignature(address, message, signature)`.
Check the nonce once and reject messages older than five minutes.

## 5. Send a transaction

```ts
const account = await inaz.getAccount(address) as { nonce: number };
const tx = signTransfer({ secret, to, amountRai: parseInaz("1"), nonce: account.nonce });
await inaz.simulateTransaction(tx);      // free dry-run
const hash = await inaz.sendTransaction(tx);
await inaz.waitForTransaction(hash);
```

Batching many transactions? Track the nonce yourself and submit with
`sendTransactions`.

## 6. Live updates

```ts
subscribe("heads", (head) => setHeight(head.height));   // also: finality, mempool, logs
```

## 7. Trustless reads

Do not trust an RPC node for anything valuable: fetch a state proof with
`inaz_getProof` and verify it locally against the state root. See
[state-proofs.md](state-proofs.md).

## 8. Production checklist

- Run your own RPC node, or use an API key — shared anonymous limits are for development ([rpc-node.md](rpc-node.md)).
- Handle `RpcError` explicitly; show the node's message rather than a generic failure.
- Re-read nonces on failure instead of retrying blindly.
- Never place a secret key, phrase or `inazkey1` string in server code, logs or analytics.
- Display fees in INAZ, and never round a balance up.
