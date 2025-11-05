---
description: >-
  This section will guide you trough the preparation of the node wallets (keys)
  for each of the blockchains currently supported by OriginTrail DKG node.
---

# Node keys (wallets)

## What are node keys and why are they needed?

For a DKG node to be able to properly operate, it will need to execute transactions on the blockchains it is connected to, and for that it uses  node keys (wallets) of H160 type (Ethereum). Nodes have two different types of keys:

* **operational** keys, for which the node requires access to (you will need to generate and upload their private keys to your node)&#x20;
* **admin** keys, for which the node doesn't require access and are used to manage the node on chain configuration

To get you started, you will need at least one operational and one one admin key. More details on keys can be found [here](broken-reference).&#x20;

The details of key setup can vary between particular blockchains, so are presented below separately for clarity.

## NeuroWeb wallet preparation:

Since DKG nodes are connected to one or more blockchains, in order to perform actions on them they need to appropriate keys (wallets). Therefore, for each blockchain you want to support with your node, you will need to setup several keys.&#x20;

More info can be found in [the node keys explained page](broken-reference).

{% hint style="info" %}
Since version 6.2.0 DKG nodes support multiple operational wallets.
{% endhint %}

## NeuroWeb wallet preparation:

In order for you to run your OriginTrail DKG node on NeuroWeb blockchain, you will need to prepare and fund multiple wallet addresses as presented below:

* At least one “Operational” Ethereum wallet and "Operational" Substrate wallet (defined in **operationalWallets**)
* An “Admin” Ethereum wallet (mapped to **evmManagementWallet**)
* An “Admin” Substrate wallet (mapped to **evmManagementWallet**)

A node can use multiple operational wallets at once. Utilising multiple is preferrable and provides the node with more throughput for sending and updating commits and proofs, as well as performing other operations in parallel.

A node can use multiple operational wallets at once. Utilising multiple is preferrable and provides the node with more throughput for sending and updating commits and proofs, as well as performing other operations in parallel.

TRAC is an ERC20 token on the Ethereum blockchain, transferred over to the NeuroWeb blockchain and enhanced with Polkadot native capabilities. In order to run OriginTrail DKG node on NeuroWeb parachain, TRAC tokens are required to be transfered from Ethereum to NeuroWeb blockchain network.

In order to transfer your TRAC tokens to the NeuroWeb blockchain, a Teleport system has been established until a Polkadot <-> Ethereum bridge is ready. Therefore to get your TRAC on the NeuroWeb blockchain, you need to [teleport your tokens first](https://teleport.origintrail.io/).

Details are available in [OT-RFC-12](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-12%20OriginTrail%20Parachain%20TRAC%20bridges%20\(v2\).pdf).

### **Mapping your operational and admin wallets**

In order to complete the Teleport and setup your V6 node, you will need to perform a process of “mapping” your Ethereum and Substrate wallets. The mapping process is explained [here](https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/teleport-instructions). The process will require you to use an “account mapping” interface - an example usage video is available [here](https://www.youtube.com/watch?v=yltbdB1bpEA).

During the installation process, the installer will ask you to provide it with the above wallet addresses (keys) and will automatically add them into your OriginTrail configuration file.

Read more about operational and admin wallets [here](https://docs.origintrail.io/decentralized-knowledge-graph-layer-2/testnet-node-setup-instructions/node-keys).

After you finish the mapping process, your keys are ready to be used by the OriginTrail DKG node.

{% hint style="info" %}
The mapping procedure is part of the EVM implementation on NeuroWeb and is a one time activity.
{% endhint %}

## Gnosis and Chiado wallet preparation:

In order for you to run your OriginTrail DKG node on Gnosis or Chiado blockchains, you will need to prepare and fund at least following wallets:

* At least one “Operational” EVM wallet (defined in **operationalWallets**)
* 1x “Admin” EVM wallet (mapped to **evmManagementWallet**)

It's recommended to assign multiple operational wallets to a node in order to increase throughput and reliability of operations.

Once the wallets have been prepared, proceed to the process of acquiring tokens on the desired network (testnet or mainnet).&#x20;



## Base and Base Sepolia wallet preparation:

In order for you to run your OriginTrail DKG node on Base or Base Sepolia blockchains, you will need to prepare and fund at least following wallets:

* At least one “Operational” EVM wallet (defined in **operationalWallets**)
* 1x “Admin” EVM wallet (mapped to **evmManagementWallet**)

It's recommended to assign multiple operational wallets to a node in order to increase throughput and reliability of operations.

Once the wallets have been prepared, proceed to the process of acquiring tokens on the desired network (testnet or mainnet).&#x20;
