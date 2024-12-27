---
description: >-
  Below you will find the guidelines for builders, TRAC delegators, and node
  runners for the V8.0 release and activities expected in the Upgrade Period.
---

# How to upgrade to V8?

<figure><img src="../../.gitbook/assets/DKG V8 update guide book - gitbook cover1 (1).png" alt=""><figcaption></figcaption></figure>

## For builders

**Edge Nodes: If you’re running edge-node services**, you should make sure the DKG Engine (ot-node service) is properly updated, as V6 Edge Nodes will not be compatible with the new features. You should also ensure that you update to the newly released V8.0 DKG clients (dkg.js and dkg.py) in your projects - a sufficient level of backward compatibility is enabled for the V6 clients, however, keep in mind that the new features of V8 are somewhat different (check the previous sections on updated Knowledge Assets).

For the ot-node service update, please follow the instructions in the “For Core Node runners section”

Having that said, individual pre-V8 Knowledge Assets will remain queryable via the GET protocol method.&#x20;

**Paranets**: If you are running a paranet on the DKG mainnet, you should be aware that it will be resynced if you have enabled paranet sync in the node config. The node will perform a re-sync by itself, and all the data will be available when sync is completed.

**Smart contracts**: If you are **querying DKG contracts** on any of the deployed chains, you can expect the productive version of V8 smart contracts to be [available on the official repo](https://github.com/OriginTrail/dkg-evm-module/) after the release.

For any questions, please reach out to the developer community in Discord.

## For TRAC delegators

If you have previously delegated your TRAC on any of the DKG-supported blockchains to Core Nodes, your stake will remain active and will continue to contribute to the network. In order to manage your stake (delegating, withdrawing, and redelegating), **you will have to perform a migration to the new system**. This migration will be facilitated by the new Staking Dashboard, which will enable executing migration transactions directly from your staking wallet. These transactions will burn your current share tokens, and account for your stake in the new V8 smart contracts directly.

There is no rush to migrate - your rewards will continue to accrue even if you don’t migrate. The only thing unavailable before migration is managing your stake.&#x20;

Learn more about the new Delegated staking [here](../delegated-staking-v8/).

### For Core Node runners

Follow [these instructions](../v8-dkg-core-node/upgrading-from-v6-to-v8.md) to update your V6 node to a V8 Core node.





####
