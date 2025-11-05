---
description: The engine of the DKG Knowledge Layer
hidden: true
icon: circle-nodes
---

# DKG Core Node

**DKG Core Nodes** are the operational foundation of the OriginTrail Decentralized Knowledge Graph (DKG). They form a permissionless peer-to-peer network that stores, verifies, and makes published knowledge assets available to AI systems and other users. By participating in Random Sampling and responding to publishing activity, they ensure that knowledge remains available and the network remains decentralized.

### What Are DKG Core Nodes?

Core Nodes are designed for reliability, availability, and fair participation. They are incentivized to maintain uptime, publish new knowledge, and offer services to the network in exchange for TRAC rewards.

#### Staking Requirements

To operate a DKG Core Node, a minimum stake of **50,000 TRAC** is required. Nodes with higher stakes gain stronger eligibility in the reward distribution process, as stake directly influences their **Node Power** and visibility to publishers and delegators.

#### Publishing & Gateway Function

DKG Core Nodes can also serve as **Gateway Nodes**, meaning they support the publishing of new Knowledge Assets into the network. Nodes that publish more knowledge gain a higher **publishing factor**, which increases their rewards through the Random Sampling proof system.

To becoeme Gateway nodes, node operators can open their Core Node **publishing API endpoint** to external publishers. This allows developers, AI agents, or platforms to use this Core Node as a gateway service for publishing their knowledge assets - similar to how blockchain RPC providers offer access to blockchain infrastructure. In OriginTrail, however, this access is **incentivized**: if others publish through your Core node, your node's publishing factor grows proportionally improving your Node Power, which improves both your rewards and overall network value.

### Network Services and Fair Pricing

Each DKG Core Node sets a **service ask** - a configurable percentage fee charged when serving publishing transactions. This ask value plays a direct role in network competitiveness:

* Nodes with **lower ask fees** are prioritized by the network
* Ask pricing influences **Node Power**, impacting score in the reward calculation

Over time, tokenomics naturally favor nodes converging on a **fair price point**, where efficient, well-operated nodes benefit from lower ask values that increase their usage and overall rewards. All of this contributes to a fair and open market of DKG services.

### Quality Metrics: Node Power and Node Health

Delegators and publishers alike benefit from understanding two key metrics that determine node performance:

#### Node Power

Node Power is a relative metric that reflects a node’s influence in the network’s reward system. It is calculated from:

* **Staked TRAC** — More stake signals trust and increases reward eligibility
* **Publishing activity** — More published knowledge assets increase score
* **Service ask** — Lower fees improve network competitiveness

A higher Node Power means the node is more likely to earn rewards.

#### Node Health

Node Health tracks how successfully a node is responding to random sampling challenges. It is a relative metric, calculated as:

* The ratio of **successful proofs submitted**
* Compared to the **expected number of proofs** during an epoch

High Node Health indicates reliability and strong uptime - crucial for reward consistency and delegator trust.&#x20;

### What You Need to Operate a Node

Operating a DKG Core Node doesn’t require blockchain or knowledge graph expertise, however **it requires diligent monitoring and maintenance in order for your Core node to attract a sensible amount of TRAC rewards**, including regular updates, maintaining uptime etc. It is recommended to have at least some general knowledge about the DKG, operating Linux servers, long running services and firewalls.&#x20;

We recommend trying it out on the **DKG testnet** to get familiar with the environment. When you're ready, proceed to the Core Node setup guide to learn how to deploy a node and begin participating.

> As a Core Node operator, you can also delegate TRAC to your own node. This shows economic commitment to the network and can improve your attractiveness to other delegators.
