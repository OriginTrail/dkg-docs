---
description: >-
  The OriginTrail full node is playing a crucial role on the Decentralized
  Knowledge Graph (DKG) by hosting Knowledge assets.
---

# Running a full node

## How to initiate a full DKG node?

Once the OriginTrail DKG node starts, **several blockchain transactions need to be executed for your node to become an active part of the network and start hosting the DKG Knowledge assets**. These transactions are needed to set the required TRAC stake for your node (50 000 TRAC at this time) and set the node service ask. Both values are set in TRAC tokens.

### **Setting the node stake and service ask parameters**

{% hint style="warning" %}
**50000** **TRAC** is the minimum amount of TRAC for a Full DKG Mainnet for your node to become eligible for DKG hosting and rewards. More information is available in the following OriginTrail [OT-RFC-14](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-14%20DKG%20v6%20TRAC%20Tokenomics.pdf).

If a Full DKG node's TRAC falls below 50,000, reset the operator fee to the desired value before reactivating it.
{% endhint %}

\
You can set the node stake and ask settings in two ways. The first option is to use the Houston application and the second is to do it by running a few npm scripts directly on the server where your nodes is installed.

In order to configure stake and ask parameters on your OriginTrail DKG node, we recommend using [Houston application](houston-origintrail-node-command-center.md).

### Setting up node stake and service ask via Houston (Recommended):

[Houston](houston-origintrail-node-command-center.md) is the OriginTrail node user interface (command center) that allows you to execute certain operations regarding your node on the blockchain. There are two ways to run Houston:

1. Via a hosted application, which is available at the following link: [https://houston.origintrail.io/](https://houston.origintrail.io/) or
2. Run Houston Web application locally by following the setup [instructions](houston-origintrail-node-command-center.md#setup-houston-locally).

More  information on Houston can be found [here](houston-origintrail-node-command-center.md)\
\
**Setting your node service ask**\
Navigate to the "Service tokenomics" page within the Houston application, enter the service ask amount, denominated in TRAC and click "Update ask" button. This will trigger the transaction signing process with Metamask.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-05-29 at 18.44.29.png" alt="" width="320"><figcaption><p>Node service ask setting interface</p></figcaption></figure>

**Staking TRAC to your node**

Navigate to the "Service tokenomics" section within Houston application, enter the stake amount in TRAC and click "Add stake" button. This will again trigger the transaction signing process with Metamask, this time requiring two transactions to complete the process of TRAC staking to your node.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-05-29 at 18.44.49.png" alt="" width="375"><figcaption><p>Node stake settings interface</p></figcaption></figure>
