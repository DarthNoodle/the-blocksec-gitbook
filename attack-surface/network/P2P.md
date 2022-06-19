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


## Variations


## Functions

### Connecting To Peers

### Broadcasting Blocks


### Broadcasting Transactions/Mempool




[^1]: Bitcoin Developer: P2P Network
  https://developer.bitcoin.org/devguide/p2p_network.html
[^2]: Horizen Academy: P2P - PEER-TO-PEER NETWORK
  https://academy.horizen.io/technology/advanced/a-peer-to-peer-p2p-network/

