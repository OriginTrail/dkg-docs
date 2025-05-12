---
description: >-
  This page will guide you through the DKG Edge Node installation process for
  MacOS and Linux
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
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

#### 2.1 - Clone the edge-node-installer repository using git:

<pre class="language-sh"><code class="lang-sh">git clone https://github.com/OriginTrail/edge-node-installer.git
<strong>cd edge-node-installer
</strong></code></pre>

## 3. Configure the environment (.env)

#### 3.1 - Create .env file using .env.example:

```bash
cp .env.example .env
```

The **.env.example** is used as a guide template, but is well documented and should help you understand what each of the variables mean.

#### **3.2 - Populate .env file:**&#x20;

To simplify the development setup, we’ve provided the `env-setup.js` script. This script will automatically generate and populate all required `.env` parameters, including:

* Management keys
* Operational keys
* Publishing keys (for all supported chains)
* Node name (same across all chains)

{% hint style="success" %}
We assume that Node.js is already installed on your system to run the `env-setup.js` script.\
If Node.js is not installed or you're setting up a fresh system, we recommend using NVM to install Node.js version 20 along with npm.
{% endhint %}

Once Node.js and npm are successfully installed, you can use the following command to populate your `.env` file:

```
npm install ethers && node env-setup.js
```

#### 3.3 Funding your keys:

Once the `.env` file is populated with the mandatory parameters, you will have to fund the keys (wallets) which were added to the .env file.&#x20;

1. Open your `.env` file using `nano` or any text editor.
2. Locate the following wallet entries for each blockchain:
   * `OPERATIONAL_KEY_PUBLIC_ADDRESS`&#x20;
   * `MANAGEMENT_KEY_PUBLIC_ADDRESS` &#x20;
   * `PUBLISH_WALLET_01_PUBLIC_KEY`
3. Fund wallets for at least one blockchain under `NODE ENGINE PARAMETERS` in the `.env` file using the instructions from the [Faucet documentation page](../../../useful-resources/test-token-faucet.md), so your node can create its on-chain profile.&#x20;

**Note:** `OPERATIONAL_KEY_PUBLIC_ADDRESS`  and `MANAGEMENT_KEY_PUBLIC_ADDRESS`  require a small amount of native token (e.g., NEURO, ETH, xDAI) while `PUBLISH_WALLET_01_PUBLIC_KEY`  require both native and TRAC token in order to be able to publish Knowledge Assets

{% hint style="warning" %}
Ensure your Edge Node creates its profile on the blockchain set in `DEFAULT_PUBLISH_BLOCKCHAIN` which is by default set to **neuroweb.** \
You can update this parameter according to your needs.
{% endhint %}

#### 3.4  - Configure LLM functionality:

Edge Node components rely on LLMs to function properly. To ensure full functionality, you must add at least one of the two external service keys to your `.env`:&#x20;

* `OPEN_AI_KEY` or&#x20;
* `ANTHROPIC_API_KEY`

#### Optional .env parameters:

The Edge Node supports additional external services and tools that can be configured via the `.env` file before running the installer. Below is a list of supported services represented as configuration parameters:

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

## 4. Run installation: <a href="#id-3.-execute-the-installer-by-running" id="id-3.-execute-the-installer-by-running"></a>

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
* 8008 - Airflow web-server

\
UI (Edge node interface) will be cloned and configured in the following paths:

* MacOS - /opt/homebrew/etc/nginx/servers/edge-node-ui
* Linux - /var/www/edge-node-ui

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
