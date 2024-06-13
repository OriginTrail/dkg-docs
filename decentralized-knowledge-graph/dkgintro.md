# 🌐 OriginTrail - Decentralized Knowledge Graph (DKG)

## What is the OriginTrail Decentralized Knowledge Graph?

OriginTrail Decentralized Knowledge Graph (DKG) presents a global, open data structure comprised of interlinked **knowledge assets, structured in a RDF knowledge graph,** hosted on an open, permissionless decentralized network of DKG nodes. It's designed to support [**the Verifiable Internet for AI**](ecosystem-white-paper.md) on the basis of an open, permissionless knowledge economy in which knowledge is the primary asset class.

As a builder you can create **collaborative knowledge graphs** using DKG [paranets](autonomous-ai-paranets/), incentivise the growth of your knowledge graph with [IPOs](autonomous-ai-paranets/initial-paranet-offerings-ipos.md), with a combination of public and private (and hybrid) [knowledge assets](dkg-basic-concepts.md) and use them within an ecosystem of composable services on multiple blockchains.

OriginTrail DKG strongly focuses on interoperability through standards such as semantic web standards (RDF, SPARQL, JSON-LD etc), Verifiable Credentials and Decentralized Identifiers (DIDs) by W3C, as well as GS1 standards such as the [Digital Link](https://www.gs1.org/standards/gs1-digital-link) and [EPCIS 2.0](https://www.gs1au.org/standards/epcis) for real world asset tracking (and to which OriginTrail core developers have actively contributed to).

OriginTrail DKG is multi-chain, integrating with Ethereum and Polkadot ecosystem blockchains such as Gnosis, Neuroweb, Base and others. It is fueled by the TRAC utility token, which is used to manage relations between DKG network participants.&#x20;

There are many ways to participate, such as:

* building dapps with [DKG SDKs](dkg-sdk/)&#x20;
* launching [DKG paranets](autonomous-ai-paranets/)
* publishing knowledge to the DKG via knowledge mining&#x20;
* [delegating TRAC tokens](delegated-staking/) to DKG nodes to help secure the network and earning TRAC&#x20;
* [running DKG nodes,](node-setup-instructions/) and so helping host the DKG network and earning TRAC node operator fees&#x20;
* open source contributions [to DKG code](../useful-resources/contribute/)
* sharing your ideas and joining the discussion in [Discord](https://discord.gg/gYq6GuJ4sJ), [Telegram](https://t.me/origintrail), [Reddit](https://www.reddit.com/r/OriginTrail/), [X](https://x.com/origin\_trail)&#x20;

### Why combine Blockchain with Knowledge Graphs?

Blockchains and knowledge graphs are two different types of networks:

* **blockchains are trust networks**. They run on decentralized stateful protocols enabling a verifiable shared state, and are used for applications such as Decentralized identity, Asset tokenization (NFTs), Decentralized Finance, Trusted multi-party computation etc.
* **knowledge graphs are semantic networks.** When Google first coined the term "knowledge graph", they explained it as "things, not strings". Knowledge Graphs connect highly structured, machine-understandable, semantic entities into one **semantic data network,** enabling powerful data capabilities, such as search, reasoning, inference, recommendations and other forms of symbolic AI. Knowledge graphs inherit the technology stack idea of the [Semantic Web](https://en.wikipedia.org/wiki/Semantic\_Web) (introduced as the "original" Web3.0 by Sir Tim Berners-Lee, the inventor of WWW). They are particularly well positioned for use with LLMs as they provide highly contextualized knowledge (or annotated data)

{% hint style="info" %}
_If you are looking to jump right into the code, head over to the_ [_Getting Started_](broken-reference) _page._
{% endhint %}

## System architecture

OriginTrail synergizes blockchains and knowledge graphs in a layered architecture.&#x20;

**Blockchains are trust networks**, designed to enable trusted computation through **decentralized consensus**, behaving like a global, trusted computer. **Knowledge graphs**, on the other hand, are semantic data networks for knowledge management. Providing a trusted environment for AI applications via these two fundamental layers is what OriginTrail architecture is designed for.

<figure><img src="../.gitbook/assets/Screenshot 2024-06-13 at 23.54.29.png" alt=""><figcaption><p>The three layers of OriginTrail</p></figcaption></figure>

The following sections of the documentation dive deep into each of the two technical layers and their interplay.

We distinguish several sub-layers of the DKG layer (Layer 2):

* **the network layer**, formed by a peer to peer swarm of DKG nodes hosted by individuals and organisations, implementing S/Kademlia
* **data layer**, hosting the knowledge graph data, distributed across the network in separate instances of graph databases
* **service layer**, implementing various core & extended services, such as authentication, standard interfaces and data pipelines
* **the consensus layer**, implementing interfaces to several blockchains hosting trusted smart contracts, used to manage relations between the nodes and implement trustless protocols (currently supporting Ethereum, xDai blockchain and the OriginTrail NeuroWeb)
* **application layer,** encompassing both Dapps and traditional applications which utilize the OriginTrail DKG as part of their data flows.

<div align="center">

<img src="../.gitbook/assets/Screenshot 2022-03-30 at 16.46.10.png" alt="OriginTrail conceptual architecture">

</div>

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

Therefore, a dataset published to the DKG by a DC node:

* contains a cryptographic identity (DID) of the DC and DP, rooted in one of the supported blockchain networks
* is structured as graph linked data
* has a corresponding set of cryptographic fingerprints (graph merkle roots) stored immutably on a blockchain
* is timestamped and has a "data lifespan" on the network&#x20;
* is randomly replicated across peers based on a DKG content addressing scheme

In this way, any given graph vertex or edge (triple/chunk) in the DKG can be verifiably associated with a publisher DID, its originating dataset and cryptographic hashes proving it being contained in that dataset, as well as enabling data integrity verification on-chain & off chain.&#x20;



