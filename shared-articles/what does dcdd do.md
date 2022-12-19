
Blockchain technology is perhaps one of the most important innovations of the century. It's a complex fusion of tools and protocols like networking, cryptography, privacy, security, ownership, trustless communication, governance, etc. A true blockchain is permissionless, which means anyone can use the blockchain without asking permission. However, people who use blockchains are inherently agreeing to the rules that the blockchain runs on. Those rules are (hopefully) established by consensus. Each of those consensus rules actually have to be implemented into software, which is what enforces the rules. As such, it's important to delve into the software that's enabling and enforcing the rules on a blockchain for everyone's benefit.

Blockchains are a public ledger which are distributed among a peer-to-peer network of computers. There is no central server that stores the ledger. It doesn't exist out there, somewhere in the void. The ledger is stored on people's computers. If a new computer connects to the network and asks for the ledger, it downloads the ledger from multiple peers. 

The immutable nature of the information being transmitted and stored is the distinct difference between blockchain and a conventional network. Effectively, this is a book of accounts, better known as a ledger, which is synchronised across all fully participating computers (nodes). To participate, each computer needs to carry the ledger in its entirety and synchronise with other computers and the pool of new transactions. 

The ledger is made up of individual pages which are known as blocks, and each block is linked with a unique code which makes it hard to reverse or manipulate the historic information stored. 

The software that makes this possible on the Decred blockchain is dcrd, which is known as a full node implementation of Decred (written in Go – golang). It acts as a fully validating chain daemon for the Decred cryptocurrency. A daemon is a computer program that runs as a background process, rather than being under the direct control of an interactive user. You can consider dcrd to be your personal Decred blockchain server.

## dcrd responsibilities:
dcrd is the backbone of Decred’s peer to peer network and has specific processes to conduct to keep the network functioning. Running a full node with dcrd contributes to the overall security of the network and increases the available paths for transactions and blocks to relay.

* dcrd maintains the entire past transactional ledger of Decred
* Allows relaying of transactions to other Decred nodes around the world
* Maintains a transaction pool
* Relays newly mined blocks
* and finally ensures all transactions follow the rules

In terms of benefits, since dcrd fully validates every block and transaction, it provides the highest security and privacy possible when used with a wallet that’s also in full validation mode. This is ideal for individuals, businesses, and services that need the most reliable and accurate data about transactions.

## Node Hierarchy
As Decred builds out its infrastructure, it becomes apparent that the underlying security is a high priority. Each time a new service is added, it increases the opportunity for node participation. This is done on multiple levels, and it’s important to note that not every node is equal.

**A top tier fully validating node** is a dcrd unit run either as a stand-alone piece of software or as part of a service for 24 hours, 7 days a week, 365 days a year. This node has an inbound port open, so it can be publicly accessible for other nodes to connect to. This full node is the one that adds security to the chain and makes the project more decentralised. 

**Side note: **There is also an option for running dcrd over the Tor network for greater privacy and security.

**A second tier fully validating node** is a dcrd unit running intermittently or continuously, with the default settings which don’t include an open inbound port. This is not a publicly accessible node, which means other nodes in the network can’t connect to it, but it can connect to them. This full node is perfect for validating chain information and is good for personal privacy and security. This node setup doesn’t add to the security of the chain or make the project more decentralised.

**Simple Payment Verification (SPV)** is not a node, but a wallet function. It allows the use of a Decred wallet without having to download the entire Decred blockchain. A wallet operating in SPV mode only needs to download full blocks containing transactions relevant to it and block headers. This reduces the wallet’s hardware requirements and greatly reduces the initial load time for new wallets. When an SPV wallet initialises, it will connect to the Decred network using dcrd peer connections.

## Example:
When you run dcrd for the first time, it needs to figure out where to look for the Blockchain, so it can start downloading blocks. dcrd has a hardcoded list of seeders and when you start dcrd for the first time it will query the seeders for IPs of known good nodes and then connect to those and starts downloading blocks.

But then with each connection it makes, the nodes talk and share their connections, like saying, "hey here are all the IP addresses I know of who run dcrd." And so, your node will start building its own list of dcrd peers to check and ask, "hey, do any of you have any new blocks?" And it can do that without accepting new inbound connections. That's how it works for people who don't want to open up their inbound connection.

But if nobody opened up their inbound connection through their firewall, then all these dcrd nodes would be reaching out to the IP addresses in their peers list and asking "hey, can I talk to you? Do you have new blocks?" And the firewall would just block all the traffic and no peers would be able to talk to each other.

The point is that somebody has to open up their inbound connection to allow their node to be publicly accessible. The more people that do this will increase the security and decentralisation of the network. 

## Other nodes in the network
Decred has a multitude of services that run dcrd nodes in one way or another. Some of these options also include incentives for participation, which in turn encourages users to run a top tier fully validating node. What options do we have?
 
**Decrediton** can be run either as a fully validating node or in SPV mode. For security reasons, wallets will never have an open inbound connection. Wallets running in fully validating mode allow for maximum personal privacy and security. On the other hand, SPV mode is great for mobile wallets or when a device has limited resources. 

**Lightning Network Channels** are run as fully validating nodes and for maximum accessibility can have an open inbound connection. LN operators are also incentivised with the fees from conducting transactions over the Lightning Network. For the best performance, these nodes should run constantly 24/7/365.

**Voting Service Providers (VSP)** are run as fully validating nodes and for maximum accessibility can have an open inbound connection. VSP operators are also incentivised with the fees for conducting ticket transactions. For the best performance, these nodes should run constantly 24/7/365 and have +4 instances to increase reliability.

**DCRDEX Operators** need access to trusted full nodes for each of the assets supported. While operation via a surrogate blockchain data service such as a block explorer is potentially feasible, it would entail significant security risks. 

?? What other services could I add, and how do they interact with nodes ??

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
* Windows 10, macOS, Linux

## References
* Decred dcrd – https://github.com/decred/dcrd
* Special thanks to @zippycorners for contributing to this article and explaining how publicly accessible nodes work
* Special thanks to @richardred @bochinchero @jholdstock for helping out with the research for this piece
