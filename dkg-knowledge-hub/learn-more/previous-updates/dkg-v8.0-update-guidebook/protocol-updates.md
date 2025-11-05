---
description: What's new on the infrastructure updates
---

# Protocol updates

<figure><img src="../../../../.gitbook/assets/DKG V8 update guide book - gitbook cover1 (1).png" alt=""><figcaption></figcaption></figure>

The following description of updates should be considered a summary. **It assumes some knowledge of how the DKG V6 system worked.** The details of each feature will be further explained in the dedicated documentation pages.

## Scalability updates

The major improvement V8 brings is orders of magnitude higher throughput. Improving from V6, which peaked at 100k Knowledge Assets per day, we expect OriginTrail V8 to be able to reach up to 1000x that number, enabling Internet-scale neuro-symbolic AI.

The two major features enabling scalability are:

* **Batch minting of Knowledge Assets**, which enables minting hundreds of Knowledge Assets in one transaction (compared to previously minting just a single Knowledge Asset), as well as easier creation of whole collections of Knowledge Assets. Together with the new Edge Node’s Knowledge Mining API, it will now be very easy to create hundreds of Knowledge Assets from various data inputs such as PDFs, CSVs, JSON, and many others. The capability comes together with an updated version of Knowledge Assets, explained further below.
* **Random sampling proof system**, which makes the protocol much less gas intensive through an optimized proof system and lower complexity of implementation. This means the:
  * **V6 service agreements** are being replaced by a random sampling algorithm. This algorithm periodically proves randomized elements of the DKG by Core Nodes, significantly lowering the protocol blockchain footprint. **This will unlock significant capacity on all the blockchains connected to the DKG, significantly lowering protocol-required node transactions.**&#x20;
  * **Neighborhoods are superseded by sectors**: In V6, nodes have been organized in a p2p hash ring with fluid ranges called “neighborhoods”. A neighborhood was formed of 20 nodes closest in the hash ring (in terms of hash distance) to the Merkle root hash of the currently published Knowledge Asset. In V8, nodes are no longer grouped in neighborhoods, but rather in fixed “sectors”. A **sector** is implemented as a fixed set of Core Nodes (with hash distance no longer being relevant), and all the nodes active in V6 (with over 50k TRAC stake) will be automatically transferred to the initial V8 sector. Sectors will scale over time by fractal division (once a sector grows too big, it will be split in half). All nodes in a sector host the entire sector of the DKG. It is expected that the initial V8 sector will be the only sector and will not split for some time (several months or even years), and once more sectors are available on the network, it will be possible to have Core Nodes join multiple sectors.&#x20;
  * **Epochs**: Knowledge Asset lifetime and publishing fees will now follow synchronized epochs, rather than each Knowledge Asset service agreement having its own “timeline of epochs”. This makes the system simpler to track, implement, and understand. Together with this update, epochs in V8 will also be shortened from 3 months to 1 month.
  * **Efficient reward collection**: Nodes will collect rewards more gas-efficiently, as they will be able to collect fees for multiple proofs at once, saving on gas costs. Node runners will be able to configure the frequency of reward collection for their node

## New version of Knowledge Assets

<figure><img src="../../../../.gitbook/assets/Scalability updates.png" alt=""><figcaption></figcaption></figure>

