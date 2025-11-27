# Decentralized Stablecoin (DSC) — Foundry example

This repository is a compact Foundry project that implements a minimal, educational decentralized stablecoin system.
It demonstrates a small, self-contained protocol with two core contracts, a deployment script, a set of mocks and a thorough suite of unit and fuzz tests.

The implementation is intentionally simple and designed for learning: it focuses on collateralized minting, burning, redeeming and liquidation logic while keeping the codebase easy to read and test with Forge.

---

## Project contents (quick)

- src/
	- `DecentralizedStableCoin.sol` — an ERC20 token contract that represents the protocol's stablecoin (DSC). Only the engine contract may mint/burn.
	- `DSCEngine.sol` — the core protocol: accepts ERC20 collateral, maintains collateral-to-DSC accounting, enforces health factors, and allows liquidation.
- script/
	- `DeployDSC.s.sol` — example Foundry deployment script used by tests and demos.
- test/
	- `unit/DSCEngineTest.t.sol` — unit tests covering core flows and edge cases.
	- `fuzz/` — fuzz testing handlers and invariants to validate safety properties.
	- `mocks/ERC20Mock.sol` — ERC20 mock used throughout tests.
- lib/
	- third-party libs including `forge-std` and a Chainlink-style `MockV3Aggregator` used for test price feeds.

---

## Design & intent

- Goal: Understand how a minimal, collateralized, algorithmic USD-pegged stablecoin can be implemented and tested in Foundry.
- Core ideas: per-user collateral deposits, minting/burning DSC against collateral, health factor/overcollateralization constraints, and liquidation mechanics.

---

## Tests & examples

This repository includes a comprehensive unit test suite for `DSCEngine` and additional fuzz/invariant tests to check safety invariants (e.g. protocol solvency).

Key tests include:
- `test/unit/DSCEngineTest.t.sol` — constructor validation, pricing math, deposit/mint/redeem flows, liquidation, and view method checks.
- `test/fuzz/` — handlers and invariant suites that exercise many randomized interactions and test invariants such as "total collateral value >= total DSC supply".

Mocks used by the tests:
- `test/mocks/ERC20Mock.sol` — simple ERC20 with mint/burn helpers.
- `lib/chainlink-brownie-contracts/.../MockV3Aggregator.sol` — Chainlink-style price feed mock used to drive prices and simulate market changes.

---

## How to run locally (no compile/test run performed here)

Requirements: Foundry (forge, cast, anvil). See https://book.getfoundry.sh/.

Quick commands:

```bash
# build the project
forge build

# run tests
forge test

# run a specific test file
forge test --match-path test/unit/DSCEngineTest.t.sol
```

If you'd like a walkthrough of the code or a compact diagram of contract interactions, I can add one next.

---

## Foundry (general shortcuts)

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```
