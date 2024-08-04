# What you will learn #
- how to install the Solana CLI locally
- how to set up a localhost Solana cluster/validator
- how to create a Solana wallet for developing
- how to airdrop SOL tokens for your wallet

# Solana Local Development Setup Guide

This repository provides a comprehensive guide to setting up a local development environment for building on the Solana blockchain.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Rust**: The primary language for Solana onchain programs.
- **Solana CLI**: Command Line Interface for interacting with the Solana blockchain.
- **Anchor**: A framework for Solana's Sealevel runtime.

## Installation

### Step 1: Install Rust

Install Rust by running the following command:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```


### Step 2: Install Solana CLI
Install the Solana CLI by executing:

```bash
sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
```

Step 3: Run a Local Validator
Start a local Solana validator for testing your programs:

```bash
solana-test-validator
```
Setting Up Your Project
Creating a Solana DApp
You can scaffold a new Solana project using:

bash
Copy code
npx create-solana-dapp <project-name>
This command generates a new project with all necessary files and basic configurations.

Development Workflow
Onchain Program Development
Write your program: Use Rust to write onchain programs.
Compile and Deploy: Use the Solana CLI to compile and deploy your programs.
Testing: Run tests locally using solana-test-validator.
Client-side Development
Develop your client-side application in your preferred language. Solana supports several SDKs:

Rust: solana_sdk
JavaScript/TypeScript: @solana/web3.js
Python: solders
Java: solanaj
Go: solana-go
Example Commands
Compile your onchain program:

```bash
cargo build-bpf
```
Deploy your onchain program:

```bash
solana program deploy /path/to/your/program.so
```

We welcome contributions! Please read our contributing guidelines for more details.

