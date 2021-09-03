---
description: How to setup a local and shared development environment
---

# Setting up your development environment

## Setting up a local DKG network on your machine

You can set up an entire DKG network locally on your machine using the local network setup tool. The Local Network Setup tool \(LNS\) will start a local blockchain \(ganache\), deploy the required smart contracts, set up the configuration files for the nodes and start the nodes in separate windows. From there you're ready to send API calls to your local nodes and test new features on the ot-node without worrying about funds, servers or network connectivity issues.

You can find the [LNS Github repo here ](https://github.com/OriginTrail/ot-node/tree/develop/tools/local-network-setup)\(with the same instructions as on this page\).  


## Quick Start

### Prerequisites

* You need to have arangodb 3.5 installed and running on your machine. Find the appropriate binary on the [ArangoDB website](https://download.arangodb.com/arangodb35/index.html)
* You need to use Node.js version **9.11.2**
* You should have ot-node dependencies installed with the `npm install` command
* Install ganache-cli locally \( `npm install -g ganache-cli` \)
* generate a .env file in the ot-node root folder and insert `NODE_ENV=development` for local development

### How to start

From the ot-node directory, run the below command

```bash
npm run tools:lns:start
```

## Usage

### Specifying the number of nodes

The LNS tool deploys 4 nodes by default, each connected to three blockchain implementations which are running on a local ganache process. You can specify to run anywhere between one and ten nodes with the `--nodes` parameter.

```bash
npm run tools:lns:start -- --nodes=10
```

The first node will be named `DC`, while subsequent nodes will be named `DH1, DH2, ...`.

### Editing the node configuration

#### Editing the configuration for all nodes

If you need to edit the configuration for every node, before you run the nodes you can edit the `config_template.json` file and the new configuration will be loaded during node set up.

#### Editing the configuration for a single node

If you want to edit a single node's configuration, you can do it in two ways:

1. Before you start the nodes, edit the `generate_config_files.js` with a specific condition. For example, if you wanted to set the fifth node to reject all offers you'd add something like the following:

   ```javascript
   if (node_name === 'DH4') {
    parsedTemplate.blockchain.implementations[0].dh_price_factor = "10000000";
    parsedTemplate.blockchain.implementations[1].dh_price_factor = "10000000";
    parsedTemplate.blockchain.implementations[2].dh_price_factor = "10000000";
   }
   ```

2. Once the nodes are set up, each node has its own node configuration file in the `temporary-config-files` directory, which you can edit directly. For example, if you wanted to enable additional logs on the DC node you could add the following to `DC.json`. **Note:** After editing the the configuration this way you'll need to stop and start the node again for the changes to take effect.

   ```javascript
   {
    "...": "...",
    "commandExecutorVerboseLoggingEnabled": true
   }
   ```

  

3.  Once your local network is set up, you can go ahead and access your nodes' API at:
   * DC node: http://0.0.0.0:8900
   * DH1 node: http://0.0.0.0:8901, DH2 node at http://0.0.0.0:8902 etc

### Using one of the testnets

For a shared development environment, we recommend deploying DKG testnet nodes on the stable testnet - instructions can be found [here](../running-nodes/node-setup/). 





