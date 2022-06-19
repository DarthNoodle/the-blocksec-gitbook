# Peer To Peer Communications
## Introduction
A Peer-to-peer (P2P) network utilises a distributed architecture approach that partitions tasks between peers.  All peers on a network are equal; this means they all perform the exact same function and are both a client and server with regards to data transfer and propagation.

So what do the different P2P networks types look like [^2]:

![P2P Network Type](images/p2p.network.types.jpg)

### Centralised (A)
The centralised model takes the form of your typical client/server model where you have numerous clients all trying to connect to a centralised resource.  An example of this would be users browsing a website (the web browser is the client and web server is the.. server).

### Decentralised (B)
A decentralised network operates on a similar concept to its Centralised predecessor, however instead of having a central focal server which clients attempt to connect.  There are multiple servers that are separated (e.g. geotropically) where clients are able to connect to any available server.  This increases the fault-tolerance and load distribution, however the server's are still centralised and prone to attacks such as Denial of Service.

An example of such an implementation would be to upload a static website to a CDN network.  In which case the CDN nodes are geographically distributed, web clients will then access the closest CDN node.

### Distributed (C)
In Distributed networks all peers/nodes are treated equally; this means they act as both the client and server.  Peers will maintain a connection list of other peers on the network. The client aspect will query each connected peer for additional information (e.g. what's your block height?) where as the server aspect of a peer would process the request then respond with the relevant data (e.g. I am on block 1337, here is the block).

All peers (lets ignore light clients for a moment) on the network will have a copy of data, this means the network is extremely resilient to fault tolerant events that may occur (e.g. such as a DOS attack).

## Purpose
The most important part of a P2P network is the communication between nodes.  Blockchain data is considered secure because every node (ignoring light clients & sharding for now) on the network should have a copy of data; nodes would have a constant need to communicate with each other in order to keep data/events (such as blocks or new transactions) synchronised across the network.  As such, the distributed network described above seems like the most logical choice [^1].

P2P protocols should also ensure not only the availability of on-chain data but also the availability of nodes on the network.  This means a connecting client should be able to obtain enough information about the network, by just querying a small number of online nodes [^2].

Running a node/peer can be costly from a resource (person-hours/CPU/RAM/HDD) perspective.  To encourage network participants, each network has introduced incentives for performing these vital network functions.  In the case of cryptocurrency, such incentives would take the form of being awarded an allocation of coins for performing a network function (e.g. such as producing a new block);  this provides economic incentives to further strengthen the network.


## Functions
Peers within a blockchain network all have a number of specific/critical functions to perform.  These same functions would also be targeted by would-be attackers; attempting to compromise or disrupt the network.

### Connecting To Peers
Connecting to peers is one of the most critical aspects of a P2P network;  if your a newly created node, how does that node where to connect and how to obtain information?

In most instances a node will first attempt to utilise [DNS seed nodes](attack-surface/network/DNS.md) where a pre-defined list of domains/hosts will be queried.  In a similar fashion, a list of static IP addresses can also be used should the host system not have functioning DNS.

It would also be possible to manually specify IP addresses within the node configuration file; this would permit the node to only talk to trusted nodes [^2].

What sort of things happen once a node is connected? It would query its connected nodes for:

+ List of Other Peers
+ Current Block Height
+ Current Mempool (Uncommitted Transactions)

As a newly connecting node it would be possible to query any node on the network and receive this information.  This could then be performed recursively in order to build up a bigger topological picture and to further mature/establish links into the network [^1].

Once the node has built up sufficient knowledge (e.g. peer list, current block height) it will then start the process of `Initial Block Download` or will sync its current records utilising a similar process.


### Initial Block Download (IBD)





### Broadcasting Blocks


### Broadcasting Transactions/Mempool




[^1]: Bitcoin Developer: P2P Network
  https://developer.bitcoin.org/devguide/p2p_network.html
[^2]: Horizen Academy: P2P - peer-to-peer network
  https://academy.horizen.io/technology/advanced/a-peer-to-peer-p2p-network/
