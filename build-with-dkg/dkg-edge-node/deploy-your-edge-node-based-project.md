---
hidden: true
---

# Deploy your Edge-Node-based project

Following the steps bellow will allow you to clone and execute the automated installer, enabling you to easily set up the DKG Edge Node with minimal configuration.&#x20;

**The deployment involves a few simple steps:**&#x20;

* Cloning the [installer repository](https://github.com/OriginTrail/edge-node-installer)
* Updating the installer with your forked repositories (URL's)
* Running the installer&#x20;
* Configuring DKG Edge Node services&#x20;

This process ensures a fast and efficient deployment, making it ideal for those who want to get hands-on with DKG Edge Node functionalities without extensive setup.

{% hint style="info" %}
Please note that the automated installer currently supports Ubuntu versions 20.04, 22.04, and 24.04.
{% endhint %}

## System Requirements

* **OS:** Linux
* **RAM:** At least 8 GB
* **CPU:** 4
* **Storage:** At least 20 GB of available space
* **Network:** Stable internet connection

## Software dependencies

Ensure the following services are installed:

* Git

## Step 1: Clone the installer repository

In order to clone the Edge Node installer repository, simply run the commands below on your Linux server:

```sh
git clone https://github.com/OriginTrail/edge-node-installer.git
cd edge-node-installer
chmod +x edge-node-installer.sh
```

## Step 2: Update the installer with your repositories

{% hint style="info" %}
If you do not provide the installer with your forked Edge Node services (repositories), it will setup the basic two examples of knowledge mining pipelines and one SPARQL-based Decentralized Retrieval Augmented Generation (dRAG).
{% endhint %}

Open installer with `nano` or any other file editor, and replace the following values in the installer to match your repositories:

```bash
edge_node_knowledge_mining="<github_repository_URL>"
edge_node_auth_service="<github_repository_URL>"
edge_node_drag="<github_repository_URL>"
edge_node_api="<github_repository_URL>"
edge_node_interface="<github_repository_URL>"
```

{% hint style="info" %}
If your repositories are not publicly available, the URL should contain a token. \
Example: **ghp\_4JEzJXwD....@github.com/\<organization>/\<project>.git**
{% endhint %}

## Step 3: Execute the installer

Simply run the installer with the command provided below:

```bash
bash edge-node-installer.sh
```

{% hint style="info" %}
The installation process may take up to 30 minutes. &#x20;
{% endhint %}

When the installation process is finalized, you will be provided with the following Edge Node services deployed to your Linux server:

* [V8 DKG Runtime Node](https://github.com/OriginTrail/ot-node/tree/v8/release/testnet)
* [Edge Node Interface](https://github.com/OriginTrail/edge-node-interface)
* [Edge Node API](https://github.com/OriginTrail/edge-node-api)
* [Knowledge Mining API](https://github.com/OriginTrail/edge-node-knowledge-mining)
* [dRAG](https://github.com/OriginTrail/edge-node-drag)
* [Authentication Service](https://github.com/OriginTrail/edge-node-authentication-service)

Each Edge Node service will have its required runtime environment and dependencies properly configured. This includes the installation and setup of **Node.js (with npm), Python, MySQL, Redis**, and **Apache Airflow**.&#x20;

All services will be configured to run as **`systemd`** processes, which will be enabled and started automatically upon installation.

## Step 4: Configure Edge Node services

### 3.1 - Configure your V8 DKG Runtime Node:

In order to configure and initialize your V8 DKG Runtime Node, you will have to populate a few important placeholders in **.origintrail\_noderc** configuration file:

* \<SERVER\_PUBLIC\_IP> (to prevent issues with NAT)
* \<your\_sharesTokenSymbol>
* \<your\_sharesTokenName>
* \<RPC\_ENDPOINT> (Base Sepolia)&#x20;
* \<MANAGEMENT\_KEY\_PUBLIC\_ADDRESS>
* \<OPERATIONAL\_KEY\_PUBLIC\_ADDRESS>
* \<OPERATIONAL\_KEY\_PRIVATE\_ADDRESS>
* Whitelist your Linux server IP address on the V8 DKG Runtime node (see below):

```json
"auth": {
    "ipWhitelist": [
      "::1",
      "127.0.0.1",
      "<server_public_ip>"
    ]
  }
```

{% hint style="info" %}
If you are not familiar with how wallets work on V8 DKG Runtime Node, please check the section related to wallets, [here](../dkg-core-node/run-a-v8-core-node-on-testnet/preparation-for-v8-dkg-core-node-deployment.md).
{% endhint %}

&#x20;Once the configuration files have been provided with all the required inputs, initiate your node with the **`otnode-start`** command. Additionally, make sure that you check your V8 DKG Runtime Node logs by executing the **`otnode-logs`** command, and wait for the "**Node is up and running!**" log to be printed.

### 3.2 - Configure the rest of the DKG Edge Node services

The instructions for configuring DKG Edge Node services are available in the README file of each service's GitHub repository, where you can follow the steps provided.&#x20;

* **Edge Node Authentication Service** ([README](https://github.com/OriginTrail/edge-node-authentication-service) instructions)
* **Edge Node API** ([README](https://github.com/OriginTrail/edge-node-api) instructions)
* **Edge Node UI** ([README](https://github.com/OriginTrail/edge-node-ui) instructions)
* **Edge Node Knowledge Mining** ([README](https://github.com/OriginTrail/edge-node-knowledge-mining) instructions)
* **Edge Node dRAG** ([README](https://github.com/OriginTrail/edge-node-drag) instructions)

## Need help?

If you encounter any issues during the installation process or have questions regarding any of the above topics, we kindly invite you to join our official [Discord](https://discordapp.com/invite/FCgYk2S) and ask for assistance.
