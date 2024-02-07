---
description: >-
  This section will guide you trough the preparation of the node wallets (keys)
  for each of the blockchains currently supported by OriginTrail DKG node.
---

# Node keys (wallets)

## NeuroWeb (OriginTrail Parachain) wallet preparation:

In order for you to run your OriginTrail DKG node on NeuroWeb blockchain, you will need to prepare and fund 4 wallet addresses as presented below:

* 1x “Operational” Ethereum wallet (as nodes **evmOperationalWallet**)
* 1x “Operational” Substrate wallet (which will be mapped to **evmOperationalWallet**)
* 1x “Admin” Ethereum wallet (as nodes **evmManagementWallet**)
* 1x “Admin” Substrate wallet that will be mapped to **evmManagementWallet**

TRAC is an ERC20 token on the Ethereum blockchain, transferred over to the NeuroWeb blockchain and enhanced with Polkadot native capabilities. In order to run OriginTrail DKG node on NeuroWeb parachain, TRAC tokens are required to be transfered from Ethereum to NeuroWeb blockchain network.

In order to transfer your TRAC tokens to the NeuroWeb blockchain, a Teleport system has been established until a Polkadot <-> Ethereum bridge is ready. Therefore to get your TRAC on the OriginTrail Parachain, you need to [teleport your tokens first](https://teleport.origintrail.io/).

Details are available in [OT-RFC-12](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-12%20OriginTrail%20Parachain%20TRAC%20bridges%20\(v2\).pdf).

### **Mapping your operational and admin wallets**

In order to complete the Teleport and setup your V6 node, you will need to perform a process of “mapping” your Ethereum and Substrate wallets. The mapping process is explained [here](https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/teleport-instructions). The process will require you to use an “account mapping” interface - an example usage video is available [here](https://www.youtube.com/watch?v=yltbdB1bpEA).

During the installation process, the installer will ask you to provide it with the above wallet addresses (keys) and will automatically add them into your OriginTrail configuration file.

Read more about operational and admin wallets [here](https://docs.origintrail.io/decentralized-knowledge-graph-layer-2/testnet-node-setup-instructions/node-keys).

After you finish the Teleport and mapping process, your keys are ready to be used by the OriginTrail DKG node.

## Gnosis and Chiado wallet preparation:

Note: _Gnosis is EMV based blockchain so it does not require mapping procedures like on the NeuroWeb testnet and mainnet blockchains._

In order for you to run your OriginTrail DKG node on Gnosis or Chiado blockchains, you will need to prepare and fund 2 wallet addresses (see below):

* 1x “Operational” EMV wallet (as nodes **evmOperationalWallet**)
* 1x “Admin” EVM wallet (as nodes **evmManagementWallet**)\
  \




