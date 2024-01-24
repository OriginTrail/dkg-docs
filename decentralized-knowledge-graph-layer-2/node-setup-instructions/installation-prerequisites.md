# Installation prerequisites

{% hint style="info" %}
Before running a mainnet node, consider running a testnet node first.
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

The OriginTrail DKG nodes operate with a two token system:&#x20;

* the TRAC token which is the native utility token of the DKG used for knowledge publishing, and&#x20;
* the native blockchain token of the chosen chain, used for interacting with DKG smart contracts (e.g NeuroWeb, Gnosis, Ethereum etc and their native tokens)

In order for your node to successfully start and run, you will need to provide these tokens to its **operational wallet.**

For more information on OriginTrail two-layer utility tokens - both TRAC and OTP, please check the following page: [https://parachain.origintrail.io/whitepaper?section=trac-otp-tokenomics](https://parachain.origintrail.io/whitepaper?section=trac-otp-tokenomics)

#### Layer 2 utility token - TRAC

The Trace token (TRAC) is the utility token of the DKG (layer 2 of OriginTrail). It is required to perform operations such as publishing knowledge to the network, and is a utility token that drives the entire DKG. Nodes in the DKG can operate in two ways:&#x20;

* **as non-hosting network gateways**, which enables access to the DKG and communication with other network nodes, without hosting the DKG
* **as hosting nodes,** which apart from being network gateways also host a portion of the DKG knowledge assets, for which they receive TRAC publishing fees as rewards. T**o run a hosting node in OriginTrail DKG, your node requires at least 50.000 TRAC tokens posted as a security collateral to the network**

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

OriginTrail has over time evolved into a multichain system (supporting Ethereum, Polkadot, Polygon and Gnosis blockchains) and for a fully functional hosting node you will require native tokens of the blockchains you intend to run it on as well.

#### In case you want to use NeuroWeb blockchain&#x20;

TRAC is an ERC20 token on the Ethereum blockchain, transferred over to the NeuroWeb blockchain and enhanced with Polkadot native capabilities. In order to transfer your TRAC tokens to the NeuroWeb blockchain, a Teleport system has been established until a Polkadot <-> Ethereum bridge is ready. Therefore to get your TRAC on the OriginTrail Parachain, you need to [teleport your tokens first](https://teleport.origintrail.io/).

Details are available in [OT-RFC-12](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-12%20OriginTrail%20Parachain%20TRAC%20bridges%20\(v2\).pdf).

## **3**. **Mapping your operational and admin wallets**

In order to complete the Teleport and setup your V6 node, you will need to perform a process of “mapping” your Ethereum and Substrate wallets. The mapping process is explained [here](https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/teleport-instructions).

The process will require you to use an “account mapping” interface - an example usage video is available [here](https://www.youtube.com/watch?v=yltbdB1bpEA).

## **4**. **Provision a server for your node**

In order to deploy your OriginTrail V6 node, you will need a Linux server with the following minimum recommended hardware:

{% hint style="warning" %}
The provided installer script is designed for installing the OriginTrail node on **Ubuntu 20.04 LTS and 22.04 LTS** distributions.\
\
It is also possible to install the OriginTrail node on other systems but it would require  modifications to the installer script. If you have any such modifications in mind, we highly encourage your contributions so please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

* **4GB RAM,**&#x20;
* **2CPUs**&#x20;
* **50GB HDD space**

Make sure that you have root access to your server.

