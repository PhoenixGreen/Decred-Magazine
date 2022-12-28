
Blockchain technology is perhaps one of the most important innovations of the century. It's a complex fusion of tools and protocols like networking, cryptography, privacy, security, ownership, trustless communication, governance, etc. A true blockchain is permissionless, which means anyone can use the blockchain without asking permission. However, people who use blockchains are inherently agreeing to the rules that the blockchain runs on. Those rules are (hopefully) established by consensus. Each of those consensus rules actually has to be implemented into software, which is what enforces the rules. As such, it's important to delve into the software that's enabling and enforcing the rules on a blockchain for everyone's benefit.

Blockchains are public ledgers which are distributed among a peer-to-peer network of computers. There is no central server that stores the ledger. It doesn't exist out there, somewhere in the void. The ledger is stored on people's computers. If a new computer connects to the network and asks for the ledger, it downloads the ledger from multiple peers. 

To fully participate in the network, a computer needs to carry the ledger in its entirety, verify that the ledger is following all the consensus rules, and synchronize with the rest of the network so that all the other participants maintain an identical ledger.

There's strength in numbers. It's possible that a single, malicious, participant could invent a new ledger that makes them a multi-billionaire. However, if the majority of everyone else on the network is following the same consensus rules, it would be impossible for that malicious participant to give their malicious ledger to everyone else. Everyone else would just reject it, saying: "No, this doesn't follow the rules."

Therefore, since the network participants are each following the same set of rules, and everyone is sharing the same ledger between each other, it's practically impossible to go back and retroactively alter the ledger. You can only add new information to the ledger. That's what makes old blocks immutable.

The software that makes this all possible on the Decred blockchain is dcrd. dcrd is written in Go (golang), and implements all the consensus rules and core blockchain ledger functionality. It is important to note that dcrd does NOT include wallet functionality, and was designed that way for security reasons. You can consider dcrd to be your personal Decred blockchain server, which would connect you to the rest of the Decred network.

## dcrd responsibilities:
dcrd is the backbone of Decred's peer-to-peer network. dcrd acts as a 'full node', short for 'fully-validating node', which means that it fully validates all transactions and blocks, as opposed to trusting a 3rd party or someone else's ledger. In summary, a dcrd full node:

* Fully validates all transactions and blocks (by enforcing the Decred consensus rules),
* Maintains the entire past transactional ledger of Decred,
* Relays newly mined blocks,
* Gives the ability to mine blocks,
* Allows relaying of transactions to other Decred nodes around the world (by sharing a transaction mempool),
* Allows sharing a list of peers in the Decred network so that each new peer can talk to as many other peers as possible.

In terms of benefits, since dcrd fully validates every block and transaction, it provides the highest security and privacy possible when used with a wallet that’s also in full validation mode. This is ideal for individuals, businesses, and services that need the most reliable and accurate data about transactions.

## Full Node Distinctions
As Decred builds out its infrastructure, it becomes apparent that the underlying security is a high priority. Each time a new service is added, it increases the opportunity for node participation. This is done on multiple levels, and it’s important to note that not every node is equal. There are two factors to consider when determining the usefulness of a node:

**Uptime**
* High-uptime (running 24/7/365, or close to it)
* Low-uptime (running intermittently)
**With inbound connections**
* No (default)
* Yes (requires the user to open up a port in their firewall)

**Dcrd configuration options include**
* High-uptime with inbound connections
* High-uptime without inbound connections
* Low-uptime with inbound connections
* Low-uptime without inbound connections

The Full node that supports the network the best is the High-uptime with inbound connections.

**Simple Payment Verification (SPV)** is not a node, but a wallet function. It allows the use of a Decred wallet without having to download the entire Decred blockchain. A wallet operating in SPV mode only needs to download full blocks containing transactions relevant to it and block headers. This reduces the wallet’s hardware requirements and greatly reduces the initial load time for new wallets. When an SPV wallet initialises, it will connect to the Decred network using dcrd peer connections.

## Example:
When you run dcrd for the first time, it needs to figure out where to look for the Blockchain so it can start downloading blocks. dcrd has a hardcoded list of seeders that it queries for IPs of known good nodes. It connects to those nodes and starts downloading blocks.

With each connection a node makes, it shares its own connections, like saying "here are all the IP addresses I know of who run dcrd." Each node builds its own list of peers to check and ask, "hey, do any of you have any new blocks?" Full nodes can do this without accepting inbound connections. They still need to maintain a list of peers to query for each outbound connection.

However, imagine if nobody opened up inbound connections through their firewall. Every dcrd node would just continually reach out to the IP addresses in their peers list, asking "Hey, can I talk to you? Do you have new blocks?" And each firewall would just block all traffic. No nodes would be able to talk to each other.

The point is that somebody has to open up their inbound connection to allow their node to be publicly accessible. The more people that do this will increase the security and decentralization of the network. 

## Other nodes in the network
Decred has a multitude of services that run dcrd nodes in one way or another. Some of these options also include incentives for participation, which in turn encourages users to run a node that fully supports the network. For example, you're incentivised to run a full node so that you don't have to trust a 3rd party. IF you're solo-staking, you're incentivised for your full node to have a high uptime and allow inbound connections to your node.

## Decred Services and dcrd

**Decrediton** can be run either as a fully validating node or in SPV mode. Wallets will never have an open inbound connection. The main reason for this is because wallets usually only run for short periods of time, not as a long-running background process. Allowing other dcrd instances to connect to an instance which only runs intermittently is actually bad for the network, because every instance connected is going to have to find a replacement peer once the wallet is disconnected. Its better if they just connect to a long-lived peer in the first place.

Wallets running in fully validating mode allow for maximum personal privacy and security. On the other hand, SPV mode is great for mobile wallets or when a device has limited resources. 

**Lightning Network Wallets** are run as fully validating nodes and for maximum accessibility can have an open inbound connection. LN operators are also incentivised, to run a full node that supports the network, with the fees from conducting transactions over the Lightning Network.

**Voting Service Providers (VSP)** are run as fully validating nodes and for maximum accessibility can have an open inbound connection. VSP operators are also incentivised with the fees for conducting ticket transactions. For the best performance, these nodes should run constantly 24/7/365 and have +4 instances to increase reliability.

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
* Windows 11, OpenBSD and FreeBSD are also supported
* Preferably High uptime with an open inbound connection

## References
* Decred dcrd – https://github.com/decred/dcrd
* Special thanks to @zippycorners for contributing to this article and explaining how publicly accessible nodes work
* Special thanks to @richardred @bochinchero @jholdstock for helping out with the research for this piece
