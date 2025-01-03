---
icon: star
---

# V8 Testnet Scoring Guide

{% hint style="info" %}
The V8 testnet program has completed. The following content is kept for legacy information purposes only.
{% endhint %}

## Testnet incentives

## v8.0.0-beta (Initial focus on Publishing)

In the early stages of the OriginTrail V8 incentivized testnet, publishing **Knowledge Assets (KAs)** was the most heavily rewarded operation. This was because the primary goal at the time was to generate a large volume of KAs to thoroughly test the migration of data to the new **Knowledge Assets V2 (KAv2)** format. As a result, node runners earned **1 point** **for every published KA**, while other operations, such as **Get** and **Query**, were rewarded at much lower rates (e.g., 0.01 or 0.03 points). The high incentivization for publishing ensured that the testnet accumulated enough KAs to provide a meaningful test environment for the upcoming KAv2 migration.

## v8.1.0-beta (Focus on Paranets Synchronization)

With the release of **v8.1.0-beta**, the priorities of the testnet shifted away from publishing at scale. Having surpassed the milestone of **5 million KAs** on the network, there was no longer a need for continued high-volume KA publishing. The reward for publishing KAs was therefore drastically reduced from **1 point to 0.01 points per KA**. Node runners are now encouraged to slow down their publishing efforts. (This might change however in the coming releases)

The main focus of the new release is on testing the newly introduced **Paranet syncing** functionality, which is now much more heavily incentivized. Each synced KA across a Paranet is rewarded with **3 points**, significantly higher than the rewards for other operations. The goal of this shift is to drive collaboration between node runners on syncing KAs across different nodes and forming Paranets, which are essential for testing the network’s decentralized syncing capabilities.

### Best Pracitces for Node Runners in v8.1.0-beta

In the **v8.1.0-beta** environment, node runners should stop prioritizing high-rate publishing of new KAs. Instead, it is now more beneficial to attach existing KAs to Paranets and focus on syncing between nodes. This will not only help in reducing gas costs associated with publishing new KAs but also provide valuable testing data for the network’s syncing and collaboration features.

To make the most of the current incentivization model:

* Collaborate with other node runners to create and maintain Paranets.
* Attach existing KAs to Paranets to trigger sync operations between nodes.

The updated scoring system reflects the current needs of the network, prioritizing syncing and collaboration over sheer volume of data publishing, and node runners are encouraged to adapt accordingly for better participation and rewards.

### Syncing in OriginTrail V8 Paranets: Detailed Overview

In the OriginTrail V8 Incentivized Testnet, syncing KAs across Paranets is a critical function, and it’s important for node runners to understand how this works, especially given the introduction of two distinct types of Paranets: **Open Paranets** and **Curated Paranets**. Here’s a breakdown of how syncing operates within each Paranet type and how to trigger syncs effectively.

#### Types of Paranets

1. **Open Paranets:**
   1. **Open to all nodes:** Any node in the network can join, publish KAs, and sync data across the Paranet.
   2. **Data Distribution:** KAs are distributed across **20 nodes (R2)** based on the normal hashing scheme, using asks and distances on the hash ring to determine which nodes will store the data.
   3. **Sync Triggers:**
      1. The sync will automatically triggered in case it doesn't have the data in the specific Paranets Repository, few examples:
         1. Node was offline during publishing
         2. Node is not a part of the neighborhood where KA was published
         3. Node just joined the network
         4. KA is submitted to the Paranet after the publishing
         5. Node has data in Public Repository, but not in Paranets Repository
      2. How to start syncing: For details on how to sync Open Paranets, refer to[ this guide](../../dkg-v6-previous-version/node-setup-instructions/sync-a-dkg-paranet.md).
2. **Curated Paranets:**
   1. **Access Control:** Curated Paranets provide two levels of control:
      1. Who can publish KAs to the Paranet (curated miners).
      2. Which nodes can join the Paranet to sync and access data (curated nodes). Only whitelisted nodes are allowed.
   2. **Private Data Sharing:** Curated Paranets also allow private data exchange among whitelisted nodes, offering a layer of exclusivity and privacy.
   3. **Sync Triggers:**
      1. The sync will automatically triggered in case it doesn't have the data in the specific Paranets Repository, few examples:
         1. Node is not a Publisher node, which means that Node will sync it from the node where the data was stored
         2. Node was offline during publishing
         3. Node just joined the Paranet
         4. Node has data in Public/Private Repositories, but not in Paranets Repository
         5. _<mark style="color:red;">**KA for Curated Paranets couldn't be submitted to the Paranet as for v8.1.0-beta, it can only be synced if was published using Local Store operation!**</mark>_
      2. Syncing curated paranets: Syncing [follows the same steps](broken-reference) as for Open Paranets, but your node must be whitelisted by the Paranet operator.

#### How to Create Paranets and Manage Curated Access

1. Creating a Paranet:
   1. To create either an Open or Curated Paranet, follow these guides ([dkg.js](../v8-dkg-sdk/dkg-v8-js-client/interact-with-dkg-paranets.md#creating-a-paranet) and [dkg.py](../v8-dkg-sdk/dkg-v8-py-client/interact-with-dkg-paranets.md#creating-a-paranet)), which walk through the setup process for both types.
2. Managing Curated Nodes and Miners:
   1. For Curated Paranets, you need to manage access controls:
      1. Add Curated Nodes: Only these nodes can sync data within the Paranet.
         1. Paranet Operator can add Curated Nodes.
         2. Node runners can Request Access to become a Curated Node, while Paranet Operator might Reject or Accept the Request.
      2. Add Curated Miners: Only these nodes can publish KAs to the Paranet.
         1. Paranet Operator can add Curated Miners.
         2. Miners can Request Access to become a Curated Miner, while Paranet Operator might Reject or Accept the Request.
      3. For step-by-step instructions on adding curated nodes and miners, refer to these combined guides ([dkg.js](../v8-dkg-sdk/dkg-v8-js-client/interact-with-dkg-paranets.md#adding-removing-nodes-to-from-a-curated-paranet) and [dkg.py](../v8-dkg-sdk/dkg-v8-py-client/interact-with-dkg-paranets.md#adding-removing-nodes-to-from-a-paranet)).

#### Key Takeaways

* **Open Paranets** allow unrestricted syncing and publishing of KAs. Sync is triggered if a node is offline, node is not part of the initial KA neighborhood or just copying KA from the public repository to the specific Paranet Repository.
* **Curated Paranets** offer tighter control over who can publish and sync KAs, with sync triggered by local storage events among whitelisted nodes. This creates a more selective and private data-sharing environment.

This syncing mechanism promotes collaboration between nodes and adds flexibility in forming Paranets, allowing for effective decentralized data sharing and testing within the **OriginTrail V8 Incentivized Testnet**.
