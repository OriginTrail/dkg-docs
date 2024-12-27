---
description: How to setup a local and shared development environment
---

# Development environment setup

Quick Start

### Prerequisites

* This instructions are made for MacOS and Linux
* An installed and running **Blazegraph**
  * In order to download and run Blazegraph, please visit their [official website](https://blazegraph.com/).
* An installed and running **MySQL**
  * You need to create empty table named **operationaldb** inside MySQL.
* You should have **npm** and **Node.js (v16)** installed

{% hint style="success" %}
Need any assistance with node setup? Join the [Discord ](https://discord.com/invite/FCgYk2S)chat and find help within the OriginTrail tech community!
{% endhint %}

### Installation steps

First, clone the ot-node repo by running:

```
git clone https://github.com/OriginTrail/ot-node
```

Navigate to it:

```
cd ot-node
```

Change the branch:

```
git checkout v8/develop
```

Then, install the required dependencies by running:

```
npm install
```

Next, create a file called  `.env` and add following lines:

```
NODE_ENV=development
RPC_ENDPOINT_BC1=http://127.0.0.1:8545
RPC_ENDPOINT_BC2=http://127.0.0.1:9545
```

In order to start the local DKG network, run the **local network setup** script to have multiple nodes running in local environment. It's recommended to run at least 12 nodes (1 bootstrap and 11 subsequent nodes) to ensure stability of operation.

{% hint style="warning" %}
The scripts below only work for macOS and Linux (or Windows WSL). If you need help with the setup, contact the team on [Discord](https://discord.com/invite/FCgYk2S).
{% endhint %}

\
In order to start the local DKG network on **macOS**, run the following command:

```bash
bash tools/local-network-setup/setup-macos-environment.sh --nodes=12
```

For running the local DKG network on **Linux**, run the following command:

```bash
./tools/local-network-setup/setup-linux-environment.sh --nodes=12
```

## Running nodes on V8 Testnet

For a shared development environment, we recommend deploying DKG V8 Testnet nodes - instructions can be found [here](https://docs.origintrail.io/dkg-v8-upcoming-version/run-a-v8-core-node-on-testnet).

## Contributing

These setup instructions for DKG v8 are a "Work in progress" and are subject to change. The development team expects to introduce improvements of setting up the DKGv8 node in local environment in the future.

As ot-node is open source, we happily invite you to join us in our mission of building the decentralized knowledge graph - we're excited for your contributions! Please visit the [Github](https://github.com/OriginTrail/ot-node) repo for more info.

