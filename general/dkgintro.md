# OriginTrail - Decentralized Knowledge Graph \(DKG\)

## What is a decentralized knowledge graph?

A **decentralized knowledge graph \(DKG\)** is a global shared knowledge graph that is designed to benefit organizations and individuals by providing shared public infrastructure for knowledge exchange. 

The OriginTrail DKG:

* removes central authorities - is hosted on the OriginTrail Decentralized Network \(ODN\)
* utilizes DIDs & Verifiable Credentials for identity and assertions management
* enables Dapps with search, integration, analytics, AI and ML capabilities for any data source: blockchains, IPFS, enterprise systems, web services, personal devices
* enables permissionless PUBLISH and QUERY operations

The OriginTrail Decentralized Network is an implementation of the OriginTrail DKG. With the ODN therefore you can **query for data across a multitude of systems** \(discovery\), to **exchange it** via several data exchange protocols and **integrate it** in your own local knowledge graph or data store. 

_To jump right into the code, head over to the_ [_Getting Started_](../developers/getting-started.md) _page._

## System architecture

We distinguish several layers of the DKG:

* **the network layer**, formed by a peer to peer swarm of DKG nodes hosted by individuals and organisation
* **data layer**, hosting the knowledge graph data, distributed across the network
* **service layer**, implementing various core & extended services, such as authentication, standard interfaces and data pipelines
* **the consensus layer**, which



![](../.gitbook/assets/origintrail-technical-stack.png)

Dataset are uploaded on ODN through a Data Creator node, which could be from any number of business functions, including existing ERPs, blockchains \(permissioned and permissionless\), etc. A cryptographic data hash of the data is first fingerprinted to a blockchain to ensure data immutability. This data is then passed \(via a bidding process through a smart contract\) to three Data Holder nodes that agree to hold the data for the terms of a contract. Data holder nodes are essentially decentralized, interconnected servers and provide that data upon demand to relevant parties. 

![Schematic of the interaction between network nodes, enterprise connections, and the blockchain layer](../.gitbook/assets/origintrail-decentralized-network.png)

ODN is integrated to Ethereum and xDAI blockchains, where businesses and users can choose which one they prefer based on their preferences in terms of fees and security. Upcoming integration to Polkadot is planned for Q3 2021.

The bidding process is completely random and cannot be influenced in any way by any of the parties. Payment is utilized through the Trace Token \(TRAC\) which is the glue between all entities and is used as both a stake \(to keep data holders honest and data immutable\) and a payment \(to compensate data holders for their time and resources\). More information on TRAC utility and economics can be found [HERE](trac.md).

Data creators can [set the data to be public or private](https://medium.com/origintrail/linking-data-in-supply-chains-to-bring-much-needed-resilience-to-global-businesses-8a2ed51cc928), have the data expire after a required time \(i.e. months or years\), or have that data \(or parts of data\) shared only with appropriate parties. Sensitive data is protected using zero-knowledge methods in a privacy-by-design approach. These data holding nodes also function as a vast, decentralized knowledge graph to connect data sets across companies/users quickly and efficiently. This core feature of the ODN is a groundbreaking utility of the protocol, as searching for inter-related data between partners has not been possible before.

![](../.gitbook/assets/image%20%285%29.png)





