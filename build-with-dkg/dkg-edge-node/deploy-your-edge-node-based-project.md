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

{% hint style="info" %}
This page is intended for developers who have already built [custom Edge Node components](customize-and-build-with-the-edge-node.md) and are looking to deploy their solution to a server. As such, instructions for configuring node keys (wallets) and other mandatory parameters in the `.env` file are not included here. These parameters are still required for the Edge Node to function properly so the list of mandatory `.env` parameters can be found under [Automated boilerplate setup](get-started-with-the-edge-node-boilerplate/automated-setup-with-the-installer.md).
{% endhint %}

## Step 1: Clone the installer repository

In order to clone the Edge Node installer repository, simply run the commands below on your Linux server:

```sh
git clone https://github.com/OriginTrail/edge-node-installer.git
cd edge-node-installer
chmod +x edge-node-installer.sh
```

## Step 2: Update the installer with your repositories

Open `.env` file in the Edge node installer directory with `nano` or any other file editor, and add your repositories URL's:

```bash
EDGE_NODE_KNOWLEDGE_MINING_REPO=
EDGE_NODE_DRAG_REPO=
EDGE_NODE_API_REPO=
EDGE_NODE_UI_REPO=
EDGE_NODE_AUTH_SERVICE_REPO=
```

{% hint style="info" %}
If you do not provide the installer with your forked Edge Node services (repositories), it will deploy the basic two examples (boilerplate) of knowledge mining pipelines and one SPARQL-based Decentralized Retrieval Augmented Generation (dRAG) to the server.
{% endhint %}

If your Github repositories are private, make sure to provide the installer with your Github credentials by passing them to the following `.env` variables:

```bash
REPOSITORY_USER=
REPOSITORY_AUTH=
```

{% hint style="success" %}
Since you are deploying your solution to Linux server we suggest that you configure the  `DEPLOYMENT_MODE=production`  and the installer will enable and start all its services once installed since they run as systemd.
{% endhint %}

## Step 3: Run the installer

{% hint style="info" %}
It is assumed that, in addition to your GitHub repository URLs and GitHub credentials, you have provided the Edge Node installer with its other mandatory parameters via the `.env` file such as keys (wallets) and other required parameters.
{% endhint %}

Simply run the installer with the command provided below:

```bash
bash edge-node-installer.sh
```

{% hint style="info" %}
The installation process may take up to 30 minutes. &#x20;
{% endhint %}

All  Edge node services will be configured to run as **`systemd`** processes, which will be enabled and started automatically upon installation.

## Step 4: Configure Edge Node services

### 3.1 - Configure your V8 DKG Core Node:

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



## Need help?

If you encounter any issues during the installation process or have questions regarding any of the above topics, we kindly invite you to join our official [Discord](https://discordapp.com/invite/FCgYk2S) and ask for assistance.
