
Blockchain technology is perhaps one of the most important innovations of the century. It's a complex fusion of tools and protocols like networking, cryptography, privacy, security, ownership, trustless communication, governance, etc. A true blockchain is permissionless, which means anyone can use the blockchain without asking permission. However, people who use blockchains are inherently agreeing to the rules that the blockchain runs on. Those rules are (hopefully) established by consensus. Each of those consensus rules actually has to be implemented into software, which is what enforces the rules. As such, it's important to delve into the software that's enabling and enforcing the rules on a blockchain for everyone's benefit.

Blockchains are public ledgers which are distributed among a peer-to-peer network of computers. There is no central server that stores the ledger. It doesn't exist out there, somewhere in the void. The ledger is stored on people's computers. If a new computer connects to the network and asks for the ledger, it downloads the ledger from multiple peers. 

To fully participate in the network, a computer needs to carry the ledger in its entirety, verify that the ledger is following all the consensus rules, and synchronize with the rest of the network so that all the other participants maintain an identical ledger.

There's strength in numbers. It's possible that a single, malicious, participant could invent a new ledger that makes them a multi-billionaire. However, if the majority of everyone else on the network is following the same consensus rules, it would be impossible for that malicious participant to give their malicious ledger to everyone else. Everyone else would just reject it, saying: "No, this doesn't follow the rules."

Therefore, since the network participants are each following the same set of rules, and everyone is sharing the same ledger between each other, it's practically impossible to go back and retroactively alter the ledger. You can only add new information to the ledger. That's what makes old blocks immutable.

The software that makes this all possible on the Decred blockchain is dcrd. dcrd is written in Go (golang), and implements all the consensus rules and core blockchain ledger functionality. It is important to note that dcrd does NOT include wallet functionality, and was designed that way for multiple reasons including security. You can consider dcrd to be your personal Decred blockchain server, which would connect you to the rest of the Decred network.

## dcrd responsibilities
dcrd is the backbone of Decred's peer-to-peer network. dcrd acts as a 'full node', short for 'fully-validating node', which means that it fully validates all transactions and blocks, as opposed to trusting a 3rd party or someone else's ledger. In summary, a dcrd full node:

* Fully validates all transactions and blocks (by enforcing the Decred consensus rules),
* Maintains the entire past transactional ledger of Decred,
* Relays newly mined blocks,
* Gives the ability to mine blocks,
* Allows relaying of transactions to other Decred nodes around the world (by sharing a transaction mempool),
* Allows sharing a list of peers in the Decred network so that each new peer can talk to as many other peers as possible.

In terms of benefits, since dcrd fully validates every block and transaction, it provides the highest security and privacy possible when used with a wallet that’s also in full validation mode. This is ideal for individuals, businesses, and services that need the most reliable and accurate data about transactions.

## Full node distinctions
As Decred builds out its infrastructure, it becomes apparent that the underlying security is a high priority. Each time a new service is added, it increases the opportunity for node participation. This is done on multiple levels, and it’s important to note that not every node is equal. There are two factors to consider when determining the usefulness of a node:

**Uptime**

* High-uptime (running 24/7/365, or close to it)
* Low-uptime (running intermittently)

**With inbound connections**

* No (default)
* Yes (requires the user to open up a port in their firewall)

**dcrd configuration options include**

* High-uptime with inbound connections
* High-uptime without inbound connections
* Low-uptime with inbound connections
* Low-uptime without inbound connections

The full node that supports the network the best has high-uptime and allows inbound connections. Let's flesh out WHY people would be incentivized to allow inbound connections?

**Incentives**

What would incentivize someone to run a dcrd server with high-uptime and inbound connections? There's maintenance hassle, hardware and electricity costs, and some inherent security risk by exposing a port in their network firewall so that dcrd can have inbound connections from the public internet.

This is one of the many differences between Bitcoin and Decred. In the Bitcoin network, there's no real incentive for people to run their own full nodes, other than to not have to trust a 3rd party. People who run Bitcoin nodes are doing it for fun or their own goodwill. However, with Decred, people are incentivized to run full nodes so that they can solo-stake and earn staking rewards.

Note: since many people aren't technical enough to run their own dcrd servers, but still want to participate in staking, Decred created Voting Service Providers (VSPs). VSPs allow staking, but don't require people to run a server or mess with their firewalls. These will be discussed later.

**Uptime**

Solo-staking requires people to be actively watching the chain and validating new blocks. Therefore, high-uptime is important if you don't want to miss a vote!

**Connections**

dcrd is hardcoded to only ever create 8 outbound connections - https://docs.decred.org/faq/configuration/#5-why-am-i-connecting-to-only-8-outbound-peers -- . Conversely, dcrd allows 125 inbound connections by default, but the server operator needs to open up a hole in their firewall for any of those inbound connections to be used.

What's the difference between inbound and outbound connections? If your node initiated the connection to an external peer, it's outbound. Otherwise, it's inbound. Outbound/inbound connections don't share different types of data. Nodes will send and receive data from both types of connections exactly the same way.

Without firewall changes, dcrd will only ever have 8 connections maximum. By allowing dcrd to have inbound connections through their firewall, solo-stakers get to be connected to more peers (up to 125 more). This means they can receive messages propagating through the network faster, and they're also less vulnerable to things like eclipse or sybil attacks. Getting messages faster is important, especially if you want to get your vote included in the latest block.

