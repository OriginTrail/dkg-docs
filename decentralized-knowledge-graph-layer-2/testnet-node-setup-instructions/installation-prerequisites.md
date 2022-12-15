# Installation prerequisites

{% hint style="info" %}
Before running a mainnet node, consider first to run a testnet node.
{% endhint %}

Before we dive into the installation process of the DKG node, there are a few important steps that need to be executed such as acquiring tokens needed for the node’s proper functioning on the network as well as mapping your **ERC20** and **Substrate** wallets.

## 1. Node wallets

There are 4 wallets (keys) that your node needs to properly function with OriginTrail V6:

* 1x “Operational” Ethereum wallet (as nodes **evmOperationalWallet**)
* 1x “Operational” Substrate wallet (which will be mapped to **evmOperationalWallet**)
* 1x “Admin” Ethereum wallet (as nodes **evmManagementWallet**)
* 1x “Admin” Substrate wallet that will be mapped to **evmManagementWallet**

These wallets will be used during the installation process and you will add them into the configuration file.

Read more about operational and admin wallets [here](https://docs.origintrail.io/decentralized-knowledge-graph-layer-2/testnet-node-setup-instructions/node-keys).

## 2. Tokens

OriginTrail V6 Mainnet nodes will support multiple blockchains, however, V6 mainnet is launching first on the OriginTrail Parachain. Its operations are fueled by two tokens, TRAC and the native blockchain token - OTP in the case of OriginTrail Parachain, ETH in the case of Ethereum, MATIC for Polygon etc.

In order for your node to successfully start and run, you will need to provide these tokens to its **operational wallet.**

For more information on OriginTrail two-layer utility tokens - both TRAC and OTP, please check the following page: [https://parachain.origintrail.io/whitepaper?section=trac-otp-tokenomics](https://parachain.origintrail.io/whitepaper?section=trac-otp-tokenomics)

#### Layer 2 utility token - TRAC

The Trace token (TRAC) is the utility token of the DKG (layer 2 of OriginTrail). It is required to perform operations such as publishing assets on the network, and is a utility token that drives the entire DKG.

**To run a node in OriginTrail V6, your node requires at least 50.000 TRAC tokens posted as a security collateral to the network.**

#### How can you acquire TRAC?&#x20;

TRAC token can be accessed through multiple (decentralized and centralized) platforms. A non-exhaustive list includes:

* Coinbase&#x20;
* Huobi&#x20;
* Kucoin&#x20;
* Uniswap&#x20;
* Bancor&#x20;
* Wintermute (over-the-counter)

More options can be found on [CoinMarketCap](https://coinmarketcap.com/currencies/origintrail/) or [CoinGecko](https://www.coingecko.com/sl/coins/origintrail#markets) platforms.

{% hint style="danger" %}
**IMPORTANT: There is no association between the core development team and the above mentioned platforms. You should familiarise yourself with all possible risks of using their services as you are doing so under your own responsibility.**
{% endhint %}

#### Layer 1 utility tokens

OriginTrail has over time evolved into a multichain system (supporting Ethereum, Polygon and Gnosis blockchains) and with V6 makes an extension to the OriginTrail Parachain on Polkadot, which is the first blockchain OriginTrail V6 will support.

The OriginTrail Parachain Token (OTP) is the utility token for OriginTrail Parachain and is necessary for OriginTrail V6 nodes to run.

#### How can you acquire OTP tokens?

OTP tokens have been distributed to contributors of the OriginTrail Parachain crowdloan, as well being available in bounty for teleporting TRAC tokens to OriginTrail Parachain.

Follow the announcements in Discord to learn once a converter between TRAC and OTP will be launched on the OriginTrail Parachain, allowing you to exchange between the two tokens.

#### Getting your TRAC tokens on the OriginTrail Parachain (TRAC Teleport)

&#x20;TRAC is an ERC20 token on the Ethereum blockchain, transferred over to the OriginTrail Parachain and enhanced with Polkadot native capabilities. In order to transfer your TRAC tokens to the OriginTrail Parachain, a Teleport system has been established until a Polkadot <-> Ethereum bridge is ready. Therefore to get your TRAC on the OriginTrail Parachain, you need to [teleport your tokens first](https://teleport.origintrail.io/).

Note: Teleporting is performed in 15 batches. Details are available in [OT-RFC-12](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-12%20OriginTrail%20Parachain%20TRAC%20bridges%20\(v2\).pdf).

## **3**. **Mapping your operational and admin wallets**

In order to complete the Teleport and setup your V6 node, you will need to perform a process of “mapping” your Ethereum and Substrate wallets. The mapping process is explained [here](https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/teleport-instructions).

The process will require you to use an “account mapping” interface - an example usage video is available [here](https://www.youtube.com/watch?v=yltbdB1bpEA).

## **4**. **Provision a server for your node**

In order to deploy your OriginTrail V6 node, you will need a Linux server with the following minimum recommended hardware:

* **4GB RAM,**&#x20;
* **2CPUs**&#x20;
* **50GB HDD space**

Make sure that you have root access to your server.

