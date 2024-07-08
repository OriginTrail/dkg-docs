# 🔌 DKG Basic concepts

The OriginTrail Decentralized Knowledge Graph (DKG) combines several standardized components from both blockchain and knowledge graph technologies. The core primitive of the DKG is the "knowledge asset" (KA), the _"molecule"_ of the DKG.\


### Knowledge Assets

A knowledge asset is an ownable container of knowledge that can describe any digital or physical object, abstract concept, or really any "thing". It lives in a decentralized knowledge graph which makes it easily discoverable, while its information integrity and ownership are supported by the blockchain.

More precisely, a Knowledge Asset is a web resource identified by Uniform Asset Locators (or UAL, which is an extension of the traditional URL), consisting of

* **knowledge:** in the form of graph data (RDF) and vector embeddings, stored on the DKG (not on the blockchain)
* **cryptographic proofs**:  representing cryptographic digests of the **knowledge,** stored on the blockchain
* **Uniform Asset Locator:** globally unique URI with assigned ownership using blockchain accounts, implemented as a non-fungible token on the blockchain

<figure><img src="../.gitbook/assets/Screenshot 2024-06-13 at 22.59.48.png" alt=""><figcaption></figcaption></figure>

The knowledge content can be observed as a time series of knowledge content states, or **assertions**.  Each assertion can be independently verified for integrity, by recomputing the cryptographic fingerprint by the verifier and comparing if the computed result matches with the corresponding blockchain fingerprint record.

Technically, an assertion is represented using the n-quads serialization and a cryptographic fingerprint used for assertion verification (n-quads graph Merkle root, stored immutably on the blockchain).

Knowledge Assets can contain both public and private data - the public assertion data being replicated on the OriginTrail Decentralized Network and publicly available, and private assertion data contained within the private domain of the asset owner (e.g. OriginTrail Node run by the asset owner, such as a person or company).

In summary, a knowledge asset is a combination of an NFT record and a semantic record. Using the dkg.js SDK you will be able to perform CRUT (create, read, update, transfer) operations with Knowledge assets, which will be explained in further detail below.

#### State finality

Similar to distributed databases, the OriginTrail Decentralized Knowledge Graph applies replication mechanisms and needs mechanisms to reach a consistent state on the network for knowledge assets. In OriginTrail DKG, state consistency is reconciled using the blockchain, which hosts state proofs for knowledge assets, as well as replication commit information from DKG nodes. This means that updates for an existing knowledge asset are accepted by the network nodes (similar to the way nodes accept knowledge assets on creation) and can operate with all accepted states.

There are three phases for a state of a knowledge asset:

* LATEST: which indicates the Knowledge Asset state pending for an update, awaiting commits from DKG nodes. Once commits are received, the state transitions to LATEST\_FINALIZED.
* LATEST\_FINALIZED: latest committed state, accepted by the network.
* HISTORICAL: any previously finalized state, identifiable by its state hash.

### Decentralized Retreival Augmented Generation

