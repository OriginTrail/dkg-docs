---
description: >-
  This page will help you prepare all the requirements for the V8 DKG Core Node
  installation process.
---

# Preparation for V8 DKG Core Node deployment

Before initiating an installer, there are a few important requirements that each node runner should prepare in order to initialize the v8 DKG node successfully.&#x20;

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
The installer script provided in these instructions is designed for installing the OriginTrail node on **Ubuntu 20.04 LTS , 22.04 LTS and 24.04 LTS** distributions.\
\
It is also possible to install the OriginTrail V8 Core Node on other systems, but it would require  modifications to the installer script. If you have any such modifications in mind, we highly encourage your contributions. Please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

{% hint style="warning" %}
During the v8 DKG Core Node installation process, the interactive installer will prompt you to input all the required information outlined below. Please make sure that you have all the requirement inputs prepared before running the installer.
{% endhint %}

## 2. Core Node keys (wallets):

DKG Core Nodes periodically execute blockchain transactions, for which they need node keys (wallets) of the H160 type (Ethereum). There are two categories of keys associated with DKG nodes however:

* **operational keys,** which are used directly by the node to make blockchain transactions. The nodes requires their private keys to be accessible (stored in the node configuration file), so that the node can sign transactions
* **admin keys**, which are used by the node operator, and not by the node itself. Admin keys are intended for administrative transactions to be done by the node operator (such as rotating keys), meaning the nodes don't need access to their private keys (doesn't need to be stored on the node server or configuration file). An admin key can be stored with a hardware wallet, a multisig or any other Ethereum compatible wallet of your preference.

To get a DKG node running, you will need **at least one operational key and one admin key**. For more information on  keys and their roles, please refer to the detailed [documentation](preparation-for-v8-dkg-core-node-deployment.md#node-keys-wallets).

The OriginTrail DKG nodes operate with a two token system:&#x20;

* the TRAC token which is the native utility token of the DKG used for knowledge publishing, and&#x20;
* the native blockchain token of the chosen chain, used for interacting with DKG smart contracts&#x20;

## 3. Funding your keys:

In order to acquire TRAC token on **Neuroweb**, [Teleport](https://docs.origintrail.io/dkg-v6-current-version/node-setup-instructions/installation-prerequisites/acquiring-tokens#teleporting-trac-tokens-to-neuroweb) process needs to be executed.&#x20;

For Base and Gnosis blockchains, you can use bridge applications as described [here](https://docs.origintrail.io/dkg-v6-current-version/node-setup-instructions/installation-prerequisites/acquiring-tokens#bridging-trac-to-gnosis).

## 4. Acquire RPC endpoints:

There are many RPC providers that host and provide Base and Gnosis endpoints and its up to a node runner to choose the best possible option for their nodes.

We recommend checking [Gnosis](https://docs.gnosischain.com/tools/RPC%20Providers/) and [Base](https://docs.base.org/docs/tools/node-providers/#coinbase-developer-platform-cdp) official documentation&#x20;

{% hint style="success" %}
Neuroweb RPCs are provided automatically during the node installation process.
{% endhint %}

## 5. Configure firewall on the server:

OriginTrail node requires the following ports to be allowed in order to properly operate.

* 8900 (default node API endpoint)
* 9000 (networking port for communication with other nodes)

{% hint style="warning" %}
Please keep in mind that different cloud providers use different security practices when it comes to configuring firewalls on the servers so make sure that firewall rules are configured according to their practices. &#x20;
{% endhint %}
