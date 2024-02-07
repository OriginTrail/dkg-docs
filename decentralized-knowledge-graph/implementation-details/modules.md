---
description: OriginTrail node building blocks
---

# Modules

Ot-Node is composed of various modules that can easily be added or removed. It's even possible to have different implementations of the same module, making the ot-node very flexible.

As soon as you run the node, module configurations are picked up from the **config.json** file and used for module initialization.  All modules must be initialized for a node to run properly.&#x20;

### Module types

#### The Blockchain module

The ot-node blockchain module enables interactions with multiple blockchains in order to perform operations of the OriginTrail protocol. To learn more about the OriginTrail blockchain layer visit [blockchains.md](../../general/blockchains.md "mention").

#### Triple store module

The entire DKG state is replicated and sharded across the ODN network. Each node persists their designated replicas in their individual local triple stores (graph databases). The triple store module is responsible for connecting and communicating to a triple store avaiable to the ot-node. There are several triple store implementations supported directly at the moment:

* [Ontotext GraphDB](https://www.ontotext.com/products/graphdb/)
* [Blazegraph](https://blazegraph.com/)
* [Apache Jena Fuseki](https://jena.apache.org/documentation/fuseki2/)

However due to the standard implementation (W3C RDF / SPARQL standards) it is easy to integrate with any standardized RDF triple store.&#x20;

The triple store module utilizes [the Communica framework](https://comunica.dev/) under the hood.&#x20;

#### Validation module

The validation module is used to validate assertions seen on the network. More information on assertions can be found [here](../dkg-basic-concepts.md#dkg-assertions).

#### Auto updater module

If enabled, this module takes care of automatic updates of the local node. Every 15 minutes, it checks if the remote (git) version is different than the local version of ot-node, and if it is, local node will be updated to the latest version of the code. After a successful update, node will be restarted and start running on the latest version.&#x20;

#### Network module

The network module takes care of all network RPC communication between nodes in the DKG. It is utilized for implementing the necessary protocol choreographies such as the publishing choreography. Under the hood it is utilizing an implementation of [_Kademlia_](https://en.wikipedia.org/wiki/Kademlia).&#x20;

#### Http client module

Client applications use http requests to communicate with the node. The Http client module implements the endpoints at which requests can be made and defining ot-node's response to http requests.&#x20;

#### Repository module

The repository module is responsible for establishing connections with the operational database and storing, updating, deleting commands and operations data. Storing commands and operations states makes the node fault tolerant, making it possible to, in e.g. the case of node restart, continue from the last preserved state of operation and continue working from where it left off.&#x20;

We expect additional modules to be added in the future based on the evolution of the DKG implementations.

