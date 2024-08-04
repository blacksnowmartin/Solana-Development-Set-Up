How to get Solana devnet SOL (including airdrops and faucets) #
This is a collection of the different ways for developers to acquire SOL on Solana's testing networks, the Solana devnet and testnet.

1. Solana Airdrop #
Available on Devnet and Testnet

This is the base way of acquiring SOL, but it can be subject to rate limits when there is a high number of airdrops.

Here are three different ways of requesting airdrops with it:

Using the Solana CLI: #
solana airdrop 2

Using web3.js: #
const connection = new Connection("https://api.devnet.solana.com");
connection.requestAirdrop();

See more: requestAirdrop() documentation inside web3.js.

2. Web Faucet #
Available for Devnet

faucet.solana.com - A public web faucet hosted by the Solana Foundation
SolFaucet.com - Web UI for airdrops from the public RPC endpoints
QuickNode - A web faucet operated by QuickNode
Available for Testnet

faucet.solana.com - A public web faucet hosted by the Solana Foundation
SolFaucet.com - Web UI for airdrops from the public RPC endpoints
QuickNode - A web faucet operated by QuickNode
TestnetFaucet.org - A web faucet with a rate limit separate than the public RPC endpoints, operated by @Ferric
3. RPC Provider Faucets #
Available for Devnet

RPC Providers can opt in to distributing devnet SOL via their devnet Validators.

Info
If you are an RPC Provider and want to distribute SOL please get in touch here.

Currently supported:

Helius
QuickNode
Triton
Using the Solana CLI #
Specify your Cluster to be your RPC provider's URL:

solana config set --url <your RPC url>

Then you can request an airdrop like you would in the first option in this guide:

solana airdrop 2

Using Web3.js #
const connection = new Connection("your RPC url");
connection.requestAirdrop();

4. Proof of work Faucet #
Available for Devnet

This is a proof of work Faucet where devnet SOL can be distributed to you thanks to your computing power.

Install the Devnet POW Crate:

cargo install devnet-pow

Start mining devnet SOL

devnet-pow mine

⚠️ The POW Faucet is maintained by Ellipsis Labs

5. Discord Faucets #
Various Discord communities have setup devnet SOL Faucets as BOTs.

Community	Usage	Link
The 76 Devs	Run !gibsol in the BOT commands channel.	Join Server
The LamportDAO	Run /drop <address> <amount> in the BOT commands channel.	Join Server
6. Reuse devnet SOL #
The most sustainable way to save SOL is to reuse it. With the Solana CLI you can show and close all previous buffer accounts with the following command:

solana program show --buffers

What's a buffer account?
Buffer accounts are automatically created when you deploy a program. All the program's data is transferred into this account during the deployment. When its done, the data of your program is replaced with the new data.

Normally, these buffer accounts are closed automatically. In the event they are not, you can close them manually to reclaim the SOL in them using the following command:

solana program close <buffer account>

You can also the show subcommand to show all programs you deployed have already deployed to your currently selected cluster:

solana program show --programs

You can then close each program with the close subcommand to close them and retrieve the SOL you used to deploy them:

solana program close <program id>

You can then use that SOL to deploy new programs.

Caution
You will NOT able to use the same program id again once you closed the program. So make sure are closing the right program and that you will not need that id anymore.

If you get rate limited by the RPC endpoint your Solana CLI is configured to use, you can add -u "urlToYourRpc" to the any of these command to use a different RPC endpoint.
