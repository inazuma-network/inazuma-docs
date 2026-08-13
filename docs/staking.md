# Staking, rewards and slashing

## Why stake

Validators lock INAZ as collateral. Block production rights are weighted by stake,
so honest validators earn rewards and dishonest ones lose collateral. Staking is
what makes attacking the chain expensive.

## Numbers

| | |
| --- | --- |
| Minimum stake | 1,000 INAZ |
| Unbonding period | 300 blocks (~2 minutes) |
| Rewards | Block reward + fees, paid to the block producer |
| Selection | Stake-weighted deterministic leader election per slot |

## Bonding

Staking is a transaction from the validator's key. The node's install script sets
it up; the manual sequence is in [validator.md](validator.md).

Unstaking has two steps: request the unbond, then wait out the unbonding period
before the INAZ becomes spendable. This delay is what makes slashing enforceable —
a validator cannot misbehave and instantly withdraw.

## Slashing: what is punished

| Offence | Detection | Penalty |
| --- | --- | --- |
| **Double-signing (equivocation)** | Two conflicting signed blocks at the same height, reported by anyone | Portion of stake burned + key permanently tombstoned |
| **Extended downtime** | Missing more than half the slots in the measurement window | Jailed for 10,000 blocks, no rewards while jailed |

Worked example: a validator with 100,000 INAZ bonded double-signs one block. A
5% equivocation penalty burns 5,000 INAZ, the remaining stake begins unbonding,
and the key can never validate again — a new key and fresh stake are required.

Being briefly offline for a restart is not slashed; sustained absence is jailed,
not burned.

## Reporting misbehaviour

Anyone can submit evidence with `inaz_reportEquivocation`, and
`inaz_previewSlash` shows the penalty that evidence would produce before you
submit it. Read the live parameters with `inaz_slashing`.

## Risk checklist before staking

- Run one validator per key. Never run the same key on two machines — that is
  exactly how double-signing happens.
- Back up the validator key offline; losing it means losing the ability to unbond.
- Monitor uptime and alert on missed slots (see [validator.md](validator.md)).
- Restart during your own maintenance window; a few missed blocks cost rewards, not stake.
