---
description: >-
  This page will guide you through the DKG Edge Node installation process for
  MacOS and Linux
layout: editorial
---

# Automated setup with the installer

## Supported operating systems

* macOS
* Ubuntu 22.04 and Ubuntu 24.04

{% hint style="success" %}
Edge node installer will detect your operating system automatically (MacOS or Linux) so no configuration related to this is required by the user.
{% endhint %}

## 1. Pre-installation Requirements

Before getting started with the installation, there are a few important preparations to make. The process requires certain inputs such as wallet addresses and funds. The following sections will walk you through each of these prerequisites step by step.

#### 1.1. Software dependencies:

* [Git](https://git-scm.com/downloads)&#x20;
* [Homebrew](https://brew.sh/) (macOS)

#### 1.2. Edge node keys (wallets):

The Edge Node uses three types of keys: a **management key**, an **operational key**, and a **publishing key**. The management and operational keys need a small amount of the utility token based on the blockchain you will be using (NEURO, Base ETH, xDai) to sign transactions for certain operations, while publishing key requires both the utility and TRAC tokens to perform publishing operations.&#x20;

#### 1.3. Funding Edge node keys (wallets):

In order to fund your wallets, please refer to our faucet [page](https://docs.origintrail.io/useful-resources/test-token-faucet).

{% hint style="warning" %}
In order to receive TRAC to on Neuroweb, first acquire NEURO via faucet to initiate your wallet.
{% endhint %}

Note: To check your wallets funds on Neuroweb testnet, use [Subscan explorer](https://neuroweb-testnet.subscan.io/). &#x20;

## 2. Download the OriginTrail DKG Edge Node installer

Once you have your wallets funded and ready, you may proceed with cloning, configuring and running the Edge node installer by following the instructions provided below.

#### 2.1 Clone the edge-node-installer repository using git:

<pre class="language-sh"><code class="lang-sh">git clone https://github.com/OriginTrail/edge-node-installer.git
<strong>cd edge-node-installer
</strong></code></pre>

## 3. Configure the environment (.env)

#### 3.1 Prepare .env file using .env.example:

```bash
cp .env.example .env
```

The **.env.example** is used as a guide template, but is well documented and should help you understand what each of the variables mean.

#### 3.2  Open .env file using nano or any editor of your choice:

```
nano .env
```

Refer to the section below which will help you prepare your Edge node configuration.&#x20;

### MADATORY PARAMETERS (.env)

* <kbd>**DEPLOYMENT\_MODE**</kbd> (defaults to development) - The installer differentiates between two modes of operation - development and production, controlled by the DEPLOYMENT\_MODE variable. Production mode enables persistency, by enabling and starting services. **Production mode is currently only supported for systems with systemd.**
* <kbd>**DB\_USER**</kbd> - Set this to root&#x20;
* <kbd>**DB\_PASSWORD**</kbd> -  used to connect to existing **MySQL** instance, or setup an authenticated connection on fresh installs.

{% hint style="info" %}
If you already have a password for root user configured, pass it to the <kbd>**DB\_PASSWORD**</kbd> variable in .env. and installer will use it to setup MySQL tables required for the Edge node services.\
If you do not have MySQL running locally, <kbd>**DB\_PASSWORD**</kbd>  that you provide will be set as your root password.
{% endhint %}

* <kbd>**DEFAULT\_PUBLISH\_BLOCKCHAIN**</kbd> and <kbd>**BLOCKCHAIN\_ENVIRONMENT**</kbd>**&#x20;-** By default, the Edge Node publishes to the Neuroweb testnet blockchain. You can change this behaviour by editing the **DEFAULT\_PUBLISH\_BLOCKCHAIN** and **BLOCKCHAIN\_ENVIRONMENT** variables.&#x20;

{% hint style="info" %}
To prevent loss of funds, we recommend developing the Edge Node on the testnet environment at this stage since you are still getting familiar with the technology.
{% endhint %}

* <kbd>**PUBLISH\_WALLET\_01\_PUBLIC\_KEY**</kbd> and <kbd>**PUBLISH\_WALLET\_01\_PRIVATE\_KEY**</kbd> - Are keys used by the node to publish knowledge assets to the blockchain (using the default blockchain configuration mentioned above).

{% hint style="info" %}
At least 1 key should be provided to the installer in order for the Edge node to be able to execute publish operations.
{% endhint %}

* <kbd>**NODE ENGINE PARAMETERS**</kbd> - This section of the .env file is related to passing management and operational keys for your Edge node as well as RPC endpoints which your node engine will use to communicate with the selected blockchain.&#x20;

{% hint style="info" %}
Populating <kbd>**NODE ENGINE PARAMETERS**</kbd>  is required for at least 1 blockchain otherwise Edge node will not connect to any chain which will prevent services from properly operating.
{% endhint %}

{% hint style="info" %}
RPC endpoints for Neuroweb blockchain are not required and are automatically passed to your node engine (Core node) while for Base and Gnosis, we have already added public ones. \
**If you have your own, private RPC endpoint for Base or Gnosis, you can replace public ones.**
{% endhint %}

* <kbd>**OPEN\_AI\_KEY**</kbd>**&#x20; or&#x20;**<kbd>**ANTHROPIC\_API\_KEY**</kbd>**&#x20; -** Edge Node components rely on LLMs to function properly. To ensure full functionality, at least one of the two external services is required.

### OPTIONAL PARAMETERS (.env)

Edge node supports multiple external services and tools which can be configured via `.env`  before running the installer. The list of supported ones is presented below in the form of parameters:

```sh
# Unstructured.io - can be obtained from https://unstructured.io/api-key-free 
# (used by default for parsing PDF documents)
UNSTRUCTURED_API_URL=""

# HuggingFace - can be obtained from https://huggingface.co/settings/tokens 
# (used if you use vector search in your dRAG pipeline)
HUGGINGFACE_API_KEY=""

# Milvus (vector database) - Can be obtained from https://cloud.zilliz.com/ 
# (used if using vector search for the dRAG pipeline)
MILVUS_USERNAME=""
MILVUS_PASSWORD=""
MILVUS_URI=""
```

## 4. Execute the installer by running: <a href="#id-3.-execute-the-installer-by-running" id="id-3.-execute-the-installer-by-running"></a>

Once all the required parameters have been configured in the .env file, simply run the installer and wait for it to finish the Edge node setup.

```bash
bash edge-node-installer.sh
```

Edge node installer will deploy each component within the **edge\_node** directory: airflow, drag-api, edge-node-auth-service, ka-mining-api, ot-node.

Edge node services will be available and listening on the following local ports upon installation:

* UI will be available on [http://localhost](http://localhost)
* 3001 - Authentication service
* 3002 - API (backend)
* 5002 - dRAG
* 5005 - Knowledge mining
* 8900 - OT Node
* 8080 - Airflow web-server

\
UI (Edge node interface) will be cloned and configured in the following paths:

* MacOS - /var/www/edge-node-ui/
* Linux - /opt/homebrew/etc/nginx/servers/edge-node-ui

{% hint style="success" %}
The default login credentials for the Edge node UI are as follows:

**username:** my\_edge\_node

**password:** edge\_node\_pass
{% endhint %}

## Exploring Edge Node Capabilities

Once the Edge Node is up and running in your local environment, you’re ready to explore its features and capabilities. To get started, refer to the [**Usage Example**](usage-example.md) section to learn how to interact with the node and understand what it can do.

## Need help? <a href="#need-help" id="need-help"></a>

If you encounter any issues during the installation process or have questions about any of the topics above, jump into our official [Discord](https://discord.gg/xCaY7hvNwD) and ask for assistance.

Follow our official channels for updates:

* [X](https://x.com/origin_trail)
* [Medium](https://medium.com/origintrail)
* [Telegram](https://t.me/origintrail)
