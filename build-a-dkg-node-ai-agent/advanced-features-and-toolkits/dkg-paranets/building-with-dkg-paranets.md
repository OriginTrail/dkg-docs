# Build with Paranets

Paranets are like "virtual" knowledge graphs on the OriginTrail Decentralized Knowledge Graph (DKG). Building with them is quite similar to building on the DKG in general. However, paranets enable you to contain your operations services on these "virtual" graphs, e.g., querying a specific paranet with SPARQL or adding a knowledge collection\* to a specific paranet.

{% hint style="info" %}
\***A** **knowledge collection (KC)** is a **collection of Knowledge Assets.** It refers to structured data that can be stored, shared, and validated within a distributed network.
{% endhint %}

To gain access to the paranet knowledge graph, you can use one of the [public DKG nodes](../../../dkg-knowledge-hub/useful-resources/public-nodes.md), or deploy a [DKG node](../../../graveyard/everything/dkg-core-node/) and set it up to host the paranet (or "sync" it). More information is available on the [Sync a DKG Paranet](syncing-a-dkg-paranet.md) page.

**A direct code example of paranets in use can be found here -** [**Paranet Demo**](https://github.com/OriginTrail/dkg.js/blob/v8/develop/examples/paranet-demo.js)

### Querying paranets

Once you have access to the paranet knowledge graph via a gateway node, you can use one of the [DKG SDKs](../dkg-sdk/) to interact with it. It is also possible to open up your triple store SPARQL endpoint directly and query the paranet knowledge graph in its own repository (the paranet repository name is equivalent to the paranet profile Knowledge Asset UAL, with dash characters instead of slash).&#x20;

Using SPARQL, it is possible to query and integrate knowledge from multiple paranets and whole DKG in one query using SPARQL federated queries. &#x20;

### Running paranet services

Paranets enable registering and exposing both on-chain and off-chain services associated with it. A paranet service can be identified by all users of the paranet via its registry Knowledge Asset and can have multiple on-chain accounts associated with it, enabling them to engage in economic activity within the DKG. Examples of paranet services are AI agents (e.g., autonomous reasoners mining knowledge collections), chatbots (e.g., [Polkabot](https://polkabot.ai/)), oracle feeds, LLMs, dRAG APIs, etc.

Paranet operators manage the services through the Paranet Services Registry smart contracts or DKG SDK.&#x20;

### Paranet permissions

There are three permission policies for paranet:

* Nodes access policy—defines which nodes can sync the _paranet_:
  * OPEN—Any node can sync the _paranet._
  * PERMISSIONED — Only approved nodes can sync the _paranet_.
* Miners access policy—defines which knowledge miners can add knowledge to the _paranet_:
  * OPEN—Any address can submit a knowledge asset to the _paranet._
  * PERMISSIONED — Only approved addresses can submit a knowledge asset to the _paranet_.
* Knowledge asset submission access policy:
  * OPEN—Any knowledge asset can be added to the _paranet._
  * STAGING—Knowledge miners first submit the knowledge asset to staging, where it is reviewed by curators chosen by the paranet owner. The curators can _approve_ (and automatically add knowledge asset to the paranet) or _deny_ staged knowledge asset(which then doesn't get added to the paranet).



