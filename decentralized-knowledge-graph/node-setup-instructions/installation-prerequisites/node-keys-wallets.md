---
description: >-
  This section will guide you trough the preparation of the node wallets (keys)
  for each of the blockchains currently supported by OriginTrail DKG node.
---

# Node keys (wallets)

## Intro on node keys

Since DKG nodes are connected to one or more blockchains, in order to perform actions on them they need to appropriate keys (wallets). Therefore, for each blockchain you want to support with your node, you will need to setup several keys.&#x20;

More info can be found in [the node keys explained page](../useful-resources/node-keys-explained.md).

{% hint style="info" %}
Since version 6.2.0 DKG nodes support multiple operational wallets.
{% endhint %}

## NeuroWeb (OriginTrail Parachain) wallet preparation:

In order for you to run your OriginTrail DKG node on NeuroWeb blockchain, you will need to prepare and fund multiple wallet addresses as presented below:

* At least one “Operational” Ethereum wallet and "Operational" Substrate wallet (defined in **operationalWallets**)
* An “Admin” Ethereum wallet (mapped to **evmManagementWallet**)
* An “Admin” Substrate wallet (mapped to **evmManagementWallet**)

A node can use multiple operational wallets at once. Utilising multiple is preferrable and provides the node with more throughput for sending and updating commits and proofs, as well as performing other operations in parallel.

TRAC is an ERC20 token on the Ethereum blockchain, transferred over to the NeuroWeb blockchain and enhanced with Polkadot native capabilities. In order to run OriginTrail DKG node on NeuroWeb parachain, TRAC tokens are required to be transfered from Ethereum to NeuroWeb blockchain network.

In order to transfer your TRAC tokens to the NeuroWeb blockchain, a Teleport system has been established until a Polkadot <-> Ethereum bridge is ready. Therefore to get your TRAC on the NeuroWeb blockchain, you need to [teleport your tokens first](https://teleport.origintrail.io/).

Details are available in [OT-RFC-12](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-12%20OriginTrail%20Parachain%20TRAC%20bridges%20\(v2\).pdf).

### **Mapping your operational and admin wallets**

In order to complete the Teleport and setup your V6 node, you will need to perform a process of “mapping” your Ethereum and Substrate wallets. The mapping process is explained [here](https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/teleport-instructions). The process will require you to use an “account mapping” interface - an example usage video is available [here](https://www.youtube.com/watch?v=yltbdB1bpEA).

During the installation process, the installer will ask you to provide it with the above wallet addresses (keys) and will automatically add them into your OriginTrail configuration file.

Read more about operational and admin wallets [here](../useful-resources/node-keys-explained.md).

After you finish the Teleport and mapping process, your keys are ready to be used by the OriginTrail DKG node.

## Gnosis and Chiado wallet preparation:

Note: _Gnosis is EMV based blockchain so it does not require mapping procedures like on the NeuroWeb testnet and mainnet blockchains._

In order for you to run your OriginTrail DKG node on Gnosis or Chiado blockchains, you will need to prepare and fund at least following wallets:

* At least one “Operational” EVM wallet (defined in **operationalWallets**)
* 1x “Admin” EVM wallet (mapped to **evmManagementWallet**)

It's recommended to assign multiple operational wallets to a node in order to increase throughput and reliability of operations.



