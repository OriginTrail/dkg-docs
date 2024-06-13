# 🔌 DKG Basic concepts

OriginTrail Decentralized Knowledge Graph (DKG) combines several standardized components from both blockchain and knowledge graph space. The core primitive of the DKG is the "Knowledge Asset", explained together with other important components below.

### What is a Knowledge Asset?

A knowledge asset is an ownable container for your valuable information that can describe any physical thing, documents, abstract concepts, numbers and strings. It lives in a decentralized knowledge graph which makes it easily discoverable, while your information integrity and knowledge asset ownership are safeguarded by the underlying blockchain.

More precisely, a Knowledge Asset is a web resource identified by Uniform Asset Locators (or UAL, which is an extension of the traditional URL), consisting of

* the asset graph, which contains the knowledge asset **data**, represented in RDF, stored on the DKG (and not on the blockchain)
* Immutability proofs & ownership record: consisting of asset graph state **proofs** and **ownership record**, represented using a non-fungible token stored on a blockchain.

<figure><img src="https://lh4.googleusercontent.com/Cr4oefUxDeNxFWsnoJzp9b_N3aaQ85W8UUJJ8psliceQqM5X4SxSWNlKgij_UrkNXcsI6Re50hYOWBbIO8lMc5oNPRGVVfM6PeptRfb40DavCxR7Kl33eud6gZ51WIqh90acwVR-L_EZQpv6Aer9bog" alt=""><figcaption><p>The anatomy of a Knowledge Asset</p></figcaption></figure>

Asset graphs are formed of **assertions**, which represent asset content states. An assertion is stored on the DKG with a cryptographic fingerprint used for verification. Each assertion can be independently verified for integrity, by recomputing the cryptographic fingerprint by the verifier and comparing if the computed result matches with the corresponding blockchain fingerprint record.

Technically, an assertion is represented using the n-quads serialization (stored on the DKG) and a cryptographic fingerprint used for assertion verification (n-quads graph Merkle root, stored immutably on the blockchain).

Knowledge Assets can contain both public and private data - the public assertion data being replicated on the OriginTrail Decentralized Network and publicly available, and private assertion data contained within the private domain of the asset owner (e.g. OriginTrail Node run by the asset owner, such as a person or company).

In summary, a knowledge asset is a combination of an NFT record and a semantic record. Using the dkg.js SDK you will be able to perform CRUT (create, read, update, transfer) operations with Knowledge assets, which will be explained in further detail below.

#### State finality

Similar to distributed databases, the OriginTrail Decentralized Knowledge Graph applies replication mechanisms and needs mechanisms to reach a consistent state on the network for knowledge assets. In OriginTrail DKG, state consistency is reconciled using the blockchain, which hosts state proofs for knowledge assets, as well as replication commit information from DKG nodes. This means that updates for an existing knowledge asset are accepted by the network nodes (similar to the way nodes accept knowledge assets on creation) and can operate with all accepted states.

There are three phases for a state of a knowledge asset:

* LATEST: which indicates the Knowledge Asset state pending for an update, awaiting commits from DKG nodes. Once commits are received, the state transitions to LATEST\_FINALIZED.
* LATEST\_FINALIZED: latest committed state, accepted by the network.
* HISTORICAL: any previously finalized state, identifiable by its state hash.

More information about [Knowledge Assets.](broken-reference)

### What is RDF?

The Resource Description Framework (RDF) is a W3C standardized model designed to represent data about physical objects and abstract concepts (resources). It’s a model to express relations between entities using a graph format.

RDF Schemas provide mechanisms for describing related resources and their relationships. It is similar to object-oriented programming languages and differs in that it describes properties in terms of resource classes. RDF enables querying via the SPARQL query language.

[More information about RDF Schemas used for Knowledge Assets](broken-reference)

[Examples of Schemas Definitions by schema.org](https://schema.org/docs/schemas.html)

### What is an NFT?

NFT - short for a non-fungible token - is a type of a blockchain token, used as an implementation component of knowledge assets in the OriginTrail Decentralized Knowledge Graph. The token is used to represent ownership of the knowledge asset, and enables the owner of the knowledge asset to perform all standardized NFT functionality with it, such as to transfer the ownership of their knowledge assets, list them on NFT marketplaces and use their knowledge assets as rich-NFTs in Web3 applications.

\
If you are interested in learning more about NFTs, you can find out more [here](https://en.wikipedia.org/wiki/Non-fungible\_token).

### What is a UAL?

Universal Asset Locators are ownable identifiers of the DKG, similar to URLs in the traditional web. The UALs follow the DID URL specification and are used to identify and locate a specific Knowledge Asset within the OriginTrail Decentralized Knowledge Graph (DKG). UAL consists of 5 parts:

* did (decentralized identifier) predicate
* dkg (decentralized knowledge graph) predicate
* blockchain identifier (otp:2043 = OriginTrail NeuroWeb Mainnet)
* blockchain address (such as the address of the relevant asset NFT smart contract)
* identifier specific to the contract, such as the ID of the NFT token
* query and fragment components

An example UAL may look like this:

```
did:dkg:otp:2043/0x5cac41237127f94c2d21dae0b14bfefa99880630/318322
```

This UAL refers to the decentralized knowledge graph on the mainnet, it's blockchain address is `0x5cac41237127f94c2d21dae0b14bfefa99880630` and the ID of the token is `318322`.

More information on DID URLs can be found [here](https://www.w3.org/TR/did-core/#did-url-syntax).

**To see the DKG in action, continue to the** [**DKG SDK section**](dkg-sdk/)**.**
