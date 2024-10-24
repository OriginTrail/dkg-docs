---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# DKG Edge node architecture

The V8 DKG Edge node is intended for customisability and extensibility, enabling builders to take it's official code as a project "boilerplate" and extend it to fit their needs.&#x20;

It is based on a SoA architecture, providing multiple services designed for separation of concerns. See below block scheme for a high level overview of the architecture

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-23 at 13.58.52.png" alt=""><figcaption></figcaption></figure>

The following table describes each of the services and links to their respective repositories:



<table><thead><tr><th width="194">Service</th><th width="309">Description</th><th>Github repo</th></tr></thead><tbody><tr><td>Knowledge Mining API</td><td>Performs knowledge mining via knowledge mining pipelines, taking in various input formats to ultimately produce serialized outputs (JSON-LD), intended to then be published via the Publishing Service</td><td><a href="https://github.com/OriginTrail/edge-node-knowledge-mining">https://github.com/OriginTrail/edge-node-knowledge-mining</a></td></tr><tr><td>DRAG API</td><td>DRAG (Decentralized Retrieval-Augmented Generation) is a service for building decentralized RAGs using data from the Decentralized Knowledge Graph (DKG). It enables querying and processing data with tools like SPARQL, LLMs, and vector databases, delivering answers from decentralized, verifiable sources.</td><td><a href="https://github.com/OriginTrail/edge-node-drag">https://github.com/OriginTrail/edge-node-drag</a></td></tr><tr><td>Edge Node User Interface</td><td>The UI for accessing and utilizing all Edge node functionalities.</td><td><a href="https://github.com/OriginTrail/edge-node-interface">https://github.com/OriginTrail/edge-node-interface</a></td></tr><tr><td>Edge Node API</td><td>The Edge node backend serves as the orchestrator, coordinating operations and interactions between various services.</td><td><a href="https://github.com/OriginTrail/edge-node-api">https://github.com/OriginTrail/edge-node-api</a></td></tr><tr><td>Knowledge Graph DB Instance</td><td>An instance of an RDF enabled triple store, such as Amazon Neptune, Ontotext Graph DB, Blazegraph, Apache Jena or others. </td><td>Respective project repos</td></tr><tr><td>LLM services</td><td>Large Language Model services used by the Edge Node and chosen by the developer, enabling utilizing either local or external LLM based services (e.g. Ollama, OpenAI, Claude etc)</td><td>Respective project repos</td></tr><tr><td>Publishing Service</td><td>Responsible for creating Knowledge Assets on the DKG, intended to take inputs from the Knowledge Mining API</td><td>Part of Edge Node API repo<br></td></tr><tr><td>Authentication Service</td><td>Acts as the authentication hub for all Edge node services and serves as the central source for global configuration and custom parameters.</td><td><a href="https://github.com/OriginTrail/edge-node-authentication-service">https://github.com/OriginTrail/edge-node-authentication-service</a></td></tr><tr><td>Blockchain interface</td><td>The Edge node communicates with the blockchain through an array of RPC endpoints, configurable by the user.</td><td>No specific repo, please consult the documentation on setting up nodes and RPC endpoints</td></tr><tr><td>DKG V8 Network Runtime (ot-node)</td><td>Network runtime service, responsible for communicating with other DKG nodes</td><td><a href="https://github.com/OriginTrail/ot-node">https://github.com/OriginTrail/ot-node</a></td></tr><tr><td>Operational DBs</td><td>Various small databases used for operational purposes</td><td>Deployed with respective services</td></tr></tbody></table>

