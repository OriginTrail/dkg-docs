---
icon: hexagon-image
---

# Decentralized Knowle﻿dge Graph (DKG)

OriginTrail Decentralized Knowledge Graph (DKG) presents a global, open data structure comprised of interlinked **Knowledge Assets structured in an RDF knowledge graph** hosted on an open, permissionless decentralized network of DKG nodes. It's designed to support the [**verifiable Internet for AI**](../../dkg-v6-previous-version/ecosystem-white-paper.md) based on an open, permissionless knowledge economy in which knowledge is the primary asset class.

As a builder, you can create **collaborative knowledge graphs** using DKG paranets, incentivize the growth of your knowledge graph with Initial Paranet Offerings (IPOs), with a combination of public and private (and hybrid) [Knowledge Assets](https://origintrail.io/products/knowledge-assets), and use them within an ecosystem of composable services on multiple blockchains.

In hopes of a better understanding of DKG, the analogy can be compared to traditional centralized SQL solutions like so.

<table><thead><tr><th>DKG</th><th>SQL Server</th><th data-hidden></th></tr></thead><tbody><tr><td>Paranet</td><td>Database</td><td></td></tr><tr><td>Knowledge collection</td><td>Table</td><td></td></tr><tr><td>Knowledge asset</td><td>Individual record (row)</td><td></td></tr><tr><td>Triplets</td><td>Values (columns)</td><td></td></tr></tbody></table>

OriginTrail DKG strongly focuses on interoperability through standards such as semantic web standards (RDF, SPARQL, JSON-LD, etc.), Verifiable Credentials and Decentralized Identifiers (DIDs) by W3C, as well as GS1 standards such as the [Digital Link](https://www.gs1.org/standards/gs1-digital-link) and [EPCIS 2.0](https://www.gs1au.org/standards/epcis) for real-world asset tracking (and to which OriginTrail core developers have actively contributed to).

OriginTrail DKG is multi-chain, integrating with Ethereum and Polkadot ecosystem blockchains such as Gnosis, NeuroWeb, Base, and others. It is fueled by the TRAC utility token, which is used to manage relations between DKG network participants.&#x20;

There are many ways to participate, such as:

* Building dapps with [DKG SDKs](../../dkg-v6-previous-version/dkg-sdk/)&#x20;
* Launching DKG paranets
* Publishing knowledge to the DKG via knowledge mining&#x20;
* [Delegating TRAC tokens](../../delegated-staking/delegated-staking-introduction/) to DKG nodes to help secure the network and earn TRAC&#x20;
* [Running DKG Core Nodes](../../build-with-dkg/dkg-core-node/), helping to host the DKG network, and earning TRAC node operator fees&#x20;
* Open-source contributions [to DKG code](../../useful-resources/contribute/)
* Aharing your ideas and joining the discussion in [Discord](https://discord.gg/xCaY7hvNwD), [Telegram](https://t.me/origintrail), [Reddit](https://www.reddit.com/r/OriginTrail/), [X](https://x.com/origin_trail)&#x20;

### Why combine blockchain with knowledge graphs?

Blockchains and knowledge graphs are two different types of networks:

* **Blockchains are trust networks**. They run on decentralized stateful protocols enabling a verifiable shared state and are used for applications such as decentralized identity, asset tokenization (NFTs), decentralized finance, trusted multi-party computation, etc.
* **Knowledge graphs are semantic networks.** When Google first coined the term "knowledge graph", they explained it as "things, not strings". Knowledge graphs connect highly structured, machine-understandable semantic entities into one **semantic data network.** This enables powerful data capabilities, such as search, reasoning, inference, recommendations, and other forms of symbolic AI. Knowledge graphs inherit the technology stack idea of the [Semantic Web](https://en.wikipedia.org/wiki/Semantic_Web) (introduced as the "original" Web 3.0 by Sir Tim Berners-Lee, the inventor of WWW). They are particularly well positioned for use with LLMs as they provide highly contextualized knowledge (or annotated data)

{% hint style="info" %}
If you are looking to jump right into the code, head over to the [DKG SDK](../../build-with-dkg/dkg-sdk/) page.
{% endhint %}

## System architecture

OriginTrail synergizes blockchains and knowledge graphs in a layered architecture.&#x20;

**Blockchains are trust networks** established to enable reliable computation through **decentralized consensus**, operating as a global, dependable computer. In contrast, **knowledge graphs serve as semantic data networks** for **knowledge management**. The OriginTrail architecture is crafted to ensure a trustworthy environment for AI applications by leveraging these two fundamental layers.

<figure><img src="../../.gitbook/assets/Screenshot 2024-06-13 at 23.54.29.png" alt=""><figcaption><p>The three layers of OriginTrail</p></figcaption></figure>

The following sections of the documentation dive deep into each of the two technical layers and their interplay.

We distinguish several sub-layers of the DKG layer (Layer 2):

* **Data layer**, hosting the knowledge graph data, distributed across the network in separate instances of graph databases.
* **Service layer**, implementing various core & extended services, such as authentication, standard interfaces, and data pipelines.
* **Consensus layer**, implementing interfaces to several blockchains hosting trusted smart contracts, used to manage relations between the nodes and implement trustless protocols (currently supporting Ethereum, xDai blockchain, and the OriginTrail NeuroWeb).
* **Application layer,** encompassing both dapps and traditional applications which utilize the OriginTrail DKG as part of their data flows.

<div align="center"><img src="../../.gitbook/assets/Screenshot 2022-03-30 at 16.46.10.png" alt="OriginTrail conceptual architecture"></div>

We also distinguish between:

* **Public, replicated knowledge graph**, shared by all network nodes according to the protocol.
* **Private graphs**, hosted separately by each of the networked nodes, connected with the public knowledge graph.

The public knowledge graph enables data discoverability by hosting a decentralized index of information replicated across the network, enabling search queries through its discovery protocols. Once information is discovered in separate (private) graphs, data exchange protocols are used to obtain full query results. An example of a data exchange protocol is a data marketplace protocol, implementing trusted data-for-tokens exchange.

The protocol actors are:

* Data creator nodes (DC), responsible for publishing datasets to the DKG
* Data holder nodes (DH), hosting the DKG datasets, incentivized by tokens deposited by DCs
* Data viewers (DV), usually services or dapps that query the DKG
* Data providers (DP), which provide data to DC nodes for publishing

The distinction between DC and DH nodes is only behavioral, as they implement the same interfaces (each node can be both a DH and a DC node at the same time).

Therefore, a dataset published to the DKG by a DC node:

* Contains a cryptographic identity (DID) of the DC and DP, rooted in one of the supported blockchain networks
* Is structured as graph-linked data
* Has a corresponding set of cryptographic fingerprints (graph merkle roots) stored immutably on a blockchain
* Is timestamped and has a "data lifespan" on the network&#x20;
* Is randomly replicated across peers based on a DKG content addressing scheme

In this way, any given graph vertex or edge (triple/chunk) in the DKG can be verifiably associated with a publisher DID, its originating dataset, and cryptographic hashes proving it is contained in that dataset, as well as enabling data integrity verification on-chain and off-chain.&#x20;
