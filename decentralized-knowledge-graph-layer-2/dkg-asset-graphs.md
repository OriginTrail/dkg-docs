---
description: The new core primitive of the OriginTrail DKG v6
---

# DKG Asset graphs

From v6 of OriginTrail a new core primitive in the system has been introduced - **DKG asset graphs**, which enable further applications of the OriginTrail DKG.&#x20;

### DKG assets

Formally defined, a **DKG asset graph** is unique digital asset, representing a real-world asset so that it:&#x20;

* **has a unique identifier** - **UAI/UAL**, referring to the&#x20;
* **semantic state** representation of the real-world asset, associated with
* state **mutability**,
* state verifiability **proofs**,&#x20;
* **ownership record**,
* associated **token pools** (optional)

This means that for any asset (e.g. a physical product with a data carrier such as a barcode or RFID, a digital document such as a certificate, or a Web3 asset such as an NFT) an associated DKG Asset graph can be created, indexed and queried for on the network. **OriginTrail v6 allows all these assets to become Web3 ready and makes them easily discoverable, verifiable and valuable.**

An asset graph has therefore a verifiable **state**, in the form of an RDF graph, identifiable and resolvable by its UAI, which is maintained on the DKG replicated across the network. Each asset state is represented by an **assertion.**&#x20;

### DKG Assertions

Creating and updating asset states on the network involves publishing **verifiable graph assertions**. Assertions are based on Verifiable Credentials and their structure consists of:&#x20;

* a unique **assertionID**
* assertion **metadata** - containing indexing information, such as issuer address, timestamps etc
* **assertion data** (asset state) - containing the user provided input data

The verifiability of assertions ensured by storing two cryptographic proofs on a blockchain:

* a **data hash**, which is used as the assertionID, calculated as a hash of the assertion content
* a **root hash** graph Merkle proof, allowing the construction of Merkle proofs, verifying a specific triple being contained in a particular assertion

So in dev lingo, a DKG asset is analogous to a Git repo/branch, and an assertion is similar to a Git commit.

### UAI/UALs

Universal Asset Identifiers/Locators are novel primitives being introduced in the DKG v6, similar to URI/URL scheme on the Web2. UAIs/UALs are based on the standardized URI/URL scheme, incorporating the design ideas and recommendations from W3C Decentralized Identifiers (DIDs) .&#x20;

Using a UAL, any application can resolve a specific asset state graph fragment in the DKG, similar to standard URL resolution.

```
// standard URL
scheme ":" ["//" authority] path ["?" query] ["#" fragment]

// DKG UAL
dkg: [// DID] / UAI ["?" query] ["#" fragment]
```

\*The UAI/UAL implementation is currently in development.

**To see the DKG assets in action, continue to the** [**DKG SDK section**](dkg-sdk/)****
