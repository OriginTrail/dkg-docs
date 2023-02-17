# DKG Basic concepts

OriginTrail Decentralized Knowledge Graph (DKG) combines several standardized components from both  blockchain and knowledge graph technologies. The core primitive of the DKG is the "Knowledge Asset", explained together with other important components below.

### What is a Knowledge Asset?

A knowledge asset is an ownable container for your valuable information that can describe any physical thing, documents, abstract concepts, numbers and strings. It lives in a decentralized knowledge graph which makes it easily discoverable, while your information integrity and knowledge asset ownership are safeguarded by the underlying blockchain.

More precisely, a Knowledge Asset is a web resource identified by Uniform Asset Locators (or UAL, which is an extension of the traditional URL), consisting of

* the asset graph, which contains the knowledge asset **data**, represented in RDF , stored on the DKG (and not on the blockchain)
* Immutability proofs & ownership record: consisting of asset graph state **proofs** and **ownership record**, represented using a non-fungible token stored on a blockchain.

<figure><img src="https://lh4.googleusercontent.com/Cr4oefUxDeNxFWsnoJzp9b_N3aaQ85W8UUJJ8psliceQqM5X4SxSWNlKgij_UrkNXcsI6Re50hYOWBbIO8lMc5oNPRGVVfM6PeptRfb40DavCxR7Kl33eud6gZ51WIqh90acwVR-L_EZQpv6Aer9bog" alt=""><figcaption><p>The anatomy of a Knowledge Asset</p></figcaption></figure>

Asset graphs are formed of **assertions**, which represent asset content states. An assertion is represented using the n-quads serialization (stored on the DKG) and a cryptographic fingerprint used for assertion verification (n-quads graph Merkle root, stored immutably on the blockchain). Each assertion can be independently verified for integrity, by recomputing the cryptographic fingerprint by the verifier and comparing if the computed result matches with the corresponding blockchain fingerprint record.

Knowledge Assets can contain both public and private data - the public assertion data being replicated on the OriginTrail Decentralized Network and publicly available, and private assertion data contained within the private domain of the asset owner (e.g. OriginTrail Node run by the asset owner, such as a person or company).

In summary, a knowledge asset is a combination of an NFT record and a semantic record. Using the dkg.js SDK you will be able to perform CRUT (create, read, update, transfer) operations with Knowledge assets, which will be explained in further detail below.\


More information about [Knowledge Assets.](knowledge-assets.md)

### What is RDF?

The Resource Description Framework (RDF) is a W3C standardized model designed to represent data about physical objects and abstract concepts (resources). It’s a model to express relations between entities using a graph format.

RDF Schemas provide mechanisms for describing related resources and their relationships. It is similar to object-oriented programming languages and differs in that it describes properties in terms of resource classes. RDF enables querying via the SPARQL query language.

[More information about RDF Schemas used for Knowledge Assets](knowledge-assets.md)

[Examples of Schemas Definitions by schema.org](https://schema.org/docs/schemas.html)

### What is an NFT?

NFT - short for a non-fungible token - is a type of a blockchain token, used as an implementation component of knowledge assets in the OriginTrail Decentralized Knowledge Graph. The token is used to represent ownership of the knowledge asset, and enables the owner of the knowledge asset to perform all standardized NFT functionality with it, such as to transfer the ownership of their knowledge assets, list them on NFT marketplaces and use their knowledge assets as rich-NFTs in Web3 applications.

\
If you are interested in learning more about NFTs, you can find out more [here](https://en.wikipedia.org/wiki/Non-fungible\_token).

### What is a UAL?

Universal Asset Locators are ownable identifiers of the DKG, similar to URLs in the traditional web. The UALs follow the DID URL specification and are used to identify and locate a specific Knowledge Asset within the OriginTrail Decentralized Knowledge Graph (DKG). UAL consists of 5 parts:

* did (decentralized identifier) predicate
* dkg (decentralized knowledge graph) predicate
* blockchain identifier (otp = OriginTrail Parachain)
* blockchain address (such as the address of the relevant asset NFT smart contract)
* identifier specific to the contract, such as the ID of the NFT token
* query and fragment components



More information on DID URLs can be found [here](https://www.w3.org/TR/did-core/#did-url-syntax)

{% hint style="info" %}
This page is a WIP and is currently being updated (Q1 2023)
{% endhint %}

<figure><img src="https://documents.lucid.app/documents/f47b9383-e097-4900-a1cc-4a0dd8f92d7e/pages/cOGrK2Oo9ApD?a=845&#x26;x=-1625&#x26;y=128&#x26;w=1450&#x26;h=306&#x26;store=1&#x26;accept=image%2F*&#x26;auth=LCA%20a95999ac650cc24e34a8a53424c1b104bc59d0cc-ts%3D1676043825" alt=""><figcaption></figcaption></figure>

**To see the DKG in action, continue to the** [**DKG SDK section**](dkg-sdk/)****
