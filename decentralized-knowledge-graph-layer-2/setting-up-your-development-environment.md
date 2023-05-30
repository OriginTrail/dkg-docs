---
description: How to setup a local and shared development environment
---

# Development environment setup

These setup instructions for DKG v6 are "Work in progress" and are subject to change. The development team expects to introduce improvements of setting up the DKGv6 node in local environment in the future.

{% hint style="success" %}
Need any assistance with node setup? Join the DKGv6 [Discord ](https://discord.com/invite/FCgYk2S)chat and find help within the OriginTrail tech community!
{% endhint %}

## Quick Start

### Prerequisites

* This instructions are made for MacOS and Linux
* An installed and running **Blazegraph**
  * In order to download and run Blazegraph, please visit their [official website](https://blazegraph.com/).
* An installed and running **MySQL**
  * You need to create empty table named **operationaldb** inside MySQL
* You should have installed **npm** and **Node.js (v16)**

### Installation steps

#### Step 1 - Get the DKG code by cloning the repo and checking out the proper branch

```
git clone https://github.com/OriginTrail/ot-node
cd ot-node
```

#### Step 2 - Install dependencies

```
npm install
```

\
**Step 3 -** Create **.env** file the ot-node root folder and add following line:

```
NODE_ENV=development
RPC_ENDPOINT=http://127.0.0.1:8545
```

\
**Step 4 - Start local DKG network**

In order to start the local DKG network, run the **local network setup** script to have multiple nodes running in local environment:

{% hint style="warning" %}
The script below only works for MacOS. If you need help with the Linux setup contact the team on [Discord](https://discord.com/invite/FCgYk2S).
{% endhint %}

\
In order to start the local DKG network, run the **local network setup** script to have multiple nodes running in local environment:

```
bash tools/local-network-setup/setup-macos-environment.sh --nodes=12
```

<figure><img src="../.gitbook/assets/Screen Shot 2023-02-22 at 14.51.44 (1).png" alt=""><figcaption><p>Successfully started node</p></figcaption></figure>

## Running nodes on testnet

For a shared development environment, we recommend deploying DKG testnet nodes on the testnet - instructions can be found [here](https://docs.origintrail.io/dkg-v6-upcoming-version/setup-instructions-dockerless).
