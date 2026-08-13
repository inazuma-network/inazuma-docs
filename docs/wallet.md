# Wallet: install, back up, send, recover

## 1. Install

Two options:

| Option | Best for | How |
| --- | --- | --- |
| **Browser extension** | Everyday use, connecting to sites | [inazuma-wallet](https://github.com/inazuma-network/inazuma-wallet) → follow *Install (from source)* |
| **In-page wallet** | Trying things out, apps that embed a wallet | Any app built with [inazuma-sdk](https://github.com/inazuma-network/inazuma-sdk) |

## 2. Create and back up

1. Click **Create wallet**.
2. You are shown **24 words**. Write them on paper, in order. This is the only
   way to recover the wallet.
3. Set a password. It encrypts the wallet on this device only — it does not
   recover anything by itself.
4. Optionally export the `inazkey1…` key string to move the wallet between
   Inazuma apps.

**Never** type your words into a website, a chat, a support form or a screenshot.
No legitimate tool ever asks for them.

## 3. Receive

Copy your address (base58, e.g. `7Fh2…kQ9`) and share it. Need test INAZ? See
[faucet.md](faucet.md).

## 4. Send

1. Paste the recipient address — the wallet validates the format before enabling Send.
2. Enter the amount in INAZ. The fee defaults to the 1,000 rai minimum.
3. Confirm. Inclusion typically takes under a second.

If it fails:

| Message | Cause | Fix |
| --- | --- | --- |
| `insufficient balance` | Amount + fee exceeds balance | Send slightly less |
| `invalid nonce` | Two transactions signed with the same counter | Wait one block and retry |
| `fee below minimum` | Custom fee too low | Restore the default fee |
| `invalid address` | Wrong network's address | Inazuma addresses are base58, 32–44 chars |

## 5. Recover

Reinstall the wallet → **Import** → paste the 24 words or the `inazkey1…` key →
set a new password. The same address reappears with its balance and history.

Lost words and lost password together: the funds are unrecoverable. That is what
self-custody means.

## 6. Connecting to sites

When a site asks to connect, the wallet shows the origin and waits for approval.
Connections are per-site and revocable from the wallet. A **signature request** is
free and moves nothing; only a **transaction** moves funds — read the amount and
recipient before approving.