The term Retrieval Augmented Generation (RAG) was coined by Patrick Lewis in a [2020 paper](https://arxiv.org/pdf/2005.11401.pdf) and it represents a technique for enhancing the accuracy and reliability of GenAI models with facts fetched from external sources. This allows AI solutions to dynamically fetch relevant information before the generation process, enhancing the accuracy of responses by limiting the generation to re-working the retrieved inputs.&#x20;

\
**Decentralized Retrieval Augmented Generation (DRAG) advances the model by organizing external sources in a Decentralized Knowledge Graph (DKG) with verifiable sources** made available for AI models to use. The framework enables a hybrid AI system that brings together neural (e.g. LLMs) and symbolic AI (e.g. Knowledge Graph) methodologies. Contrary to using a solely neural AI approach which is based on vector embedding representations, a symbolic AI approach enhances it with the strength of Knowledge Graphs by introducing a basis in the symbolic representation.

DRAG is, therefore, a framework that allows AI solutions to tap into the strengths of both paradigms: the powerful learning and generalization capabilities of neural networks, and the precise, rule-based processing of symbolic AI. It operates on two core components - (1) the DKG paranets and (2) AI models. The dRAG applications framework is entirely compatible with the existing techniques, tools, and RAG frameworks and supports all major data formats.&#x20;

### Knowledge Mining

**Knowledge Mining** is the process of producing high quality, blockchain tracked knowledge for artificial intelligence, pioneered by the OriginTrail ecosystem. This cyclical process leverages the key component of the OriginTrail technology - Knowledge Assets - which are ownable containers for knowledge with inherent discoverability, connectivity and data provenance.

Similarly to the concept of Bitcoin mining, where miners collectively provide computing resources to the network and receive incentives in coins, knowledge miners contributing useful knowledge to the OriginTrail DKG will receive NEURO tokens. With Knowledge Mining incentives enabled across multiple blockchains, the ambition is to drive exponential growth of trusted knowledge in the OriginTrail Decentralized Knowledge Graph.

Read more about knowledge mining at [NeuroWeb docs](https://docs.neuroweb.ai/knowledge-mining).

### RDF & SPARQL

The Resource Description Framework (RDF) is a W3C standardized model designed to represent data about physical objects and abstract concepts (resources). It’s a model to express relations between entities using a graph format.

RDF Schemas provide mechanisms for describing related resources and their relationships. It is similar to object-oriented programming languages and differs in that it describes properties in terms of resource classes. RDF enables querying via the SPARQL query language.

[More information about RDF Schemas used for Knowledge Assets](broken-reference)

[Examples of Schemas Definitions by schema.org](https://schema.org/docs/schemas.html)

### What is an NFT?

NFT - short for a non-fungible token - is a type of a blockchain token, used as an implementation component of knowledge assets in the OriginTrail Decentralized Knowledge Graph. The token is used to represent ownership of the knowledge asset, and enables the owner of the knowledge asset to perform all standardized NFT functionality with it, such as to transfer the ownership of their knowledge assets, list them on NFT marketplaces and use their knowledge assets as rich-NFTs in Web3 applications.

\
If you are interested in learning more about NFTs, you can find out more [here](https://en.wikipedia.org/wiki/Non-fungible\_token).

### What is a UAL?

Uniform Asset Locators are ownable identifiers of the DKG, similar to URLs in the traditional web. The UALs follow the DID URL specification and are used to identify and locate a specific Knowledge Asset within the OriginTrail Decentralized Knowledge Graph (DKG). UAL consists of 5 parts:

* did (decentralized identifier) predicate
* dkg (decentralized knowledge graph) predicate
* blockchain identifier (otp:2043 = OriginTrail NeuroWeb Mainnet)
* blockchain address (such as the address of the relevant asset NFT smart contract)
* identifier specific to the contract, such as the ID of the NFT token
* query and fragment components

An example UAL may look like this:

```
did:dkg:otp:2043/0x5cac41237127f94c2d21dae0b14bfefa99880630/318322#color
```

This UAL refers to the decentralized knowledge graph on the mainnet, it's blockchain address is `0x5cac41237127f94c2d21dae0b14bfefa99880630` and the ID of the token is `318322`and to a property "color" inside its knowledge graph.

More information on DID URLs can be found [here](https://www.w3.org/TR/did-core/#did-url-syntax).

### Autonomus AI Paranets

Next building block of DKG after Knowledge Assets are **AI Para-networks** or **paranets**.

**AI Para-networks** or **paranets** are autonomously operated structures in the DKG, owned by its community as a paranet operator. In paranets, we find assemblies of **Knowledge Assets** driving use cases with associated **paranet-specific AI services** and **an incentivization model** to reward knowledge miners fueling its growth. \
To read more on **Autonomus AI Paranets** go to [#autonomus-ai-paranets](dkg-basic-concepts.md#autonomus-ai-paranets "mention")

**To see the DKG in action, continue to the** [**DKG SDK section**](dkg-sdk/)**.**
