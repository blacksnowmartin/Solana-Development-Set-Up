The Solana test validator is a local emulator for the Solana blockchain, designed to provide developers with a private and controlled environment for building and testing Solana programs without the need to connect to a public testnet or mainnet. If you have the Solana CLI tool suite already installed, you can run the test validator with the following command:

solana-test-validator

Advantages #
Ability to reset the blockchain state at any moment
Ability to simulate different network conditions
No RPC rate-limits
No airdrop limits
Direct on-chain program deployment
Ability to clone accounts from a public cluster
Ability to load accounts from files
Configurable transaction history retention
Configurable epoch length
Installation #
Since the solana-test-validator is part of the Solana CLI tool suite, ensure you have Solana's command-line tools installed. You can install them using the following command:

sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

You can replace stable with the release tag matching the software version of your desired release (i.e. v1.18.12), or use one of the three symbolic channel names: stable, beta, or edge.

Info
For more detailed instructions, checkout this guide on setting up your local environment for Solana development. It includes installing the Solana CLI, Anchor, getting a local keypair, and more.

Starting the Test Validator #
To start your local validator, simply run:

solana-test-validator

This command initializes a new ledger and starts the validator.

Interacting with a Running Test Validator #
Once you have the solana-test-validator up and running, you can interact with it using various Solana CLI (Command Line Interface) commands. These commands let you deploy programs, manage accounts, send transactions, and much more. Here’s a detailed guide on the key commands you will use.

Checking the Status of the Test Validator #
Before interacting with the test validator, it's useful to confirm its status and ensure it is running correctly.

solana ping

This command pings the local test validator and returns the current blockhash and latency, verifying that it is active.

Account Management #
To create a new keypair (account), use:

solana-keygen new

This command creates a new keypair and saves it to the specified file.

To add SOL to your account:

solana airdrop 10 <ACCOUNT_ADDRESS>

To retrieve details about an account, such as its balance and owner:

solana account <ACCOUNT_ADDRESS>

You must first airdrop funds to the account for the account to exist.

This command sends 10 SOL to the specified account address.

Deploying and Managing Programs #
To deploy a compiled program (BPF) to the test validator:

solana program deploy <PROGRAM_FILE_PATH>

This uploads and deploys a program to the blockchain.

To check the details of a deployed program:

solana program show <ACCOUNT_ADDRESS>

Sending Transactions #
To transfer SOL from one account to another:

solana transfer --from /path/to/keypair.json <RECIPIENT_ADDRESS> <AMOUNT>

This sends AMOUNT of SOL from the source account to the RECIPIENT_ADDRESS.

Simulating and Confirming Transactions #
Before actually sending a transaction, you can simulate it to see if it would succeed:

solana transfer --from /path/to/keypair.json --simulate <RECIPIENT_ADDRESS> <AMOUNT>

To confirm the details and status of a transaction:

solana confirm <TRANSACTION_SIGNATURE>

Viewing Recent Block Production #
To see information about recent block production, which can be useful for debugging performance issues:

solana block-production

Creating Token Accounts #
Adjusting Logs #
For debugging, you might want more detailed logs:

solana logs

This streams log messages from the validator.

Useful Tips Logging:

Increase log verbosity with the -v flag if you need more detailed output for debugging.
Use the --rpc-port and --rpc-bind-address options to customize the RPC server settings.
Adjust the number of CPU cores used by the validator with the --gossip-host option to simulate network conditions more realistically.
Configuration #
Check CLI Tool Suite configuration:

solana genesis-hash

View all the configuration options available for the Solana test validator:

solana-test-validator --help

Local Ledger #
By default, the ledger data is stored in a directory named test-ledger in your current working directory.

Specifying Ledger Location #
When starting the test validator, you can specify a different directory for the ledger data using the --ledger option:

solana-test-validator --ledger /path/to/custom/ledger

Resetting the Ledger #
By default the validator will resume an existing ledger. To reset the ledger, you can either manually delete the ledger directory or restart the validator with the --reset flag:

solana-test-validator --reset

If the ledger exists, this command will reset the ledger to genesis, which resets the state by deleting all existing data and starting fresh.

Runtime Features #
Solana has a feature set mechanism that allows you to enable or disable certain blockchain features when running the test validator. By default, the test validator runs with all runtime features activated.

To query the runtime feature status:

solana feature status <ADDRESS>

ADDRESS is the feature status to query [default: all known features]
To activate a specific feature:

solana feature activate <FEATURE_KEYPAIR> <CLUSTER>

FEATURE_KEYPAIR is the signer for the feature to activate
CLUSTER is the cluster to activate the feature on
To deactivate specific features in genesis:

solana-test-validator --deactivate-feature <FEATURE_PUBKEY> --reset

This must be done on a fresh ledger, so if a ledger already exists in your working directory you must add the --reset flag to reset to genesis.

Changing Versions #
To check your current solana-test-validator version:

solana-test-validator --version

Your solana-test-validator runs on the same version as the Solana CLI version.

To test your programs against different versions of the Solana runtime, you can install multiple versions of the Solana CLI and switch between them using the solana-install set command:

solana-install init <VERSION>

VERSION is the desired CLI version to install
Make sure to restart your Solana test validator after changing versions to ensure it runs the correct version.

Cloning Programs #
To add existing onchain programs to your local environment, you can clone the program with a new ledger.

To clone an account from the cluster:

solana-test-validator --clone PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO

This is useful for testing interactions with standard programs.

If a ledger already exists in your working directory, you must reset the ledger to be able to clone a program.

To clone an account from the cluster when a ledger already exists:

solana-test-validator --clone PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO --reset

To clone an upgradeable program and its executable data from the cluster:

solana-test-validator --clone-upgradeable-program PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO

Resetting State on Accounts at Startup #
By default the validator will resume an existing ledger (if present). But during startup, you can reset the ledger either to genesis or to specific account state that you provide.

Reset to Genesis #
To reset the ledger to the genesis state:

solana-test-validator --reset

Reset to Specific Accounts #
To reset the state of specific accounts every time you start the validator, you can use a combination of account snapshots and the --account flag.

First, save the desired state of an account as a JSON file:

solana account PROGRAM_ADDRESS --output json > account_state.json

Then load this state each time you reset the validator:

solana-test-validator --reset --account PROGRAM_ADDRESS account_state.json

Solana CLI Commands #
To view all CLI commands and see other ways to interact with the test validator:

solana --help

This command list all flags, options, and subcommands available.

Example Use Case #
Create a USDC Token Account on your localnet

Clone the USDC mint address to your local validator
solana-test-validator --clone EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v --url mainnet-beta --reset

Create a token account
spl-token create-account EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v --url localhost
