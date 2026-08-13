# Smart contracts

Inazuma executes **WebAssembly**. Any language that compiles to WASM with no
host-OS dependencies can be used; Rust is the best-supported path today.

## Model

- A contract is WASM bytecode deployed to its own address.
- Contracts hold key-value storage; state changes are metered by gas and charged in INAZ.
- Reads are free: `inaz_query` runs a method without a transaction.
- Writes are transactions and appear in blocks like transfers.

## Lifecycle

| Step | How |
| --- | --- |
| Write | Rust (or any WASM target). Examples: [inazuma-contracts](https://github.com/inazuma-network/inazuma-contracts) |
| Build | `cargo build --target wasm32-unknown-unknown --release` |
| Deploy | Submit the bytecode as a deploy transaction; you receive a contract address |
| Call | Write: transaction. Read: `inaz_query(address, method, args)` |
| Inspect | `inaz_getContract`, `inaz_contractStorage`, `inaz_contracts` |

## Practical rules

- Keep storage small — every byte is paid for by everyone who syncs.
- Validate all inputs; a panic aborts the call and consumes gas.
- Charge-then-act: update balances before external effects.
- Simulate first with `inaz_simulateTransaction` to catch reverts for free.

## Native tokens

Simple fungible tokens do not need a contract — they exist at the protocol level
(`inaz_tokens`, `inaz_getToken`, `inaz_tokenBalance`, `inaz_tokenHoldings`),
which makes them cheaper and faster than a contract-based token.

Start from the worked examples and build scripts in
[inazuma-contracts](https://github.com/inazuma-network/inazuma-contracts).
