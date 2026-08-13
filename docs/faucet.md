# Faucet: get test INAZ

The faucet hands out small amounts of INAZ so you can pay fees while testing.

## Limits

| | |
| --- | --- |
| Per claim | 2 INAZ |
| Claims per day | 3 per address |
| Gap between claims | 3 hours |

Limits are enforced by the faucet contract on-chain, so retrying does not help.

## How to claim

1. Create a wallet ([wallet.md](wallet.md)) and copy your address.
2. Open the faucet page, paste the address, and claim.
3. Wait ~1 second, then refresh your balance. The claim returns a transaction
   hash you can look up on the explorer.

## If nothing arrives

| Symptom | Cause | Fix |
| --- | --- | --- |
| "Cooldown active" | Less than 3 hours since your last claim | Wait for the timer shown |
| "Daily limit reached" | 3 claims used in 24 h | Wait for the window to roll over |
| Hash returned, balance unchanged | You are reading a different address | Compare the address character by character |
| "Faucet empty" | The faucet balance ran out | Report it — it gets refilled |

Faucet INAZ is for testing fees and app flows. Run your own faucet or automate
claims for CI with [inazuma-faucet](https://github.com/inazuma-network/inazuma-faucet).
