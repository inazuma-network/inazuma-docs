# Quantum resistance

## The short answer

Inazuma is **quantum-ready, not yet quantum-enforced.**

| | Status |
| --- | --- |
| Every account already has a quantum-safe key | Yes — derived automatically, no action from you |
| Every transaction already carries a quantum-safe signature | Yes — attached next to the classical one |
| Nodes currently *require* that signature to be valid | Not yet — enforcement turns on at a future block height |
| Your backup phrase already covers the quantum key | Yes — one backup, both keys |

So nothing is being promised for later that you have to migrate into. The keys and
signatures exist in the wire format today; the last step is nodes rejecting
transactions without them, which is a consensus change and happens at an announced
activation height.

## What the quantum problem actually is

Almost every blockchain today proves ownership with elliptic-curve signatures —
Ed25519 or secp256k1. Their security rests on one assumption: given a public key,
you cannot work backwards to the private key.

For a normal computer that is true, and will stay true. For a large
**cryptographically relevant quantum computer** it is not. Shor's algorithm solves
exactly the maths that elliptic curves rely on. A machine big enough to run it on
256-bit curves does not exist publicly today, and credible estimates put it years
away — but "years away" is a bad thing to bet a chain's entire history on, for two
reasons:

1. **Public keys are already exposed.** The moment you send one transaction, your
   public key is on the chain forever. An attacker does not need to be fast; they
   need to be patient. This is called *harvest now, decrypt later*.
2. **Old coins never move.** Wallets that have been dormant for years cannot be
   asked to upgrade. If a chain only fixes this after the fact, those balances are
   permanently exposed.

Signing with a quantum-safe scheme *before* the machine exists is the only version
of this that works.

## What Inazuma does

### One secret, two keys

Your wallet holds a single 32-byte master secret (what your backup phrase and your
`inazkey1` export represent). From it, two independent signing keys are derived
using **domain separation** — the secret is hashed together with a fixed label
before each derivation:

```text
master secret (32 bytes)
   │
   ├── hash( "inazuma/v2/ed25519"    ‖ master ) ──► Ed25519 key      (classical, fast, small)
   └── hash( "inazuma/v2/pq-mldsa65" ‖ master ) ──► ML-DSA-65 key    (quantum-safe, FIPS 204)
```

Domain separation matters: knowing one derived key tells you nothing about the
other, and the master secret itself is not a usable key on any other network. Your
`inazuma` backup cannot be imported anywhere else, and no other chain's key becomes
an Inazuma key by accident.

### Every transaction is dual-signed

When you send a transaction, your wallet signs the same canonical message twice and
attaches both:

```json
{
  "kind": "transfer",
  "from": "...", "to": "...", "amount": "...", "nonce": 7,
  "pubkey":       "<ed25519 public key>",
  "signature":    "<ed25519 signature>",
  "pq_scheme":    "ml-dsa-65",
  "pq_pubkey":    "<ML-DSA-65 public key>",
  "pq_signature": "<ML-DSA-65 signature>"
}
```

Today nodes verify the Ed25519 signature and carry the quantum fields through into
the block, so they become part of chain history. That is the important part: the
proof that *you* — holder of a lattice-based key, not just a curve key — authorised
that transaction is recorded permanently, starting now, not starting on the day
someone announces a quantum breakthrough.

### Why ML-DSA-65

ML-DSA (formerly CRYSTALS-Dilithium) is the signature scheme standardised by NIST as
**FIPS 204** in 2024, after a multi-year public competition. Its security rests on
lattice problems, which Shor's algorithm does not solve and for which no efficient
quantum attack is known.

Parameter set 65 is the middle security level — roughly comparable to AES-192 —
chosen because the top level costs more bytes per transaction without addressing a
threat the middle level fails against.

| | Ed25519 | ML-DSA-65 |
| --- | --- | --- |
| Public key | 32 bytes | 1,952 bytes |
| Signature | 64 bytes | 3,309 bytes |
| Safe against a quantum computer | No | Yes, as far as is known |
| Verification cost | Very cheap | Cheap, but heavier |

The size difference is exactly why enforcement is staged rather than instant: a
quantum-only transaction is ~50× larger than a classical one, so block-space,
mempool and bandwidth limits all have to be sized for it before it becomes
mandatory. That work is a protocol change, not a wallet change.

## The plan, honestly

| Phase | What happens | State |
| --- | --- | --- |
| 1. Derive | Every account gets a quantum key from the same backup | Done |
| 2. Attach | Wallets dual-sign; quantum signatures are stored in blocks | Done |
| 3. Verify | Nodes verify the quantum signature when present, and reject an invalid one | Next |
| 4. Bind | An account can publish its quantum key and forbid classical-only spends | Planned |
| 5. Enforce | At an activation height, quantum signatures become mandatory | Planned |
| 6. Consensus keys | Validator identity and block signing move to a hybrid scheme | Researching |

Phases 3–5 change consensus, so each one ships as a proposal in
[inazuma-improvement-proposals](https://github.com/inazuma-network/inazuma-improvement-proposals)
with an activation block, and old blocks keep validating under the rules they were
made under.

## What this does not protect you from

Being honest about scope matters more than the marketing line:

- **A stolen backup phrase.** Quantum-safe or not, whoever holds your secret is you.
  Hashing does not help if the input is copied.
- **Signing a malicious transaction.** Cryptography confirms you approved it; it does
  not judge whether approving it was smart.
- **A compromised device or a fake wallet page.** Keys are only as safe as the machine
  they are used on.
- **Symmetric-crypto panic.** Hashes (SHA-256) and AES are *not* broken by quantum
  computers in the same way; Grover's algorithm at best halves their effective
  strength, which the sizes in use already account for. The block hashes and state
  root do not need replacing.
- **A quantum computer that exists tomorrow.** Phases 3–5 are not finished. Until
  enforcement is live, an attacker with a working machine could still forge a
  classical-only signature. The difference is that the migration path is already
  built into every existing account instead of needing a chain-wide key change.

## Checking your own quantum key

Your quantum public key has a short fingerprint you can view in the wallet. Two
things worth knowing:

- It is derived, never stored separately — restoring your backup phrase restores it.
- Legacy raw-hex keys imported from before the `inazkey1` format have no quantum
  half. Move funds to a freshly generated Inazuma account to get one.

## Further reading

- [Architecture](architecture.md) — where keys sit in the wider design
- [Security](security.md) — practical key hygiene
- [Glossary](glossary.md) — plain-English definitions
