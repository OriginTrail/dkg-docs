# Building with DKG paranets

Paranets are like "virtual" knowledge graphs on the OriginTrail DKG and building with them is quite similar to building on the DKG in general. Paranets enable you to however contain your operations services on these "virtual" graphs, e.g. querying a specific paranet with SPARQL, or adding a knowledge asset to a specific paranet.

To gain access to the paranet knowledge graph you can deploy a DKG [gateway node](../node-setup-instructions/running-a-gateway-node.md) and set it up to host the paranet (or "sync" it). More information is available on the [sync-a-dkg-paranet.md](../node-setup-instructions/sync-a-dkg-paranet.md "mention") page.

### Querying paranets

Once you have access to the paranet knowledge graph via a gateway node, you can use one of the[ DKG SDKs](../dkg-sdk/) to interact with it. It is also possible to open up your triple store SPARQL endpoint directly and query the paranet knowledge graph in its own repository (the paranet repository name is equivalent to the paranet profile knowledge asset UAL, with dash characters instead of semicolons).&#x20;

Using SPARQL it is possible to query and integrate knowledge from multiple paranets in one query using SPARQL federated queries. &#x20;

### Running paranet services

Paranets enable registering and exposing both on chain and off chain services associated with it. A paranet service can be identified by all users of the paranet via its registry knowledge asset, and can have multiple on-chain accounts under its control, enabling them to engage in economic activity within the DKG. Examples of paranet services are AI agents (e.g. autonomous reasoners mining knowledge assets), chatbots (e.g. [Polkabot](https://polkabot.ai/)) , oracle feeds, LLMs, DRAG APIs etc.

Paranet operators manage the services through the Paranet Services Registry smart contracts.&#x20;