**Simple Payment Verification (SPV)** is not a node, but a wallet function. It allows the use of a Decred wallet without having to download the entire Decred blockchain. A wallet operating in SPV mode only needs to download full blocks containing transactions relevant to it and block headers. This reduces the wallet’s hardware requirements and greatly reduces the initial load time for new wallets. When an SPV wallet initialises, it will connect to the Decred network using dcrd peer connections.

## Example:
When you run dcrd for the first time, it needs to figure out where to look for the blockchain so it can start downloading blocks. dcrd has a hardcoded list of seeders that it queries for IPs of known good nodes. It connects to those nodes and starts downloading blocks.

With each connection a node makes, it shares its own connections, like saying "here are all the IP addresses I know of who run dcrd." Each node builds its own list of peers to check and ask, "hey, do any of you have any new blocks?" Full nodes can do this without accepting inbound connections. They still need to maintain a list of peers to query for each outbound connection.

However, imagine if nobody opened up inbound connections through their firewall. Every dcrd node would just continually reach out to the IP addresses in their peers list, asking "Hey, can I talk to you? Do you have new blocks?" And each firewall would just block all traffic. No nodes would be able to talk to each other.

The point is that somebody has to open up their inbound connection to allow their node to be publicly accessible. The more people that do this will increase the security and decentralisation of the network. 

## Other nodes in the network
Decred has a multitude of services that run dcrd nodes in one way or another. Some of these options also include incentives for participation, which in turn encourages users to run a node that fully supports the network. For example, you're incentivised to run a full node so that you don't have to trust a 3rd party. IF you're staking, you're incentivized to both have high-uptime (so you won't miss a vote) AND allow inbound connections (so you have more peers, meaning you receive messages propagating through the network earlier, meaning you won't miss a vote).

## Decred services and dcrd

**Decrediton** can be run either as a fully validating node or in SPV mode. Wallets will never have an open inbound connection. The main reason for this is because wallets usually only run for short periods of time, not as a long-running background process. Allowing other dcrd instances to connect to an instance which only runs intermittently is actually bad for the network, because every instance connected is going to have to find a replacement peer once the wallet is disconnected. Its better if they just connect to a long-lived peer in the first place.

Wallets running in fully validating mode allow for maximum personal privacy and security. On the other hand, SPV mode is great for mobile wallets or when a device has limited resources. 

**Lightning Network** nodes are run as fully validating and for maximum accessibility can have an open inbound connection. LN operators are also incentivised, to run a full node that supports the network, with the fees from conducting transactions over the Lightning Network.

**Voting Service Providers (VSP)** A VSP server needs a reliable RPC connection to a dcrd node. As not to depend on external services it's convenient to run a full node dcrd besides a VSP server and for maximum accessibility it can have an open inbound connection. As an incentive, VSP users pays a fee (normally when the ticket is purchased) and in return the VSP will vote with the ticket when that ticket is called by the network for voting (4 weeks later on average). This allows the VSP user to not run their solo voting wallet 24/7 and go offline as soon as the fee is paid to the VSP.

**DCRDEX Operators** need access to trusted full nodes for each of the assets supported. While operation via a surrogate blockchain data service such as a block explorer is potentially feasible, as it is with all Decred services. It would entail significant security risks and threat of funds being stolen.  

## Conclusion
Running a fully validating node is the best way of understanding how the network is performing. When you participate in the decentralisation of the network, you understand what it takes to run it and the levels to which you are contributing. 

It occurs to me, from my research here, that decentralisation is a collective endeavour, and making the system and your investment more secure means your participation is necessary. In centralised products, you can rely on someone else to run the system. In fully decentralised products, you are the system and the responsibility sits squarely at your feet.

In the past, I’ve been criticised for liking the fact that Decred’s blockchain size is so small. My rebuttal has always been, “Try running your favourite blockchain, and then you’ll understand!”. I relish in the knowledge that every time I turn on Decrediton (in fully validation mode) I’m looking at the full blockchain and have the latest information at my fingertips. 

From a personal perspective, I’m secure! The next step for me is to add security to the network by running a top-tier node with an open inbound connection running 24/7/365.

## Technical specifications for running dcrd
* 16 GB disk space (as of April 2022, increases over time, 2 GB/yr)
* 2 GB memory (RAM)
* 150 MB/day download, 1.5 GB/day upload
* Plus one-time initial download of the entire blockchain
* Windows, macOS Linux, OpenBSD and FreeBSD are also supported
* Preferably high uptime with an open inbound connection

## References
* Decred dcrd – https://github.com/decred/dcrd

* btcd: Not your mom’s Bitcoin daemon -> "Separate Chain and Wallet" section - https://blog.conformal.com/btcd-not-your-moms-bitcoin-daemon/
* btcwallet and btcgui: Wallet handling for btcd -> "The Wallet Daemon: btcwallet" section - https://blog.conformal.com/btcwallet-and-btcgui-wallet-handling-for-btcd/

* Special thanks to @zippycorners for contributing to this article and explaining how publicly accessible nodes work
* Special thanks to @bee, @richardred, @bochinchero, @jholdstock for helping out with the research, fact and error checking for this piece