DKG V6 introduced Knowledge Assets for the first time - a revolutionary AI primitive initially implemented as 'containers of knowledge'. More specifically, a Knowledge Asset in DKG V6 is implemented as a binding between a triple store [named graph](https://en.wikipedia.org/wiki/Named_graph), containing as many triples as one wants, and an on-chain ERC721 NFT containing the Knowledge Asset Merkle root. The Knowledge Asset is addressed by the use of a special kind of ownable URI - a **Universal Asset Locator**, or UAL, which is provably globally unique, is a qualified Decentralized Identifier (DID), and is transferrable (via ERC721).&#x20;

Knowledge Assets have been deployed productively in [various contexts](https://origintrail.io/solutions/overview) and have yielded two key feedback points from builders:

1. For most of the builders, it was more intuitive to think in terms of having **one Knowledge Asset correspond to one real-world entity** (building, train, wheel, song, etc.). Having the ability to put multiple entities in a “container of knowledge” (Knowledge Asset in V6) was often not used because of this intuition, and likely as it requires a deeper understanding of the underlying implementation, such as the concept of named graphs.
2. More importantly, from a semantic perspective, **pointing to a UAL of a named graph is much less practical than referring to a UAL of an actual knowledge graph (KG) entity** when building a knowledge graph or a paranet.&#x20;

Combining those two learnings with the scalability improvements, the DKG V8 brings an updated version of Knowledge Assets, which are now knowledge graph entities. Named graphs are now used to implement “Knowledge Collections” (equivalent to NFT collections) that can still be referenced by a UAL. Each resource in the graph becomes a Knowledge Asset, represented by an ERC1155Delta standard token on-chain. This satisfies both feedback points 1 and 2, making Knowledge Assets more intuitive, semantically useful, and easier to operate with.&#x20;

Given the scalability updates and the new paradigm introduced with Knowledge Assets in V8, it is expected that the cost of publishing per Knowledge Asset will go down significantly.&#x20;

## V8 staking updates

<figure><img src="../../../../.gitbook/assets/Staking updates.png" alt=""><figcaption></figcaption></figure>

The V8 staking system will also be improved in many ways. Specifically in terms of visibility and transparency of the system on-chain, as well as user experience and interface improvements.

The V8 staking system is inspired by Uniswap V3 implementation, just as the V6 system was inspired by Uniswap V2 by adopting the concept of “**node share tokens**”. In V6, node share tokens are ERC20 tokens that represent the “share” of one’s delegated TRAC stake in a node. Share tokens are minted when TRAC is delegated to a node and burned when one withdraws it.&#x20;

In V8, the share tokens are going away, being replaced by a more optimal system. **However, this will require all V6 delegators to migrate their staking tokens**. The updated Staking Dashboard will facilitate this migration. The migration will require delegators to submit several transactions that will burn their share tokens and account for the stake in the new V8 smart contracts. The V8 staking mechanism remains fully non-custodial.

**IMPORTANT**: Note that **this** **migration can be done at any time.** If you are a stake delegator in V6, your TRAC stake will still be accruing rewards and be accounted for in the contracts after the V8 update. The migration is only required for delegators to be able to interact with the new V8 system (to delegate TRAC, withdraw rewards, etc.).

The new Staking Dashboard will also provide new statistics and ways to measure your TRAC stake performance, according to the updated tokenomics described in [OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf), and will be upgraded, specifically during the Tuning period.

## Core and Edge Nodes as neuro-symbolic AI systems

<figure><img src="../../../../.gitbook/assets/Core and Edge Nodes as Neuro-symbolic AI systems.png" alt=""><figcaption></figcaption></figure>

The DKG V8 introduces a **new concept of a DKG Edge Node**, designed to run the DKG on edge devices such as laptops, phones, and others. DKG Core Nodes, on the other hand, are designed to host the DKG and form a secure network backbone. The new **Edge Node services include neuro-symbolic services such as:**

* Knowledge Mining API, which facilitates Knowledge Asset graph creation pipelines
* DRAG API, which provides a framework to perform Decentralized Retrieval Augmented Generation (DRAG) on the DKG,&#x20;
* Multi-modal LLM interfaces,&#x20;
* A customizable UI,&#x20;
* A publishing service, and more. &#x20;

**Edge and Core Nodes share most of their code and services**, and as a builder, you can extend and combine them in different ways, including creating your custom services either for your node or paranet. The key differences between Core and Edge Nodes are in their mode of operation:

**DKG Edge Node:**&#x20;

* It is designed for privacy-preserving applications, where private Knowledge Assets, the use of local LLMs, and knowledge pipelines enable the utmost privacy-preserving environment.
* Is not intended to host the public DKG and, therefore, does not require a TRAC stake collateral. The Edge Node is, therefore, also not capable of collecting publishing fees and network rewards.
* Does not require high uptime, as does the DKG Core Node.
* Can be used as a substrate to quickly create neuro-symbolic AI applications based on the DKG paranets.
* Can be “converted” into a Core Node, assuming the right conditions (interesting for builders of paranets who would like to recuperate some of the publishing fees by running a Core Node).

**DKG Core Node:**

* It is designed to host the public DKG and provide high availability, so is incentivized to provide high uptime.
* Requires a minimum of 50,000 TRAC token stake to be eligible for joining the network, however, with a higher stake Core Nodes increase their reward chances.
* Can be used as a “gateway node” for publishing, and with a higher publishing rate, the chances of network rewards grow.
* Performs the network services for a fee, determined globally by the pricing mechanism from all the individual Core Node asks. However, nodes with lower asks (less “greedy” nodes) have a higher chance of receiving network rewards.

More details on the system are provided in the [OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf).

For more information on the DKG Edge Node [visit this page](../../../../graveyard/everything/dkg-edge-node/), or see [this talk at DKGCon2024](https://youtu.be/9WeVMHH3gg4?t=5831).

## Protocol pricing updates

With the protocol tokenomics upgrade, the DKG publishing fee system is also being optimized. With learnings from V6 and removing neighborhood pricing complexities, the new system of “sectors” relies on a simpler and more robust implementation of pricing on the network. The new implementation is **expected to solve the reward “cliff effect”** (where only nodes with close to the maximum stake were receiving rewards), as well as solve some recurring problems with obtaining the right market price.

\
To determine the price of network service in V8 in a specific sector (V8.0 starts with only 1 sector), a sector-wide DKG publishing fee is computed based on individual node asks. To achieve a price equilibrium, the V8 pricing system utilizes the statistics-based sigma approach, determining the **publishing fee as a stake-weighted average ask of all Core Node asks within 1 standard deviation from the current price equilibrium**. That is a mouthful :), so here’s the formula:

$$
\text{serviceFee} = \frac{\sum \left( \text{nodeStake}_i \times \text{nodeAsk}_i \right)}{\sum \left( \text{nodeStake}_i \right)}
$$

for all nodes which satisfy the

$$
\text{serviceFee} - \sigma \leq \text{nodeAsk} \leq \text{serviceFee} + \sigma
$$

where $$\sigma$$ is the standard deviation across the population of all node asks. If a Core Node ask is outside of the bounds, it will, therefore, not influence the DKG service fee.

This means the fee will also be available on-chain and can be easily read, eliminating the previously encountered “bid suggestion” issues that would occur in V6.

{% hint style="info" %}
You can manage your Core Node ask in the new [Staking Dashboard](https://staking.origintrail.io).
{% endhint %}

As a key implementation component requiring real economic conditions for proper testing, the pricing system will be improved during the **Tuning period**.

### Upgraded tokenomics

The [OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf) has laid out the V8 updated tokenomics with additional factors incentivizing positive behavior on the network. It sets **4 key factors for Core Node performance:**&#x20;

* The amount of TRAC stake,&#x20;
* The amount of publishing performed through the node,&#x20;
* The node ask, and&#x20;
* Total uptime.&#x20;

We encourage exploring the RFC further until the detailed documentation for the implementation is published.
