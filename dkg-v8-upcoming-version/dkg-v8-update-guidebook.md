---
icon: rocket-launch
cover: ../.gitbook/assets/DKG V8 update guide book - gitbook cover.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
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

# DKG V8 update guidebook

V8 is a major update that increases scalability up to 1000x, introduces DKG Edge Nodes to power privacy-preserving AI use, improves Knowledge Assets, and much more.&#x20;

This guide will introduce you to the DKG V8 update, what you can expect from the new features, the launch timeline, and most importantly, what you need to do if you are a builder, staker, or node operator.&#x20;

Check [this page](https://docs.origintrail.io/dkg-v8-upcoming-version/whats-new-with-origintrail-v8) to get acquainted with the most important new updates of the DKG V8. In this document, we will focus on the implementation details of the protocol.

## The DKG V8 protocol updates

The following description of updates should be considered a summary, and **it assumes some knowledge of how the DKG V6 system works.** The details of each of the features will be further explained in the dedicated documentation pages.

### Scalability updates

The major improvement V8 brings is orders of magnitude higher throughput. Improving from V6, which peaked at 100k Knowledge Assets per day, we expect OriginTrail V8 to be able to reach up to 1000x that number, enabling Internet-scale neuro-symbolic AI.

The two major features enabling scalability are:

* **Batch minting of Knowledge Assets**, which enables minting hundreds of Knowledge Assets in 1 transaction (compared to previously minting just a single Knowledge Asset), as well as easier creation of whole collections of Knowledge Assets. Together with the new Edge Node’s Knowledge Mining API, it will now be very easy to create hundreds of Knowledge Assets from various data inputs such as PDFs, CSVs, JSON, and many others. The capability comes together with an updated version of Knowledge Assets, explained further below.
* **Random sampling proof system**, which makes the protocol much less gas intensive through an optimized proof system and lower complexity of implementation. This means the:
  * **V6 service agreements** are being replaced by a random sampling algorithm, which periodically proves randomized elements of the DKG by Core Nodes, which significantly lowers the protocol blockchain footprint. **This will unlock significant capacity on all the blockchains connected to the DKG, significantly lowering protocol required node transactions.**&#x20;
  * **Neighborhoods are superseded by sectors**: In V6 nodes have been organized in a p2p hash ring with fluid ranges called “neighborhoods”. A neighborhood was formed of 20 nodes closest in the hash ring (in terms of hash distance) to the Merkle root hash of the currently published Knowledge Asset. In V8, nodes are no longer grouped in neighborhoods, but rather in fixed “sectors”. A **sector** is implemented as a fixed set of Core Nodes (with hash distance no longer being relevant), and all the nodes active in V6 (with over 50k TRAC stake) will be automatically transferred to the initial V8 sector. Sectors will scale over time by fractal division (once a sector grows too big, it will be split in half). All nodes in a sector host the entire sector of the DKG. It is expected that the initial V8 sector will be the only sector and will not split for some time (several months, or even years), and once more sectors are available on the network, it will be possible to have Core Nodes join multiple sectors.&#x20;
  * **Epochs**: Knowledge Asset lifetime and publishing fees will now follow synchronized epochs, rather than each Knowledge Asset Service Agreement having its own “timeline of epochs”. This makes the system simpler to track, implement, and understand. Together with this update, epochs in V8 will also be shortened from 3 months to 1 month.
  * **Efficient reward collection**: Nodes will collect rewards more gas-efficiently, as they will be able to collect fees for multiple proofs at once, saving on gas costs. Node runners will be able to configure the frequency of reward collection for their node

### New version of Knowledge Assets

<figure><img src="../.gitbook/assets/Scalability updates.png" alt=""><figcaption></figcaption></figure>

DKG V6 introduced Knowledge Assets for the first time - a revolutionary AI primitive initially implemented as 'containers of knowledge'. More specifically, a Knowledge Asset in DKG V6 is implemented as a binding between a triple store [named graph](https://en.wikipedia.org/wiki/Named_graph), containing as many triples as one wants, and an on-chain ERC721 NFT containing the Knowledge Asset Merkle root. The Knowledge Asset is addressed by the use of a special kind of ownable URI - a **Universal Asset Locator**, or UAL, which is provably globally unique, is a qualified Decentralized Identifier (DID), and is transferrable (via ERC721).&#x20;

Knowledge Assets have been deployed productively in [various contexts](https://origintrail.io/solutions/overview), and have yielded two key feedback points from builders:

1. For most of the builders, it was more intuitive to think in terms of having **one Knowledge Asset correspond to one real-world entity** (building, train, wheel, song, etc.). Having the ability to put multiple entities in a “container of knowledge” (Knowledge Asset in V6) was often not used because of this intuition, and likely as it requires a deeper understanding of the underlying implementation, such as the concept of named graphs.
2. More importantly, from a semantic perspective, **pointing to a UAL of a named graph is much less practical than referring to a UAL of an actual knowledge graph (KG) entity** when building a knowledge graph or a paranet.&#x20;

Combining those two learnings with the scalability improvements, the DKG V8 brings an updated version of Knowledge Assets, which are now knowledge graph entities. Named graphs are now used to implement “Knowledge Collections” (equivalent to NFT collections) that can still be referenced by a UAL, and each resource in the graph becomes a Knowledge Asset, represented by an ERC1155Delta standard token on-chain. This satisfies both feedback points 1 and 2, making Knowledge Assets more intuitive, semantically useful, and easier to operate with.&#x20;

Given the scalability updates and the new paradigm introduced with Knowledge Assets in V8, it is expected that the cost of publishing per Knowledge Asset will go down significantly.&#x20;

### &#x20;V8 Staking updates

<figure><img src="../.gitbook/assets/Staking updates.png" alt=""><figcaption></figcaption></figure>

The V8 staking system will also be improved in many ways, more specifically in terms of visibility and transparency of the system on-chain, as well as user experience and interface improvements.

The V8 staking system is inspired by Uniswap V3 implementation, just as the V6 system was inspired by Uniswap V2 by adopting the concept of “**node share tokens**”. In V6, node share tokens are ERC20 tokens that represent the “share” of one’s delegated TRAC stake in a node - they are minted when TRAC is delegated to a node and burned when one withdraws it.&#x20;

In V8, the share tokens are going away, being replaced by a more optimal system. **This will however require a migration of staking tokens by all V6 delegators**. The updated Staking Dashboard will facilitate this migration, which will require delegators to submit several transactions that will burn their share tokens and account for the stake in the new V8 smart contracts. The V8 staking mechanism remains fully non-custodial.

**IMPORTANT**: Note that **this** **migration can be done at any time** - if you are a stake delegator in V6, your TRAC stake will still be accruing rewards and accounted for in the contracts after the V8 update. The migration is only required for delegators to be able to interact with the new V8 system (to delegate TRAC, withdraw rewards, etc.).

The new Staking Dashboard will also provide new statistics and ways to measure your TRAC stake performance, according to the updated tokenomics described in [OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf), and will be upgraded, specifically during the Tuning period.

### Core and Edge Nodes as neuro-symbolic AI systems

<figure><img src="../.gitbook/assets/Core and Edge Nodes as Neuro-symbolic AI systems.png" alt=""><figcaption></figcaption></figure>

The DKG V8 introduces a new concept of a DKG Edge Node, designed to run the DKG on edge devices such as laptops, phones, and others. DKG Core Nodes on the other hand are designed to host the DKG and form a secure network backbone. The new Edge Node services include neuro-symbolic services such as the Knowledge Mining API which facilitates Knowledge Asset graph creation pipelines, the DRAG API which provides a framework to perform Decentralized Retrieval Augmented Generation (DRAG) on the DKG, multi-modal LLM interfaces, a customizable UI, a publishing service and more. &#x20;

Edge and Core Nodes share most of their code and services, and as a builder, you can extend and combine them in different ways, including creating your custom services either for your node, or paranet. The key differences between Core and Edge Nodes are in their mode of operation:

DKG Edge Node:&#x20;

* It is designed for privacy-preserving applications, where private Knowledge Assets, the use of local LLMs, and knowledge pipelines enable the utmost privacy-preserving environment.
* Is not intended to host the public DKG and, therefore, does not require a TRAC stake collateral. The Edge Node is therefore also not capable of collecting publishing fees & network rewards.
* Does not require a high uptime as the DKG Core Node does.
* Can be used as a substrate to quickly create neuro-symbolic AI applications based on the DKG paranets.
* Can be “converted” into a Core Node (interesting for builders of Paranets who would like to recuperate some of the publishing fees by running a Core Node), assuming the right conditions

DKG Core Node:

* It is designed to host the public DKG and provide high availability, so is incentivized to provide high uptime.
* Requires a minimum of 50,000 TRAC token stake to be eligible for joining the network, however, with a higher stake Core Nodes increase their reward chances.
* Can be used as a “gateway node” for publishing, and with a higher publishing rate, the chances of network rewards grow.
* Performs the network services for a fee, determined globally by the pricing mechanism from all the individual Core Node asks. However, nodes with lower asks (less “greedy” nodes) have a higher chance of receiving network rewards.

More details on the system are provided in the [OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf).

For more information on the DKG Edge Node [visit this page](https://docs.origintrail.io/dkg-v8-upcoming-version/v8-dkg-edge-node), or see [this talk at DKGCon2024](https://youtu.be/9WeVMHH3gg4?t=5831).

### Protocol pricing updates

With the protocol tokenomics upgrade, the DKG publishing fee system is also being optimized. With learnings from V6 and removing neighborhood pricing complexities, the new system of “sectors” relies on a simpler and more robust implementation of pricing on the network. The new implementation is **expected to solve the reward “cliff effect”** (where only nodes with close to the maximum stake were receiving rewards), as well as solve some recurring problems with obtaining the right market price.

\
To determine the price of network service in V8 in a specific sector (V8.0 is starting with 1 sector), a sector-wide DKG publishing fee is computed based on individual node asks. To achieve a price equilibrium, the V8 pricing system utilizes the statistics-based sigma approach, determining the **publishing fee as a stake-weighted average ask of all Core Node asks within 1 standard deviation from the current price equilibrium**. That is a mouthful :), so here’s the formula:

$$
\text{serviceFee} = \frac{\sum \left( \text{nodeStake}_i \times \text{nodeAsk}_i \right)}{\sum \left( \text{nodeStake}_i \right)}
$$

for all nodes which satisfy the

$$
\text{serviceFee} - \sigma \leq \text{nodeAsk} \leq \text{serviceFee} + \sigma
$$

where $$\sigma$$ is the standard deviation across the population of all node asks. If a Core Node ask is outside of the bounds, it will therefore not influence the DKG service fee.

That means the fee will also be available on-chain and can be easily read, which will eliminate the previously encountered “bid suggestion” issues that would occur in V6.

As a key implementation component, requiring real economic conditions for proper testing, the pricing system will be improved during the **Tuning period**.

### Upgraded tokenomics

The [OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf) has laid out the V8 updated tokenomics with additional factors incentivizing positive behavior on the network. It sets 4 key factors for Core Node performance: the amount of TRAC stake, the amount of publishing performed through the node, the node ask, and total uptime. We encourage exploring the RFC further until the detailed documentation for the implementation is published.

## V8 update mechanics - What you need to know

## Release timeline

The V8 deployment is a major update executed as a direct upgrade on the existing OriginTrail V6 network. The update process will therefore require several migrations to be executed. To successfully complete all the necessary activities, the V8 launch will be executed through an “**Upgrade Period**”, which will last for approximately 1 week. During the upgrade period, all relevant DKG components will be updated (nodes, blockchain contracts, Staking Dashboard, DKG Explorer, and others). The update will be executed on all three connected blockchains - Neuroweb, Gnosis, and Base.&#x20;

<figure><img src="../.gitbook/assets/V8 Timeline.png" alt=""><figcaption><p>V8 timeline illustration</p></figcaption></figure>

The beginning of the Upgrade Period, marking the start of the V8 deployment, is scheduled for **Thursday, December 19th, 2024**, and the Upgrade Period is expected to end on **Thursday, December 26th, 2024**.

#### V8.0 - Launch and Tuning Period

Following the launch of DKG V8.0, which will introduce fundamental updates and batch-minting features, the network will enter the **Tuning Period.** During this period more features and parameter tuning updates are expected on all blockchains of the network.&#x20;

During the Tuning Period, DKG Core Nodes will be accruing rewards, which will be claimable after the expiry of the first epoch in V8, which is expected to be at the end of January (with the shortened epoch).&#x20;

The pending publishing rewards from the V6 period will also be made available through the new proof system through the upgrade, with the V6 tokenomics factor of TRAC stake being the only reward factor (as the distance factor is being deprecated), and available only to nodes online prior to V8 launch. The new Random Sampling System will also tackle the problem of under-submission of proofs by V6 nodes, making the reward collection process more efficient. Due to the migration to the new system of synchronized epochs, the V6 reward pool will be distributed across 1 year.

#### V8.1 - Random sampling proof system goes online

The Tuning Period ends with **V8.1**, which will fully introduce the **Random Sampling** features and complete the scalability updates. From this moment on the Core Nodes will start collecting rewards, and the system will be further tuned for different blockchains. More details on the Random Sampling features will be published in the documentation in due time.

### V8 upgrade guidelines

Below you will find the **guidelines for builders, TRAC delegators, and node runners** for the V8.0 release and activities expected in the Upgrade Period.

### For builders

**Edge Nodes: If you’re running edge-node services**, you should make sure the DKG Engine (ot-node service) is properly updated, as V6 Edge Nodes will not be compatible with the new features. You should also ensure that you update to the newly released V8.0 DKG clients (dkg.js and dkg.py) in your projects - a sufficient level of backward compatibility is enabled for the V6 clients, however, keep in mind that the new features of V8 are somewhat different (check the previous sections on updated Knowledge Assets).

For the ot-node service update, please follow the instructions in the “For Core Node runners section”

Having that said, individual pre-V8 Knowledge Assets will remain queryable via the GET protocol method.&#x20;

**Paranets**: If you are running a paranet on the DKG mainnet, you should be aware that it will be resynced if you have enabled paranet sync in the node config. The node will perform a re-sync by itself, and all the data will be available when sync is completed.

**Smart contracts**: If you are **querying DKG contracts** on any of the deployed chains, you can expect the productive version of V8 smart contracts to be [available on the official repo](https://github.com/OriginTrail/dkg-evm-module/) after the release.

For any questions, please reach out to the developer community in Discord.

### For TRAC delegators

If you have previously delegated your TRAC on any of the DKG-supported blockchains to Core Nodes, your stake will remain active and will continue to contribute to the network. In order to manage your stake (delegating, withdrawing, and redelegating), **you will have to perform a migration to the new system**. This migration will be facilitated by the new Staking Dashboard, which will enable executing migration transactions directly from your staking wallet. These transactions will burn your current share tokens, and account for your stake in the new V8 smart contracts directly.

There is no rush to migrate - your rewards will continue to accrue even if you don’t migrate. The only thing unavailable before migration is managing your stake.&#x20;

### For Core Node runners

A few manual steps must be performed to successfully update your V6 node to a V8 Core Node. The following steps should be performed after the official V8 release has been deployed on the DKG mainnet.

#### Preparing your node for V8 update:

Have your node automatically download the latest version, and verify that the auto-updater is enabled on the ot-node service. To enable the auto-updater, follow the instructions on the following [page](https://docs.origintrail.io/dkg-v6-current-version/node-setup-instructions/useful-resources/manually-configuring-your-node).&#x20;

Once the auto-updater is enabled in the .origintrail\_noderc file, restart the node to apply the configuration changes. When the update is released, your node will automatically pull the latest version (V8), install node modules, and restart.

#### Configuring the new V8 blockchainEvents module:

The new V8 ot-node engine introduces a <mark style="color:green;">blockchainEvents</mark> module, which you will need to configure on your node by adjusting the settings in the configuration file. The provided template includes configurations for three blockchains: <mark style="color:green;">otp:2043, gnosis:100</mark>, and <mark style="color:green;">base:8453</mark>. Depending on which blockchains your node is connected to, you should modify the template accordingly.

* **Adjust the&#x20;**<mark style="color:green;">**blockchains**</mark>**&#x20;array**: Only include the blockchain IDs relevant to your node. For example, if your node is not connected to the <mark style="color:green;">gnosis:100</mark> blockchain, remove it from the array.
* **Update the&#x20;**<mark style="color:green;">**rpcEndpoints**</mark>**&#x20;section**: Provide the appropriate RPC endpoints for each blockchain your node is connected to. Remove any endpoints that do not apply to your node’s blockchain configuration.
* **Modify the&#x20;**<mark style="color:green;">**hubContractAddress**</mark>**&#x20;section**: Provide the correct hub contract addresses for the blockchains your node supports, and remove the addresses for blockchains that are not in use.

Template blockchainEvents module:

```
 "blockchainEvents": {
                "enabled": true,
                "implementation": {
                    "ot-ethers": {
                        "enabled": true,
                        "package": "./blockchain-events/implementation/ot-ethers/ot-ethers.js",
                        "config": {
                            "blockchains": ["otp:2043", "gnosis:100", "base:8453"],
                            "rpcEndpoints": {
                                "base:8453": ["<your rpc"],
                                "otp:2043": [
                                    "https://lofar-testnet.origin-trail.network",
                                    "https://lofar-testnet.origintrail.network"
                                ],
                                "gnosis:100": ["<your rpc>"]
                            },
                            "hubContractAddress": {
                                "base:8453": "<new_base_hub_address>",
                                "otp:2043": "<new_neuroweb_hub_address>",
                                "gnosis:100": "<new_gnosis_hub_address>"
                            }
                        }
                    }
                }
            }


```

The new hub addresses will be available at launch.

#### Running data migration:

After the node successfully starts with version 8, you **should manually run the data migration script** run-data-migration.sh, located in the "**/ot-node/current/v8-data-migration/**" directory, by executing "**bash run-data-migration.sh**".

The data migration script migrates all triples from their V6 to V8 triple store repositories. Make sure you have configured RPCs properly for all the blockchains your node is connected to. Depending on how much data your node is hosting, this migration might last several hours to several days. **Note**: This migration will not influence your node reward performance. Your node will remain fully operational, and all pre-V8 Knowledge Assets will remain queryable via the GET protocol method.

If the data migration is interrupted for any reason (e.g., server restart), simply re-run the script. It will automatically resume from the point where it was interrupted.

#### Tracking data migration progress:

To track the data migration progress, check the migration script log file located at                               **"/ot-node/current/v8-data-migration/logs/migration.log**", for example by using the command "**tail -f migration.log**".

We strongly encourage all node runners to update as soon as the release is out to ensure continued compatibility and to take advantage of the latest features and improvements.

## Further information

If you have any questions, please join the [Discord #v8-discussion](https://discord.gg/9WwMRhP9) channel and post them there. Prior to the V8 launch, there will also be a dedicated live discussion (most likely on X spaces) where you can ask all questions about the V8 upgrade.

Trace On!\
