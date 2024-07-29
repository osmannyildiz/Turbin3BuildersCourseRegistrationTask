# Turbin3 Builders Course Registration Task (Rust)

> Here is my proof of work: https://explorer.solana.com/tx/3Ajo2D5fdDjgUiYMZzLTWB1XwVnBcBaUwwnbswDQqLVnLGnqWt568EtgFwFbKJevgz8UuzLe5sWPoYFi3UsUy83b?cluster=devnet

This repo demonstrates some basic operations performed using Solana's Rust libraries.

## Installation

Cargo automatically installs dependencies when necessary.

## Usage

### Generate Keypair

This will create a new keypair, and print its public and secret keys.

```sh
cargo test keygen -- --nocapture
```

Create the file `wallets/dev-wallet.json` and paste the secret key (starting with `[`, ending with `]`, both included) inside the file.

### Convert Secret Key from Byte Array to Base58

This will get the byte array as input and print its Base58 representation.

```sh
cargo test byte_array_to_base58 -- --nocapture
```

Some wallet software (like Phantom) expect secret keys as Base58. This functionality will come in handy for importing a JSON wallet file into Phantom.

### Convert Secret Key from Base58 to Byte Array

This will get the Base58 string as input and print its byte array representation.

```sh
cargo test base58_to_byte_array -- --nocapture
```

Some wallet software (like Phantom) let you export secret keys as Base58. This functionality will come in handy for converting it into a JSON wallet file.

### Get Devnet SOL

This will request 2 devnet SOLs into the wallet.

```sh
cargo test airdrop -- --nocapture
```

### Transfer some SOL

This will send 0.1 SOL from the new account to my previous account.

```sh
cargo test transfer_sol -- --nocapture
```

In Solana, fund transfers are done via the System Program. The sender needs to sign the transaction, which requires their secret key. This way, we can ensure that nobody can transfer someone else's funds (as long as they keep their secret key "secret").

### Transfer all SOL

This will send the maximum amount of SOL possible from the new account to my previous account.

```sh
cargo test transfer_all_sol -- --nocapture
```

To accomplish this, we need to consider the transaction fee while deciding on the amount to send. For that, we first create a transaction similar to the real one. Then we ask the network how much fee this mock transaction would require. Finally we subtract the fee from the destination account's total balance, and this gives us the maximum amount of SOL we can send.

### Interact with the `wba_prereq` Program

In order to finish registration for the Turbin3 Builders Course, we are required to interact with a program that's already deployed on the devnet. For this, we need the program's IDL (Interface Definition Language), which contains all the necessary information to use the program.

This will call the `complete` method of the on-chain program, giving my GitHub username as an argument, also deriving and providing a PDA to store my data in.

```sh
cargo test complete -- --nocapture
```

## My Transactions

- Getting devnet SOL: https://explorer.solana.com/tx/3U6m3EaaVZLe9jsUqHH9acmAMSbuauq8UdJQfmSoGw9aTDe6gr75W1m6Ngu6t4eL58nhvamGSVPr9tpGDGLQdJkv?cluster=devnet
- Transferring 0.1 SOL: https://explorer.solana.com/tx/3Vevz5N3gcHR5QjV5bkWyA9bpxxdi3mKnFZxPa9WxcazcvBbLaLngR9fXDzVqPxwiTJZywsDW6HjExRfnLzpqcpf?cluster=devnet
- Transferring all SOL: https://explorer.solana.com/tx/3QgyAtwhGktyJArjkPazCA25QBHXi35k8sJjBXkLm76na7aczA9yFbdXa1aQbYh3acdXhc1f1hmZ4TB53gTaQYJh?cluster=devnet
- Interacting with the program: https://explorer.solana.com/tx/3Ajo2D5fdDjgUiYMZzLTWB1XwVnBcBaUwwnbswDQqLVnLGnqWt568EtgFwFbKJevgz8UuzLe5sWPoYFi3UsUy83b?cluster=devnet
