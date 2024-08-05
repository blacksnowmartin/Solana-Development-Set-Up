
# Quick Start Guide: Setting Up Your Local Development Environment for Solana

This guide will demonstrate how to quickly install and set up your local development environment, getting you ready to start developing and deploying Solana programs to the blockchain.

## What You Will Learn
- How to install the Solana CLI locally
- How to set up a localhost Solana cluster/validator
- How to create a Solana wallet for developing
- How to airdrop SOL tokens for your wallet

**Info**: If you are very new to development in general, or have only tried EVM-based blockchain development, your machine is likely not yet ready to help you code on Solana.

This guide will mainly cover three operating systems: Windows (using WSL), Linux, and macOS. Between each of these operating systems, the broad steps to get set up locally are largely the same:

- Install dependencies
- Install Rust and Cargo toolchain
- Install Solana CLI
- Install Anchor
- Set up a local blockchain cluster
- Create a filesystem wallet
- Airdrop Solana tokens to your wallet

## 1. Installing Dependencies

Just because Rust compiles and builds your software into a binary that can run for the computer architecture we specify, we need to install some OS-level dependencies on our machine.

### Dependencies for Windows

You can get started with Solana on Windows with WSL, the Windows subsystem for Linux. WSL allows you to run Linux software easily on Windows using a lightweight VM that instantly starts when you need it.

#### Setup WSL for Solana Development

First, start with installing WSL on your system. Be sure to restart your computer when installation is done, then continue this guide.

```sh
wsl --install
```

After installing WSL and restarting your computer, open a new Linux terminal session using WSL:

```sh
wsl
```

For the remainder of this guide and your Solana development using WSL, you will run all your commands, Solana builds, and program deployments inside this Linux terminal (except where otherwise noted in this guide).

If you are using VS Code as your code editor of choice, we recommend you follow this [tutorial on the VS Code website](https://code.visualstudio.com/docs/remote/wsl) to properly configure VS Code and WSL together. This will give you the best developer experience.

**Notice**: After the following section below about setting up WSL for Solana development, Windows/WSL users should continue to follow the Linux steps in this guide, except where otherwise noted.

Inside your Linux/WSL terminal session, continue to set up your local Solana development environment using the "Linux" steps below.

WSL can sometimes be a little slow due to its file system write speed limitations. You can also try dual booting your computer, installing a Linux operating system natively on the same machine, or using the full web browser-based Solana IDE called Solana Playground.

### Dependencies for Linux

Install the following dependencies on your Linux system:

```sh
sudo apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev \
    llvm \
    libclang-dev \
    protobuf-compiler \
    libssl-dev
```

### Dependencies for macOS

In macOS, build tools are provided by Xcode command line tools, which you can download directly from Apple. You will likely need to sign in with your Apple ID to download.

You can check if the Xcode CLI is installed via this command:

```sh
xcode-select -p
```

If you don't see a path returned, you need to install the CLI tools.

#### There are Three Ways to Install Xcode CLI Tools

- Installing via your terminal using the following command:
    ```sh
    xcode-select --install
    ```
- Download the installer and install it with a graphical interface from [Apple Developer Tools](https://developer.apple.com/download/more/)
- Installing via Homebrew:
    ```sh
    brew install xcode-select
    ```

**Congrats**: You have now installed system dependencies and build essentials required for Solana program development.

## 2. Install Rust

The Rust programming language is a multi-paradigm, general-purpose programming language that emphasizes performance, type safety, and concurrency.

Using `rustup`, the official Rust version installer and manager, we will install `rustc` (the compiler for Rust) and `cargo` (the package manager for Rust) all at once.

### Install Rust for macOS, Linux, WSL, or Another Unix-like OS

Using the following command, we can install and configure the Rust tooling on your local system. The following command will automatically download the correct binaries needed for your specific operating system:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
```

As part of this Rust installer, Rustup will also configure your terminal's PATH to include the Rust toolchain.

After the installation is complete, restart your terminal or run the following command to manually refresh your new PATH settings to make the Rust tooling (like `cargo`) available:

```sh
source ~/.bashrc
```

## 3. Install the Solana CLI

For local development, including compiling your Solana programs, you will need to install the Solana CLI. This command-line tool suite provides all the commands needed to perform common tasks, like:

- Creating and managing file-system Solana wallets/keypairs
- Connecting to Solana clusters
- Building Solana programs
- Deploying your programs to the blockchain

### For Linux, macOS, WSL, or Other Unix-like Systems

Install the Solana CLI tool suite using the official install command:

```sh
sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
```

You can replace `stable` with the release tag matching the software version of your desired release (e.g., `v1.18.1`), or use one of the three symbolic channel names: `stable`, `beta`, or `edge`.

Depending on your specific operating system, the Solana CLI installer messaging may prompt you to update the PATH environment.

Please update your PATH environment variable to include the Solana programs:

If you get the above message, simply copy and paste the command recommended by the Solana CLI installer to update your PATH environment variable.

After running this command, restart your terminal to make sure your Solana binaries are accessible in all the terminal sessions you open afterward.

To check if your installation was successful, check the Solana CLI version:

```sh
solana --version
```

You can see more versions and releases according to the target [Solana releases](https://docs.solana.com/cli/releases).

### Updating the Solana CLI

In the future, you can use the Solana CLI to update itself based on which latest version is available:

```sh
solana-install update
```

## 4. Install Anchor for Solana

Anchor is a framework for the Solana runtime providing several convenient developer tools for writing on-chain programs. It helps you write programs with less code since it has abstracted away a lot of security checks and common boilerplate using Rust's macros.

To install and manage Anchor versions, we will use `avm`, the Anchor version manager. Since `avm` is installed via `cargo` (the Rust package manager), the installation steps will be the same for all the operating systems.

We can then use `avm` to install the desired version of the Anchor framework.

### Install `avm`

```sh
cargo install --git https://github.com/coral-xyz/anchor avm --locked --force
```

### Install Anchor Using `avm`

To install the latest version of Anchor using `avm`:

```sh
avm install latest
avm use latest
```

After the Anchor installation is complete, you can verify Anchor was installed by checking the installed version:

```sh
anchor --version
```

If you do not see an output or receive an error, you may need to restart your terminal.

## 5. Setup a Localhost Blockchain Cluster

The Solana CLI comes with the test validator built-in. This command line tool will allow you to run a full blockchain cluster on your machine:

```sh
solana-test-validator
```

**Pro Tip**: Run the Solana test validator in a new/separate terminal window that will remain open. This command line program must remain running for your localhost cluster to remain online and ready to process transactions and requests (like deploying programs).

Configure your Solana CLI to use your localhost validator for all your future terminal commands:

```sh
solana config set --url localhost
```

At any time, you can view your current Solana CLI configuration settings:

```sh
solana config get
```

## 6. Create a File System Wallet

To deploy a program with Solana CLI, you will need a Solana wallet with SOL tokens to pay for the cost of transactions and data storage on the blockchain.

Let's create a simple file system wallet to use during local development:

```sh
solana-keygen new
```

By default, the `solana-keygen` command will create a new file system wallet located at `~/.config/solana/id.json`. You can manually specify the output file location using the `--outfile /path` option.

**Info**: If you already have a file system wallet saved at the default location, this command will NOT override it unless you explicitly force override using the `--force` flag.

### Set Your New Wallet as the Default

With your new file system wallet created, you must tell the Solana CLI to use this wallet to deploy and take ownership of your on-chain program:

```sh
solana config set -k ~/.config/solana/id.json
```

