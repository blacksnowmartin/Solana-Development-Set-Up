In this article, I will take you out of the rabbit hole. We will, together, put back the pieces of all the blockchain concepts by uncovering the true purpose of wallets.

Hint: Wallets are not here to show your losses in a bear market 😅, they are here to access the blockchain and build!

Puzzle Piece 1: The Balance Myth #
🤫 Tell you a secret, wallets are misleading. They do not store your crypto. In fact, they do not hold anything. So why do we need even them in dapps and blockchain?

A screenshot of a wallet balance
A screenshot of a wallet balance

Skeptical? Take a look at this account's balance. If my crypto were stored inside a wallet, how come you can just look up what's inside my wallet on the Internet?

A screenshot of a transaction on the solana explorer
A screenshot of a transaction on the solana explorer

Why am I starting to talk about wallet balance? You may ask. Because the "wallet" term is misleading! For a casual crypto holder, that notion of token storage might be enough. But as devs, this does not make sense at all. So let's debunk all the myths about wallets by investigating how data and balances are stored.

Your wallet balance is stored on the blockchain, not inside your Phantom app, not inside your nano ledger. So it is just data that you can query from the blockchain, and anyone can see it!

Earlier, I used the Solana explorer to check my wallet SOL balance. We can retrieve data about a wallet by identifying it by its public key.

Let's update our definition of wallets:

A wallet can be identified by a public key (its address).
A wallet balance is just data stored on the blockchain.
A diagram showing how data is stored on-chain
A diagram showing how data is stored on-chain

Puzzle Piece 2: Blockchain #
Let's continue to unroll the thread. We have established that balance is stored on the blockchain and not inside your computer. The next exciting trail we could follow is to ask ourselves how data, in general, is stored in the blockchain.

To understand why we need wallets, we first need to understand how data is stored in blockchains.

But first, let's take a step back and compare how data is stored in a web2 world:

A diagram showing how data is stored in traditional systems
A diagram showing how data is stored in traditional systems

In web2, your data is siloed inside a company's server, and the data is handled by the company. So if tomorrow they decide to delete for censorship or mistakenly destroy your data, it can happen! (That's not a pro blockchain comment, it is just a fact 😅).

Now, let's compare it to how data is stored in a blockchain:

A diagram showing how data is stored on a blockchain
A diagram showing how data is stored on a blockchain

A blockchain is a distributed ledger:

A blockchain is not one single thing. It is a swarm of servers, like 🐝
Altogether, these servers represent "a blockchain," like a beehive 👁‍🗨
These servers belong to no one or rather anyone.
Anyone can be part of the blockchain, and you can use your grandma's laptop as one of these servers.
All the nodes store a copy of the data.
Info
Actually, your grandma's hardware is not probably gonna cut it, but you got my point!

💡 Think

Does a blockchain necessarily need to be on the Internet?
What is the problem with sharing data with anyone?
Puzzle Piece 3: Signing #
If we recap what we just learned about blockchains, all nodes contain a copy of your data. I don't know for you, but something is bugging me here...

It means anyone from your best friend to your worse enemy can use their computer to make a node and thus own your data!

Since data is shared by everyone, how do we avoid anarchy and people modifying other people's data or cheating the system:

If an Instagram Clone were built on the blockchain, you would not want anyone to start modifying or deleting your photos, would you?
Or, if we were making a Paypal version on the blockchain, how do we make sure that someone doesn't withdraw money from your account? After all, the data (balance) is duplicated and spread between everyone.
Let's take the example of a wallet balance, this time we gonna zoom inside a blockchain node:

A simplified version of a transaction stored on a ledger
A simplified version of a transaction stored on a ledger

Let's say we have 3 protagonists, Claire, Jay, and Brian. Claire happily sends 5 SOL to both Jay and Brian. But Brian (the evil guy in my story) wants more than 5 SOL. So he pretends to be Claire and asks the blockchain to send an additional 10 SOL to himself.

What actually prevents him from doing this?

If we were doing web2, you would be saying, well, we can check if the user is signed in, and if they are signed in, we can check if the balance's owner is indeed the user; there are two problems:

There is no "session"; the blockchain does not track who is currently "signed in."
Earlier, when we verified the wallet balance, we used the wallet public key; the public key is, well ...public; you could use my public key and pretend to be me.
Enough teasing. What's the solution?

A simplified version of a transaction stored on a ledger
A simplified version of a transaction stored on a ledger

Yes! The key is signing using the secret key! We can "password protect our data" without communicating the password, thanks to asymmetric cryptography magic.

What's asymmetric? Think SSH keys.

Can't wrap your head around it? Well, just think about the real world. For example, if a malicious imposter wants to withdraw money from your bank account, he would need your signature to do it. Well, that's precisely the same here: any modification to data identified by a public key also needs to be signed by the corresponding secret key.

Yes, there was a world like that when mobile banking did not exist.

That's the true nature of wallets!! They are here to sign access to data. They are signatures or stamps.

That's a whole different paradigm here. In web2, authentication and authorization were handled by the server. While in web3, this is done directly by cryptography with keys in your own hand!

