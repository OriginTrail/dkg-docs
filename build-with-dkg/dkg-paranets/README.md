---
icon: yelp
---

# DKG paranets

<figure><img src="../../.gitbook/assets/DKG Paranets.png" alt=""><figcaption></figcaption></figure>

**DKG para-networks**, or "**paranets",** are a feature of the OriginTrail Decentralized Knowledge Graph (DKG) designed to enable decentralized, co-owned, and incentivized knowledge graphs.&#x20;

With DKG Paranets, both humans and AI agents can **collaboratively create, curate and maintain knowledge graphs** while ensuring transparency, provenance, and providing incentives for knowledge contributions.&#x20;

### Why Paranets?

Traditional knowledge-sharing mechanisms have limitations:

* Knowledge bases like Wikipedia rely on centralized moderation, which can introduce bias and restrict contributions.
* AI models depend on private datasets, which often lack transparency and introduce biases.
* Scientific discoveries often remain behind paywalls, limiting access and slowing progress.

DKG Paranets provide a decentralized framework for knowledge governance and sharing, addressing these challenges, while maintaining a scalable and flexible semantic data structure perfectly suitable for AI applications.

### Who's who in a paranet?

We distinguish several key roles in a DKG paranet.

* **Knowledge Miners,** which produce new, useful knowledge assets and publish them to the paranet **knowledge graph.** If a miners' knowledge asset is included in an incentivised paranet, they might be eligible for token rewards for their contribution
* **Knowledge Curators,** which "curate" the submitted knowledge assets and decide if they are to be included into the paranet knowledge graph
* **Paranet operators,** who create and manage their paranets
* **Knowledge consumers,** which query the paranet knowledge and use it for their benefit
* [**IPO**](initial-paranet-offerings-ipos/) **voters,** which can support Paranet growth through voting in Initial Paranet Offerings
* an associated **Knowledge Value,** representing the total amount of tokenized knowledge accumulated in the paranet (measured in TRAC). This value is used as a key multiplier for IPO incentives, which are implemented as a ratio. For example, a paranet operator may offer 20 Neuro tokens for each TRAC spent to Knowledge miners as a reward for successfully mined Knowledge Assets.&#x20;

### Paranet structure

Each DKG paranet has a:

* **shared Knowledge Graph, assembled from paranet Knowledge Assets**, published by knowledge miners and stored on the OriginTrail DKG. Depending on the paranet specifics, these knowledge assets conform to a set of paranet rules, such as containing knowledge about a particular topic, data structured according to defined ontology, etc.
* **Staging environment -** where knowledge assets are registred prior to inclusion in a paranet by knowledge curators
* **Paranet Services** registered to the paranet, such as dRAG interfaces, AI agents, smart contracts, data oracles, etc.
* **Incentivization model** specifying the rules under which growth activities in the paranet are rewarded, such as knowledge mining and paranet-specific AI services. The incentivisation system may be kick-started through an Initial Paranet Offering (IPO)
* **a "Home" blockchain** on which the paranet is hosting the **knowledge assets**.

### Some paranet use cases

DKG Paranets provide a structured, transparent knowledge-sharing system where value follows knowledge:

* **High performant AI agent memory** – AI agents can autonomously govern and curate their own knowledge graph based memory using paranets, either individually or as part of agentic swarms. (See more under [ElizaOS agent](../ai-agents/elizaos-dkg-agent.md))
* **Open Scientific Research** – Researchers can publish findings openly while being directly rewarded without paywalls (learn more about such a paranet [here](https://www.youtube.com/watch?v=9O-DB4EftOk))
* **Social intelligence -** paranet knowledge graph driven by social media insights and collaborative inputs ([learn more](https://origintrail.io/blog/growing-the-buz-economy-announcing-the-social-intelligence-paranet-launch))
* **AI Training on Open Data** – AI models can train on decentralized, tokenized knowledge instead of closed, biased datasets.
* **Decentralized Supply Chain Data** – Supply chain participants can contribute, verify, and access immutable records of product origins and movements, enhancing trust and reducing fraud.
* **Collaborative Educational Resources** – Educators and students can co-create knowledge repositories, ensuring open access to high-quality learning materials with verified provenance.
* **Decentralized Journalism** – Independent journalists can publish reports that are verified and co-owned by a decentralized network, reducing misinformation and ensuring accountability.
* **Crowdsourced Innovation** – Communities and organizations can jointly develop and maintain R\&D knowledge bases, allowing open collaboration while ensuring contributions are fairly recognized and rewarded.

<figure><img src="../../.gitbook/assets/Screenshot 2025-02-26 at 17.22.36.png" alt=""><figcaption><p>A paranet knowledge graph example</p></figcaption></figure>

### Decentralized knowledge sharing for AI

The characteristics of a paranet, including its Knowledge Asset parameters and how services are provisioned, are all defined by the **paranet operator.** A paranet operator can be an individual, an organization, a Decentralized Autonomous Organization (DAO), an AI agent, etc. Paranets together form the DKG, leveraging the common underlying network infrastructure. Given the DKG is a permissionless system, anyone can initiate a paranet.

Paranets provide a powerful substrate for AI systems. They leverage network effects of verifiable inputs from multiple sources to receive accurate answers through Decentralized Retrieval-Augmented Generation (dRAG), allowing it to gather information from the graph of public knowledge and privately held knowledge in relevant knowledge collections that it has access to.

In short: Paranets are the first-ever neutral, transparent knowledge-sharing layer where value follows knowledge:

* AI models can train on open, tokenized knowledge instead of closed, biased datasets.
* Scientific research can be published and rewarded directly, bypassing paywalls.
* AI agents can govern their own information ecosystems individually or in swarms.
