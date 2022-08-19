# OriginTrail - Decentralized Knowledge Graph (DKG)

## What is the OriginTrail Decentralized Knowledge Graph?

OriginTrail Decentralized Knowledge Graph (DKG) is an open, collaborative network combining **blockchain** and **knowledge graph** technology. The core unit of the network - the OriginTrail node - is the ultimate data service for your Web3 applications. OriginTrail DKG is a powerful Web3 backend, and together with DKG SDK you can create graph-native Web3 applications, interfacing with verifiable assets on the DKG.

OriginTrail connects to multiple blockchains, such as Ethereum, Polkadot (via [OriginTrail Parachain](../blockchain-layer-1/origintrail-parachain/origintrail-parachain-evm.md)), Polygon, Gnosis and more to come. It is fuelled by the TRAC token, which is used to manage relations between DKG network participants. Running an OriginTrail node also makes you one of the contributors to hosting the DKG and makes you eligible for earning TRAC token rewards.

As a developer using the OriginTrail DKG you can create and maintain **Web3 asset graphs** - immutable, queryable and searchable graphs that can be used across Web3 applications. You can additionally apply standardized technologies such as GS1 EPCIS, RDF/SPARQL, JSON-LD and other W3C and GS1 standards out of the box.

### Why combine Blockchain with Knowledge Graphs?

Blockchains and knowledge graphs are two different types of networks:

* **blockchains are trust networks**. They run on decentralized stateful protocols enabling a verifiable shared state, and are used for applications such as Decentralized identity, Asset tokenization (NFTs), Decentralized Finance, Trusted multi-party computation etc
* **knowledge graphs are semantic networks.** When Google first coined the term "knowledge graph", they explained it as "things, not strings". Knowledge Graphs connect highly structured, machine-understandable, semantic entities into one **semantic data network,** enabling powerful data capabilities, such as search, inference, recommendations, advanced machine learning and others. Knowledge graphs inherit the technology stack idea of the [Semantic Web](https://en.wikipedia.org/wiki/Semantic\_Web) (introduced as the "original" Web3.0 by Sir Tim Berners-Lee, the inventor of WWW)

The two technologies are combined in the **OriginTrail** **Decentralized Knowledge Graph**, in a materialized vision of the **Semantic Web3** - a user owned, data centric, trusted, semantic web.

{% hint style="info" %}
_If you are looking to jump right into the code, head over to the_ [_Getting Started_](../developers/getting-started.md) _page._
{% endhint %}

## System architecture

The OriginTrail tech stack is purposefully designed to bring real world assets into the Web3, enabling discoverability, verifiability and connectivity of physical and digital assets in one coherent Web3 data ecosystem.&#x20;

Two key requirements necessary for such Web3 infrastructure are the ability to ensure **trust via decentralized consensus** and utilize **semantic, verifiable asset data** for representing complex real world relationships and characteristics (such as ownership, location, business context, etc).

These distinct requirements require two distinct types of technology mentioned above  - blockchains and knowledge graphs.

**Blockchains are trust networks**, designed to enable trusted computation through **decentralized consensus**, behaving like a global, trusted computer processor. **Knowledge graphs** on the other hand are semantic data networks. Powering systems of Google, NASA, Amazon and others, knowledge graphs are connected graph data structures, best for representing complex assets and their relationships in the real world.&#x20;

The OriginTrail tech stack leverages blockchains and knowledge graphs by incorporating them into **two network layers**.



![OriginTrail combines blockchains and knowledge graphs in it's two layer infrastructure](<../.gitbook/assets/image (8).png>)



The following sections of the documentation dive deep into each of the two technical layers and their interplay.&#x20;



We distinguish several sub-layers of the DKG layer (Layer 2):

* **the network layer**, formed by a peer to peer swarm of DKG nodes hosted by individuals and organisations, implementing S/Kademlia
* **data layer**, hosting the knowledge graph data, distributed across the network in separate instances of graph databases
* **service layer**, implementing various core & extended services, such as authentication, standard interfaces and data pipelines
* **the consensus layer**, implementing interfaces to several blockchains hosting trusted smart contracts, used to manage relations between the nodes and implement trustless protocols (currently supporting Ethereum, xDai blockchain and the OriginTrail Polkadot Parachain)
* **application layer,** encompassing both Dapps and traditional applications which utilize the OriginTrail DKG as part of their data flows.

![OriginTrail conceptual architecture](<../.gitbook/assets/Screenshot 2022-03-30 at 16.46.10.png>)

We also distinguish between:

* the **public, replicated knowledge graph**, shared by all network nodes according to the protocol
* **private graphs**, hosted separately by each of the networked nodes, connected with the public knowledge graph

The public knowledge graph is used to enable data discoverability by hosting a decentralized index of information, replicated across the network, enabling search queries through its discovery protocols. Once information is discovered in separate (private) graphs, data exchange protocols are used to obtain full query results. An example of a data exchange protocol is a data marketplace protocol, implementing trusted data-for-tokens exchange.

The protocol actors are:

* data creator nodes (DC), responsible for publishing datasets to the DKG
* data holder nodes (DH), hosting the DKG datasets, incentivised by tokens deposited by DCs
* data viewers (DV), usually services or dapps that query the DKG
* data providers (DP), which provide data to DC nodes for publishing

The distinction between DC and DH nodes is only behavioural, as they implement the same interfaces (each node can be both a DH and a DC node at the same time).

\*\* Currently data providers need to run their own DC nodes to publish data to the network, which is about to change in version 6 with the introduction of gateway services.

Therefore, a dataset published to the DKG by a DC node:

* contains a cryptographic identity (DID) of the DC and DP, rooted in one of the supported blockchain networks
* is structured as graph linked data
* has a corresponding set of cryptographic fingerprints (graph merkle roots) stored immutably on a blockchain
* is timestamped and has a "data lifespan" on the network&#x20;
* is randomly replicated across peers based on a DKG content addressing scheme

In this way, any given graph vertex or edge (triple) in the DKG can be verifiably associated with a publisher DID, its originating dataset and cryptographic hashes proving it being contained in that dataset, as well as enabling data integrity verification on-chain & off chain.&#x20;



