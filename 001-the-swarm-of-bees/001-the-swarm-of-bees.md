# The Swarm — An Introduction to Bee Nodes

![Explainer](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/banner.png?token=GHSAT0AAAAAAB5ZWRIFARWBHOXX6RI7JL6GY77LLIA "Explainer")

## _What_ is Swarm?

[Swarm](https://medium.com/ethereum-swarm/towards-the-world-computer-the-swarm-network-upgrade-has-started-cfba1ed68330) is a globally distributed p2p storage network that enables a decentralised infrastructure for storage and communication, ready to power the next generation of censorship-resistant, unstoppable, serverless apps.

Swarm’s mission is to shape the future towards a self-sovereign global society with permissionless open markets by providing scalable base-layer infrastructure for the decentralised internet. [Swarm’s vision](https://www.ethswarm.org/swarm-whitepaper.pdf) is to extend the blockchain with peer-to-peer storage and communication to realise the world computer that can serve as an operating system and deployment environment for decentralised applications

![A Swarm of Bees](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/swarm-of-bees.png?token=GHSAT0AAAAAAB5ZWRIFIQPGBXIAIY5NYJEYY77LMLQ "A Swarm of Bees")

_A Swarm of Bees_

Swarm provides continuity of service and resilience against network outages or targeted denial of service attacks. As a platform for permissionless data storage, Swarm fosters freedom of information. With its exceptional privacy features like anonymous browsing, Swarm responds to the growing demand for security on the web.

Swarm is economically self-sustaining due to a built-in [incentive system](https://www.youtube.com/watch?v=qxQrvjKY-Is) enforced through smart contracts on the Gnosis blockchain. Swarm aspires to shape the future towards a self-sovereign global society with permissionless open markets where applications can run autonomously and securely.

Built-in incentives optimise the allocation of bandwidth and storage resources. Swarm nodes track their relative bandwidth contribution on each peer connection and excess debt due to unequal consumption can be settled in BZZ. Swarm users must spend BZZ to purchase the right to write data to Swarm and prepay some rent for long-term storage.

The Swarm network consists of two layers, the underlay network and the overlay network. The underlay network forms the foundation of Swarm. It consists of Bee nodes which connect with each other using the libp2p peer-to-peer network protocol. Bee nodes in the Swarm network identify each other by their “Swarm addresses” which are derived from their Ethereum addresses (overlay network).  

![Swarm’s Layered Design](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/swarm-layered-design.png?token=GHSAT0AAAAAAB5ZWRIFY6SKWFFGCOTWE5KOY77LN4Q "Swarm’s Layered Design")

_Swarm’s Layered Design_

The overlay network is built on top of the underlay and enables the core functionality of Swarm. It consists of a massive [Kademlia](https://en.wikipedia.org/wiki/Kademlia) [Distributed Hash Table](https://en.wikipedia.org/wiki/Distributed_hash_table) (DHT).  A DHT is a decentralized data structure which makes it easy to find the data you are looking for and is built to remain resilient even in the case that some of its participants go offline. A Kademlia DHT is a special implementation of a DHT which is optimized for efficient querying. Decentralized storage providers commonly use Kademlia DHTs to store information about which nodes store which data and are optimized for speedy querying. Swarm’s specialized interpretation of a Kademlia DHT is referred to as the DISC (Distributed Immutable Store for Chunks) and shares many similarities with DHTs used by other decentralized storage systems. However, the key difference is that Swarm stores data directly in the DISC, not just a reference to which node has which file. Furthermore, Swarm nodes do not store whole files —  files are instead broken down into small “chunks” and distributed around the network for efficient retrieval and data redundancy.

For developers, Swarm provides a complete stack of [essential tools](https://www.ethswarm.org/build) to host things like dApps, NFT metadata, media files and more or to build layer 2 solutions such as [Fair Data Protocol](https://fdp.fairdatasociety.org/) on top of Swarm — all in a decentralized way!


## What is a Bee Node?

The Bee node is the heart and workhorse of the Swarm network. It is a peer-to-peer (p2p) node that connects with other peers all over the world to form the Swarm network.

![A Bee Node](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/bee-node-components.png?token=GHSAT0AAAAAAB5ZWRIEZRQHT6IJ3CPVXB6OY77LU3A "A Bee Node")

_A Bee Node_

[Kademlia](https://en.wikipedia.org/wiki/Kademlia) routing ensures that each node in the Swarm network connects to a specific subset of other nodes in such a way that nodes’ local decisions about where to forward **chunks** result in globally optimal routing.

Each node is assigned a Swarm address which is distinct from its network address. Nodes in the Swarm network are grouped into “_[neighbourhoods](https://en.wikipedia.org/wiki/Kademlia#System_details)_” based on their Swarm addresses. By counting the number of prefix bits two Swarm addresses have in common, their degree of proximity or closeness (referred to as _proximity order_) can be defined. Nodes that are closest to each other in this manner form a fully connected neighbourhood. As a result, two nodes might be in the same Swarm “neighbourhood”, but really far apart geographically.

Swarm’s storage scheme declares that each chunk is stored by the nodes with an address that is close to that of the chunk itself. And all nodes in the neighbourhood are expected to store all chunks that fall in that address range.  When a chunk is requested, these chunk requests are routed to their respective neighbourhoods. Any node receiving the chunk request in that neighbourhood is expected to serve the corresponding chunk from its storage. For those who serve the chunk, it is not possible to find out who is the requester or source of the given chunk. Since the nodes do not get to choose which chunks they store, encryption, the ambiguity of context and the lack of leaked metadata all provide them protection against liability for the content they host.


## Types of Bee Nodes

![Full Node, Light Node and Ultra-Light Node](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/types-of-bee-nodes.png?token=GHSAT0AAAAAAB5ZWRIF3HGMILLUZJSVFWVSY77LVVQ "Types of Bee Nodes")
_Full Nodes, Light Nodes and Ultra-Light Nodes_

Bee nodes are highly configurable and can be customized to run in various modes to address a wide range of use cases.

### 1. Full Node: The service provider

Bees running as full nodes together form the backbone of the Swarm network. By running one or more full nodes, you can directly contribute storage and bandwidth to the network and stake BZZ to participate in [storage/bandwidth incentives](https://medium.com/ethereum-swarm/the-mechanics-of-swarm-networks-storage-incentives-3bf68bf64ceb).

![Full Node - Requirements](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/full-node-requirements.png?token=GHSAT0AAAAAAB5ZWRIE2C2D23E65UFZLZFYY77LXPA "Full Node - Requirements")

_Full Node Requirements_

As your Bee full node contributes services to the swarm, you are awarded through the [SWAP](https://docs.ethswarm.org/docs/introduction/terminology#swap) system with `BZZ`; but as your node consumes the service of the swarm, it costs you `BZZ`. Swarm uses [cheques and the ChequeBook](https://docs.ethswarm.org/docs/introduction/terminology#cheques--chequebook) smart contract to enable this process allowing you as a node operator to cash out the cheques received.

You can install and set up your own Bee on any dedicated machine (an unused PC or laptop at home, cloud host or [Raspberry Pi](https://docs.ethswarm.org/docs/installation/rasp-bee-ry-pi)) that has a stable internet connection.


### 2. Light Node

The concept of a light node refers to a special mode of operation necessitated by poor bandwidth environments, e.g. mobile devices on low throughput networks or devices allowing only transient or low-volume storage. Light nodes are primarily consumer nodes, that pay in BZZ for services rendered by _full nodes_. A light node is ideal for researchers, content creators and consumers, who are interested in actively using the Swarm network and enjoying all of Swarm’s features, without the hassle of operating a _full node_ on their own.

Due to its lightweight nature, a light node can be run on most laptops and desktops and can be turned on or off without corrupting the node’s state. 


### 3. Ultra Light Node

Ultra light nodes are for users who want to try out running a light node but don’t want to go through the hassle of blockchain onboarding. However, this imposes some limitations as well.



* Ultra light nodes can download data from Swarm within reasonable bandwidth consumption limits (as long as connected peers allow this freeriding)
* They may get blocklisted by peers for overconsumption of bandwidth
* They cannot upload data to Swarm
* Ideal for beginners testing out Swarm’s decentralized storage services
* They can be safely upgraded to a light or full node 


## Why run a Bee Node?

Although files and data on the Swarm network can be accessed through [public gateways](https://gateway.ethswarm.org/) without running your own node, public gateways often impose various limitations and offer less performance and privacy. Running your own Bee node offers unlimited bandwidth, high performance, and unparalleled privacy and decentralization.


### For Storage Providers

You should run Bee as a full node if you want to contribute storage space (as a storage provider with dedicated hardware) to the Swarm network and benefit from the network’s [storage incentive](https://medium.com/ethereum-swarm/the-mechanics-of-swarm-networks-storage-incentives-3bf68bf64ceb) system.


### For Storage Consumers

You have a few options if, as a storage user, you want to interact with the Swarm network directly on your laptop or desktop without having to run or maintain a full node (for uploading or downloading files, paying for storage):



* Install and run lightweight nodes using the user-friendly [Swarm Desktop App](https://www.ethswarm.org/build/desktop)
* or run Bee as a lightweight node in _[light](https://docs.ethswarm.org/docs/access-the-swarm/light-nodes)_ or _[ultra-light](https://docs.ethswarm.org/docs/access-the-swarm/ultra-light-nodes)_ mode.


### For Builders and Developers

For developers who want to build on the Swarm Network, there are a few options to consider.


#### Run Bee in Developer Mode

Running Bee in [developer mode](https://docs.ethswarm.org/docs/bee-developers/bee-dev-mode) will start a Bee node instance with volatile persistence and all back-ends mocked. As a developer you can interact with all the usual HTTP endpoints, for instance, you can buy postage stamps and use them to upload files, which will be saved to memory.


#### Run a local Swarm network


##### Bee Factory

![Bee Factory](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/bee-factory.png?token=GHSAT0AAAAAAB5ZWRIEBHBG5JLFLRZAL3RAY77LZOA "Bee Factory")

_Bee Factory_

[Bee Factory](https://github.com/ethersphere/bee-factory) offers a complete solution to simulate an entire Swarm Network on your machine. Bee Factory is a CLI tool to spin up a Docker cluster of Bee nodes as well as a test Blockchain for advanced testing and development.


##### FDP Play

![FDP Play](https://raw.githubusercontent.com/rampall/articles/main/001-the-swarm-of-bees/images/fdp-play.png?token=GHSAT0AAAAAAB5ZWRIEBAWHDZJIIBGXMMRQY77L2EA "FDP Play")

_FDP Play_

[Fair Data Protocol](https://fdp.fairdatasociety.org/) (FDP) is a data interoperability protocol and a layer 2 solution built on top of Swarm. It promotes self-sovereignty and privacy for dApps that use personal data in the decentralized cloud.  [FDP Play](https://github.com/fairDataSociety/fdp-play) is the entry point for developers to start building with FDP.

FDP Play is a CLI tool to spin up a local development FDP environment with Docker. It includes a Bee cluster, a FairOS instance and a blockchain node.


## Additional Resources

### Documentation

1. [The Book of Swarm](https://www.ethswarm.org/The-Book-of-Swarm.pdf)
2. [Bee](https://docs.ethswarm.org/docs/dapps-on-swarm/introduction/)
3. [Bee API](https://docs.ethswarm.org/api/)
4. [Bee Debug API](https://docs.ethswarm.org/debug-api/)

### Videos

1. [What is Swarm and how its storage incentives work - Swarm explained](https://www.youtube.com/watch?v=qxQrvjKY-Is)
2. [Join the Swarm: how to run a light node or full node by Attila Gazso | Devcon Bogotá](https://www.youtube.com/watch?v=Q-csUpkbDhc&t=1654s)
3. [Fair Data Protocol ~ FDP-PLAY explained](https://www.youtube.com/watch?v=Mt5468WzWaA&t=6s)

### References

1. [Hello, this is Swarm. A short introduction.](https://medium.com/ethereum-swarm/hello-this-is-swarm-a-short-introduction-bd4b959e5581) (Jan 28, 2022)
2. [A Brief Introduction to Ethereum Swarm](https://medium.com/geekculture/a-brief-introduction-to-ethereum-swarm-db6d79657e60) (Feb 28, 2022)
3. [What’s the Difference Between IPFS and Ethereum Swarm?](https://hackernoon.com/whats-the-difference-between-ipfs-and-ethereum-swarm)
4. [The Mechanics of Swarm network’s Storage Incentives](https://medium.com/ethereum-swarm/the-mechanics-of-swarm-networks-storage-incentives-3bf68bf64ceb) (Nov 23, 2022)
5. [Bella Ciao, data silos](https://mirror.xyz/mfw78.eth/0xImoscth-vf31BzcCnpTBBps9uh1Xrs65XgrwxJDog) (September 21st, 2022)
6. [Building Bridges](https://mirror.xyz/mfw78.eth/1jRBTu8TIoOdbOJ1Xu8bWQsvYLmE7jTZTHvB8QOx2f0) (December 5th, 2022)
7. [How Swarm Makes Internet Decentralized Again](https://getblock.io/blog/how-swarm-makes-internet-decentralized-again/) (June 25, 2021)