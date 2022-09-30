---
description: OriginTrail node building blocks
---

# Modules

Ot-Node is composed of various modules that can easily be added or removed. It's even possible to have different implementations of the same module, making the ot-node very flexible.

As soon as you run the node, module configurations are picked up from the **config.json** file and used for module initialization.  All modules must be initialized for a node to run properly.&#x20;

### Module types

#### Auto updater

If enabled, this module takes care of automatic updates of the local node. Every 15 minutes, it checks if the remote(git) version is different than the local version of ot-node, and if it is, local node will be updated to the latest version of the code. After a successful update, node will be restarted and start running on the latest version.&#x20;

#### Http client

Client applications use http requests to communicate with the node. But, how should they know which endpoints to hit? This problem is solved with Http client module, which is used for defining the endpoints at which requests can be made and defining ot-node's response to http requests.&#x20;

#### Network module

Whenever an asset is published,  it's content is hashed and replicated to _k_ nodes closest to it's hashed value on the network. Closeness is calculated using the XOR metric. Network module is in charge of finding the right nodes and storing an asset on found nodes. Essentially, we're using [_Kademlia_](https://en.wikipedia.org/wiki/Kademlia)'s _find peers_ and _store_ operations.&#x20;

#### Repository

Repository module is responsible for establishing connections with the database and storing, updating, deleting commands and operations data. Storing commands and operations states makes the node fault tolerant; making it possible to, in the case of node failure, just return to last preserved state and continue working from where it left off.&#x20;

#### Triple store

DKG's assets are persisted in the graph databases. This module is responsible for connecting and communicating to the graph database where assets are stored. There are multiple triple store implementations:

* blazegraph
* fuseki
* graphdb

#### Validation

After the publishing on an assertions is started, it's content is transformed into [_nquads_](https://www.w3.org/TR/n-quads/)_,_ and then used as leaves of a [Merkle tree](https://en.wikipedia.org/wiki/Merkle\_tree). Assertion id is the root of a Merkle tree. Transforming an assertion to nquads format and creating the assertion id is done on the client side, but after the request is passed to the ot-node, validation module is used to validate the _nquads_ and _assertion id_ format. &#x20;

#### Blockchain

Information about published assets is also persistent on the blockchain, making it public and unmodifiable. Blockchain module enables the node to use smart contract's functions as needed. To learn more about the OriginTrail blockchain layer visit [blockchains.md](../../general/blockchains.md "mention").
