---
description: How to setup a local and shared development environment
---

# Development environment setup

## Quick Start

These instructions are made for macOS and Linux.

### Prerequisites

* An installed and running **Blazegraph**
  * In order to download and run Blazegraph, please visit their [official website](https://blazegraph.com/).
* An installed and running **MySQL**
  * You need to create an empty table named **operationaldb** inside MySQL.
* You should have **npm** and **Node.js (v16)** installed.

{% hint style="success" %}
Need any assistance with node setup? Join the [Discord ](https://discord.com/invite/xCaY7hvNwD)chat and find help within the OriginTrail tech community!
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

Next, create a file called  `.env` and add the following lines:

```
NODE_ENV=development
RPC_ENDPOINT_BC1=http://127.0.0.1:8545
RPC_ENDPOINT_BC2=http://127.0.0.1:9545
```

To start the local DKG network, run the **local network setup** script to install multiple node engines in the local environment. To ensure stability of operation, it is recommended to run at least 5 node engines (1 bootstrap and 4 subsequent node engines).

{% hint style="warning" %}
The scripts below only work for macOS and Linux (or Windows WSL).&#x20;

If you need help with the setup, contact the core development team on [Discord](https://discord.com/invite/FCgYk2S).
{% endhint %}

\
In order to start the local DKG network on **macOS**, run the following command:

```bash
bash tools/local-network-setup/setup-macos-environment.sh --nodes=5
```

For running the local DKG network on **Linux**, run the following command:

```bash
./tools/local-network-setup/setup-linux-environment.sh --nodes=5
```

## Running node engines on the DKG testnet

For a shared development environment, we recommend deploying DKG testnet node engines - instructions can be found [here](../dkg-core-node/run-a-v8-core-node-on-testnet/).



{% hint style="info" %}
### Contributing

These setup instructions are a work in progress and are subject to change. The core development team expects to introduce improvements in setting up the DKG node engine in the local environment in the future.

As ot-node is open source, we **happily invite you to contribute to building the Decentralized Knowledge Graph.** We're excited about your contributions!&#x20;

Please visit the [GitHub](https://github.com/OriginTrail/ot-node) repo for more info.
{% endhint %}
