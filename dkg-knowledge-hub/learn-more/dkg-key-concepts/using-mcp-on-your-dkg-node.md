# Using MCP on your DKG Node

## How does the DKG work with MCP?

By registering the DKG as a tool provider in an MCP server, you can:

* **Query knowledge** using tools like `query_dkg_by_name`, which execute SPARQL queries over the DKG
* **Publish knowledge** from unstructured text using tools like `create_knowledge_asset`, which turn LLM-generated content into structured JSON-LD and publish it to the DKG
* Expand the tools above and add additional tools to interact with the DKG (e.g. creating Knowledge Assets from websites or documents)

This allows agents using MCP-compatible clients to:

* Interact with real-time, decentralized knowledge
* Add to the shared memory layer used by other agents
* Benefit from data provenance, versioning, and ownership built into the DKG

<figure><img src="../../../.gitbook/assets/Microsoft Copilot demo infographic.png" alt=""><figcaption><p>Example of DKG integration with the Microsoft Copilot Agent</p></figcaption></figure>

### Why is this powerful?

MCP makes it easy to build modular, agent-based systems where LLMs use tools to:

* Ask questions against the Decentralized Knowledge Graph
* Write and revise their own memory as JSON-LD Knowledge Assets
* Store results and publish new discoveries collaboratively

When paired with the DKG, this gives LLM-based systems access to a decentralized knowledge base that is:

* **Interoperable** (via RDF and schema.org)
* **Trustworthy** (anchored with cryptographic proofs)
* **Queryable** (via SPARQL and linked data tooling)

To get started:

* Explore the [dkg-mcp-server example repo ](https://github.com/OriginTrail/dkg-mcp-server)
* Try integrating the DKG into your MCP server
* Build agents that reason over, expand, and query the decentralized web of knowledge

### See it in action - DKG & Microsoft Copilot agent integration via MCP

{% embed url="https://www.youtube.com/watch?v=_S5cNdwAGsQ" %}
