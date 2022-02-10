---
description: How to setup a local and shared development environment
---

# Setting up your development environment

{% hint style="info" %}
These setup instructions for DKGv6 are "Work in progress" and are subject to change. The development team expects to introduce improvements of setting up the DKGv6 node in local environment in the future.
{% endhint %}

{% hint style="success" %}
Need any assistance with node setup? Join the DKGv6 Discord chat and find help within the OriginTrail tech community!
{% endhint %}

## Quick Start

### Prerequisites

* This instructions are made for MacOS and Linux
* An installed and running **GraphDB**
  * In order to download GraphDB, please visit their [official website](https://www.ontotext.com/products/graphdb/graphdb-free/) and fill out a form. Installation files will be provided to you via email.
* An installed and running **MySQL**
  * You need to create empty table named **operationaldb** inside MySQL
* You should have installed **npm** and **Node.js (v14)**

### Installation steps

#### Step 1 - Get the DKG code by cloning the  repo and checking out the proper branch

```
git clone https://github.com/OriginTrail/ot-node
cd ot-node
git checkout v6/develop
```

#### Step 2 - Install dependencies

```
npm install
```

\
**Step 3 -** Create **.env** file the ot-node root folder and add public and private keys for blockchain:

```
NODE_ENV=development
PUBLIC_KEY=<insert_here>
PRIVATE_KEY=<insert_here>
```

{% hint style="info" %}
OriginTrail v6 development node is running on **Polygon Mumbai (testnet)** network **** and it is currently not requiring any test TRAC tokens. Make sure that the wallet you are using in your configuration file is funded with test MATIC tokens.
{% endhint %}

#### Polygon Mumbai MATIC faucet: [https://faucet.polygon.technology/](https://faucet.polygon.technology)

#### Step **5 -** Run DB migrations:

```
npx sequelize --config=./config/sequelizeConfig.js db:migrate
```

****\
**Step 6 - Start OriginTrail v6 node**\
****In order to start the node, execute the following command:

```
node index.js
```

![Successfully started](<../.gitbook/assets/Screen Shot 2022-01-19 at 12.32.39.png>)

## Running multiple nodes in local

If you managed to setup one node to function properly, then you can proceed and run the **local network setup** script to have multiple nodes running in local environment.

Running this command you will start a network with 4 nodes in local environment:

```
bash tools/local-network-setup/setup-macos-environment.sh 
```

Running this command you can specify how many nodes you want to start:

```
bash tools/local-network-setup/setup-macos-environment.sh --nodes=10
```

## Running nodes on testnet

For a shared development environment, we recommend deploying DKG testnet nodes on the beta testnet - instructions can be found [here](https://docs.origintrail.io/dkg-v6-upcoming-version/setup-instructions-dockerless).&#x20;
