---
description: >-
  This page will help you prepare all the requirements for the V8 DKG Core Node
  installation process.
---

# Preparation for V8 DKG Core Node deployment

Before initiating an installer, each node runner should fulfill a few important requirements to successfully initialize the V8 DKG node.&#x20;

## 1. Hardware requirements:

In order to deploy your V8 DKG node, you will need a Linux server with the minimum recommended hardware as presented below:

* **4GB RAM**
* **2 CPUs**&#x20;
* **50GB HDD space**

{% hint style="success" %}
The initial node setup requires a minimum of 4GB RAM and 2 CPU cores. However, as the node operates for a longer period and accumulates more data, a hardware upgrade may be necessary to maintain optimal performance.
{% endhint %}

Make sure that you have root access to your server.

{% hint style="info" %}
The installer script provided in these instructions is designed to install the OriginTrail node on **Ubuntu 20.04 LTS , 22.04 LTS and 24.04 LTS** distributions.\
\
It is also possible to install the OriginTrail V8 Core Node on other systems, but it would require modifications to the installer script. If you have any such modifications in mind, we highly encourage your contributions. Please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

{% hint style="warning" %}
During the V8 DKG Core Node installation process, the interactive installer will prompt you to input all the required information outlined below. Please make sure that you have all the required inputs prepared before running the installer.
{% endhint %}

## 2. Core Node keys (wallets):

DKG Core Nodes periodically execute blockchain transactions, for which they need node keys (wallets) of the H160 type (Ethereum). There are two categories of keys associated with DKG nodes:

* **Operational keys,** which are used directly by the node to make blockchain transactions. The nodes require their private keys to be accessible (stored in the node configuration file) so that the node can sign transactions
* **Admin keys**, which are used by the node operator, and not by the node itself. Admin keys are intended for administrative transactions to be done by the node operator (such as rotating keys), meaning the nodes don't need access to their private keys (doesn't need to be stored on the node server or configuration file). An admin key can be stored with a hardware wallet, a multisig, or any other Ethereum-compatible wallet of your preference.

To get a DKG node running, you will need **at least one operational key and one admin key**.&#x20;

The OriginTrail DKG nodes operate with a two-token system:&#x20;

* **TRAC token:** The native utility token of the DKG used for knowledge publishing.
* **Native blockchain token of the chosen chain:** Used for interacting with DKG smart contracts.&#x20;

## 3. Funding your keys:

### Acquire Base Sepolia ETH:

The list of Base Sepolia faucets can be found in the official Base [documentation](https://docs.base.org/docs/tools/network-faucets/).

### Acquire Gnosis Chiado xDai:

The list of Gnosis Chiado faucets can be found in the official Gnosis [documentation](https://docs.gnosischain.com/tools/Faucets).

### Acquire NEURO and Base Sepolia, Gnosis Chiado, or NeuroWeb TRAC:

To acquire TRAC on the Base Sepolia, Gnosis Chiado, or NeuroWeb network, you should use the Faucet Bot provided by the OriginTrail core team in the [#faucet-bot Discord channel](https://discord.gg/WaeSb5Mxj6).&#x20;

The Faucet Bot also provides testnet NEURO tokens.

{% hint style="info" %}
**Instructions for the Faucet Bot**

You can find **full instructions** on **how to use the Faucet Bot** [**here**](../../../../dkg-knowledge-hub/useful-resources/test-token-faucet.md).

If you have any problems with the Faucet Bot, you can contact any team member on Discord for assistance or send an email to [tech@origin-trail.com](mailto:tech@origin-trail.com).
{% endhint %}

## 4. Acquire RPC endpoints:

There are many RPC providers that host and provide Base and Gnosis endpoints. It's up to the node runner to choose the best possible option for their nodes.

We recommend checking [Gnosis](https://docs.gnosischain.com/tools/RPC%20Providers/) and [Base](https://docs.base.org/docs/tools/node-providers/#coinbase-developer-platform-cdp) official documentation&#x20;

{% hint style="success" %}
Neuroweb RPCs are provided automatically during the node installation process.
{% endhint %}

## 5. Configure firewall on the server:

OriginTrail node requires the following ports to be allowed in order to operate properly.

* 8900 (default node API endpoint)
* 9000 (networking port for communication with other nodes)

{% hint style="warning" %}
Please keep in mind that different cloud providers use different security practices when it comes to configuring firewalls on the servers. Make sure that your firewall rules are configured according to the practices of the cloud provider you chose. &#x20;
{% endhint %}