Congrats! You discovered the nature of trustless and decentralized systems.

Puzzle Piece 4: Transaction #
We just uncovered the true nature of wallets just above. But what exactly do we sign? Secret keys are used to sign transactions. A transaction is how we can ask a blockchain to do something.

And the good thing for us is that blockchains are all ears to receive orders. Grossly speaking, a blockchain, or more precisely a blockchain node, stores logs or journals. They contain a very long list of orders (transactions). These transactions all together represent the state of the world. That's why we call blockchain state machines:

Maverick sends 10 SOL to Iceman.
Claire sends 5 SOL to Laura.
Michael B. buys Wakanda NFT.
Info
Blockchain actually stores a chain of blocks. Transactions are bundled into blocks. But that's a story for another time.

How do permission and signing actually work? Let's say Brian tries to impersonate Claire to send himself some extra SOL from Claire's wallet (Remember? Wallet Addresses are public).

A diagram showing the lifecycle of a transaction
A diagram showing the lifecycle of a transaction

Info
Solana can do much more than Transfer Tokens, but the same logic applies to every action, especially for modifying data, where you need to prove that you have the permission to do so. Thus you need to sign that action (transaction).

💡 Think

When do we need to sign transactions?
And when do we not need to sign?
... (don't look below before trying!)

We need to sign when we mutate data. If we create or change data, we are supposed to have the authority to do so.
We do not need to sign when just reading data.
Puzzle Piece 5: Wallet Apps #
And finally, to complete the circle, let's talk about wallet apps such as Phantom or Solflare. As you now understand, the secret sauce to the world of blockchain is really about the public key and the signing using the secret key.

Wallets Apps are really just apps regardless of if it is a mobile wallet, a browser extension, or a desktop app, it really is just an app.

These apps just wrap around your keys and add UX niceties such as:

Storing your secret key encrypted and with a password lock.
Adding a recovery passphrase to restore the key.
Fetching data from the blockchain to display your wallet's balance.
Letting you swap a token by connecting with exchanges.
Etc.
An example of how the recovery and balance feature work:

A diagram showing an example of how the recovery and balance features on a wallet work
A diagram showing an example of how the recovery and balance features on a wallet work

As you can see, the essential data live in the blockchain. Wallets are just convenience vaults that store your secret key encrypted. This is just standard industry encryption and has nothing to do with the blockchain. The most important feature it provides really is signing using the secret key.

Putting things back in order #
Data is stored in a swarm of servers (nodes); these validators form the blockchain.
Everyone can be a validator node. For this reason, data can be accessed by anyone.
Changes in a blockchain happen with directives: instructions/transactions.
To avoid chaos, we need a way to determine who can change what: this is where signing comes into play.
Thanks to cryptography, we can sign a transaction (change) using a public/secret key pair: this stamp (or signature) allows us to "password lock" some data without communicating the password to the world.
A blockchain is a state machine that stores an infinite list of records, logs, or journals of every transaction. The blockchain verifies access to data by checking a transaction signature.
That's why wallets exist! To authenticate and authorize access by signing with a secret key!
A wallet is purely a convenience we created to wrap the secret key and add niceties such as; securely storing the secret key (with a password lock) or showing the token account balance. So yes, wallets store an encrypted version of your secret key.
You can totally interact with the blockchain without a wallet app like Solflare or Phantom! It would just be a harrowing user experience. ;)
So here you have it, public/secret key pairs provide a way for the blockchain to identify you and make sure you got the permission to do what you claim you should be able to do!

Wallets are called wallets because the first usage was to lock your balance historically. But in the on-chain program world, it is still about locking your data, not just balances. If anything, wallets should really be called stamps or signature pens! ✍️.

What's Next? #
Do you want to start building on Solana?

A gentle introduction to Solana: https://solana.com/news/solana-scaffold-part-1-wallet-adapter
Tutorials: https://soldev.app/
Blockchain and blockchain #
At 10000 feet, blockchain in the macro term is a swarm of servers, validators nodes.
At 100 feet, a blockchain node contains a chain of blocks.
At 1 mm, a block bundles a list of transactions/instructions
Back to 10000 feet, a blockchain is a swarm of nodes that synchronize their chain of blocks.
The term blockchain originates from the invention of blocks that are chained together. But in general, when we say blockchain, we think about the whole swarm of nodes, because everyone is supposed to be a copy of another node. So they are all the same.

Accounts #
I haven't mentioned precisely how data are stored. In the Solana world, everything is stored in accounts. If Linux stores data into files, Solana stores data into accounts like a file system. While files have a filename, accounts have a public address:

So your SOL balance is actually stored in an account whose public address is your public key!
Modification access to that account is locked by the corresponding secret key signature!
Authentication #
When you connect your wallet to a dapp. What does connecting a wallet really do? You are not "connecting" anything, actually. It just gives your public key to the dapp. As we said earlier, to prove that you own the public key, the dapp needs to ask you to sign a message. You probably have seen this in some dapps, where you would have two popups:

One for connecting the wallet.
Another one to sign a message.
Previous
