# Solana Prediction Market Smart Contract

A **prediction market** smart contract on Solana. Create and trade YES/NO outcome tokens, then migrate completed markets to Raydium. Built with Anchor for the **Solana prediction market** ecosystem.

## What is this?

This repo provides an on-chain **prediction market smart contract** that runs on Solana. Market creators launch binary (YES/NO) markets; traders swap SOL for outcome tokens and back. When a market completes, liquidity can be migrated to Raydium. Use it as a foundation for a **Solana prediction market** app or integrate the program into your own frontend.

## Features

- **Create prediction markets** with YES and NO outcome tokens
- **Swap** SOL ↔ YES/NO tokens (buy and sell) on a bonding curve
- **Creator claims** and fee distribution
- **Migrate** completed markets to Raydium
- **Admin config** for fees and launch parameters

## Prerequisites

Install Rust, Solana, and Anchor (AVM): https://solana.com/docs/intro/installation

Use **Anchor v0.30.1**:

```bash
avm install 0.30.1
avm use 0.30.1
```

## Quick Start

### Build the program

```bash
anchor run build
```

If you use a custom `CARGO_TARGET_DIR` (e.g. `$HOME/.cargo/target`), link the built program into the deploy folder:

```bash
ln -s $HOME/.cargo/target/sbf-solana-solana/release/takesfun.so $PWD/target/deploy/takesfun.so
```

### Run tests

Run tests without a local network:

```bash
anchor test --provider.cluster Localnet
```

### Local network and deployment

Configure for localhost and start a validator:

```bash
solana config set -ul
solana config set -k ./keys/EgBcC7KVQTh1QeU3qxCFsnwZKYMMQkv6TzgEDkKvSNLv.json

# Start validator with metadata program for tokens
solana-test-validator -r --bpf-program metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s spl-programs/metadata.so
```

Deploy the prediction market program:

```bash
anchor deploy --provider.cluster Localnet
```

Run tests against localnet:

```bash
anchor run test --provider.cluster Localnet
anchor run test --provider.cluster Localnet -- "'correctly configured'"
```

### Devnet

Set the cluster in `Anchor.toml` to your devnet RPC, then:

```bash
anchor deploy
```

## Configuration

Call the `configure` instruction (admin only) to set global config: fee amounts and allowed launch parameters for the prediction market smart contract.

## CLI: Test the prediction market

### Initialize program config

```bash
yarn script config
```

### Launch a prediction market (create YES/NO market)

```bash
yarn script launch
```

### Swap SOL for outcome tokens

```bash
yarn script swap -t <TOKEN_MINT> -a <SWAP_AMOUNT> -s <SWAP_DIRECTION>
```

- `TOKEN_MINT`: YES or NO token mint (from launch output)
- `SWAP_AMOUNT`: Amount in SOL or tokens to swap
- `SWAP_DIRECTION`: `0` = Buy, `1` = Sell

### Migrate to Raydium

After the curve is completed, migrate the market to Raydium:

```bash
yarn script migrate -t <TOKEN_MINT>
```

`TOKEN_MINT`: mint address of the market token to migrate.

---

## Author

[Telegram](https://t.me/microRustyme)

**Keywords:** prediction market, prediction market smart contract, Solana prediction market, binary outcome market, YES NO tokens, Solana Anchor.
