---
description: Deployment of the Edge node using the automated installer
icon: rectangle-terminal
---

# Automated deployment with installer

### Edge Node deployment process overview

Following the steps below will allow you to clone the automated installer, populate the environment file (.env), and then run the installer for a smooth setup of the DKG Edge Node on a Linux server.

**These instructions cover the following:**

1. Cloning the [installer repository](https://github.com/OriginTrail/edge-node-installer)
2. Populate the installer's `.env` file with:
   * Your forked repository URLs
   * Edge node names for each supported blockchain
   * Edge Node wallet keys
   * Publishing wallet keys
   * OpenAI or Anthropic API key
3. Run the installer

### System Requirements

In order to successfully deploy your Edge node solution, you will need a **clean** Linux instance as described below

* **OS:** Linux
* **RAM:** At least 8 GB
* **CPU:** 4
* **Storage:** At least 20 GB of available space
* **Network:** Stable internet connection

{% hint style="info" %}
Please note that the automated installer currently supports Ubuntu versions 20.04, 22.04, and 24.04.
{% endhint %}

## **Edge node** deployment preparation

{% hint style="success" %}
With these requirements prepared, you'll be ready to quickly populate the `.env` file and proceed with running the installer.
{% endhint %}

**1. Software Dependencies:**

* [Git](https://git-scm.com/downloads)  – Required for cloning the installer repository to the server.\


**2. Edge Node keys (wallets):**

The Edge Node requires three types of keys (wallets):

* Management keys
* Operational keys
* Publishing keys

**Before deploying to a server, ensure your custom Edge Node project has already been developed** and\
that you are familiar with the wallet preparation process outlined in the [Funding Your Keys](../get-started-with-the-edge-node-boilerplate/automated-setup-with-the-installer.md#id-3.3-funding-your-keys) section of the [Get started with the Edge Node boilerplate](../get-started-with-the-edge-node-boilerplate/) project.&#x20;

{% hint style="info" %}
While the boilerplate offers helpful guidance, it is intended as a starting point for development, not a deployment-ready solution.
{% endhint %}

{% hint style="success" %}
If you're deploying on **mainnet**, ensure the following:

* You have access to TRAC tokens on the blockchains where you intend to deploy your Edge Node
* You understand how to bridge TRAC tokens to **Gnosis** or **Base**, or use **Teleport** to transfer them to **Neuroweb**.
* Your **operational** and **management** keys are properly funded with both TRAC and the native token, depending on the blockchain to which you are deploying your node.
{% endhint %}

**Useful documentation:**

* A list of exchanges where TRAC tokens can be acquired is available on our [official website](https://origintrail.io/get-started/trac-token).
* TRAC Teleport to Neuroweb is explained [here](../../teleport-instructions-neuroweb.md).
* Bridging TRAC to Base is explained [here](../../../../dkg-knowledge-hub/learn-more/connected-blockchains/base-blockchain/#bridging-trac-to-base).
* Bridging TRAC to Gnosis is explained [here](../../../../dkg-knowledge-hub/learn-more/connected-blockchains/gnosis-chain/#bridging-trac-to-gnosis).
* Neuroweb mainnet explorer is available [here](https://neuroweb.subscan.io/).
* Neuroweb testnet explorer is available [here](https://neuroweb-testnet.subscan.io/).
* Base Sepolia explorer is available [here](https://sepolia.basescan.org/).
* Base mainnet explorer is available [here](https://basescan.org/).
* Gnosis Chiado explorer is available [here](https://gnosis-chiado.blockscout.com/).
* Gnosis mainnet explorer is available [here](https://gnosisscan.io/).

**3. LLM functionality:**

Edge Node components require a Large Language Model (LLM) to operate. To ensure full functionality, you must provide at least one of the supported external API keys below:

* [**OpenAI**](https://platform.openai.com/api-keys) **API Key** – Used to access OpenAI’s GPT models.\
  Example: `sk-4hsR2exampleXv29NSHtDyzt0NlFgk1LXj6zS7...`
* [**Anthropic**](https://console.anthropic.com/account/keys) **API Key** – Used to access Anthropic’s Claude models.\
  Example: `claude-56a8e5eexamplef27b5b6e47b1...`

{% hint style="success" %}
🔐 Ensure that the API keys have the necessary usage quotas and permissions based on your expected workload. Always keep them secure and never share them publicly.
{% endhint %}

## Deployment guide (step by step)

With all prerequisites in place, you can proceed to clone the installer repository, prepare the `.env` file with the required parameters, and deploy your Edge Node solution by following the steps below.

### 1. Cloning the installer

Once all requirements are prepared, SSH into your Linux server and clone the installer repository using the commands provided below:

```sh
git clone https://github.com/OriginTrail/edge-node-installer.git && cd edge-node-installer
```

#### 1.1 - Create .env file

Based on the .env.example file create your `.env`  which will be used by the automated installer for the deployment of your Edge Node.

```bash
cp .env.example .env
```

### **2. Configure your Edge Node**&#x20;

You are now ready to populate the `.env` file and configure the installer with the necessary parameters.

{% hint style="success" %}
The .env file contains the explanation for each of the parameters to help you understand the configuration.
{% endhint %}

**2.1 - Deployment mode**

This field determines how the Edge Node services are handled post-installation. You can choose between two options:

* **`development`** – Installs all required services as **`systemd` units**, but does **not** enable or start them automatically.&#x20;
* **`production`** – Installs the services as **`systemd` units**, and automatically enables and starts them once the installation is complete. This is the recommended option for live environments where the node should be operational immediately.

**2.2 - Blockchain environment**

Choose between **`mainnet`** or **`testnet`**. \


**2.3 - Default publish blockchain**

Specify the blockchain that will be used for publishing Knowledge Assets. Enter one of the currently supported options: `neuroweb`, `base`, or `gnosis`.

#### **2.4 - Publishing Keys (wallets)**

You must provide public and private key pairs for up to three wallets that will be used for publishing Knowledge Assets to the selected blockchain (`DEFAULT_PUBLISH_BLOCKCHAIN`). The keys should be funded with both the **TRAC token** and the **native token** of the blockchain passed via "`DEFAULT_PUBLISH_BLOCKCHAIN`" parameter in `.env`.&#x20;

* **`PUBLISH_WALLET_01_PUBLIC_KEY`**: Public key for the first publishing wallet. <mark style="color:red;">**\[mandatory]**</mark>
* **`PUBLISH_WALLET_01_PRIVATE_KEY`**: Private key for the first publishing wallet. <mark style="color:red;">**\[mandatory]**</mark>
* **`PUBLISH_WALLET_02_PUBLIC_KEY`**: Public key for the second publishing wallet.
* **`PUBLISH_WALLET_02_PRIVATE_KEY`**: Private key for the second publishing wallet.
* **`PUBLISH_WALLET_03_PUBLIC_KEY`**: Public key for the third publishing wallet.
* **`PUBLISH_WALLET_03_PRIVATE_KEY`**: Private key for the third publishing wallet.

{% hint style="success" %}
If you're deploying on **mainnet**, ensure the following:

* `BLOCKCHAIN_ENVIRONMENT` parameter in the `.env` is changed to `mainnet`
* Ensure that you've bridged TRAC to Base or Gnosis, or used TRAC Teleport if Neuroweb is your blockchain of choice
{% endhint %}

#### **2.5 - Node Engine configuration (ot-node service)**

{% hint style="warning" %}
At least one blockchain configuration is required for the successful deployment of the Edge Node.\
Ensure your Edge Node creates its profile on the blockchain set in `DEFAULT_PUBLISH_BLOCKCHAIN` (**neuroweb** by default)**.**\
You can choose between `neuroweb`, `base` and `gnosis` blockchains.
{% endhint %}

**Neuroweb:**

* **`NEUROWEB_NODE_NAME`**: Name of your node on Neuroweb.
* **`NEUROWEB_OPERATOR_FEE`**: The operator fee for your Neuroweb node. Set to `0` if no fee is required.
* **`NEUROWEB_MANAGEMENT_KEY_PUBLIC_ADDRESS`**: Public address of your Neuroweb management key.
* **`NEUROWEB_OPERATIONAL_KEY_PUBLIC_ADDRESS`**: Public address of your Neuroweb operational key.
* **`NEUROWEB_OPERATIONAL_KEY_PRIVATE_ADDRESS`**: Private address of your Neuroweb operational key.

**Base:**

* **`BASE_NODE_NAME`**: Name of your node on Base.
* **`BASE_OPERATOR_FEE`**: The operator fee for your Base node.
* **`BASE_MANAGEMENT_KEY_PUBLIC_ADDRESS`**: Public address of your Base management key.
* **`BASE_OPERATIONAL_KEY_PUBLIC_ADDRESS`**: Public address of your Base operational key.
* **`BASE_OPERATIONAL_KEY_PRIVATE_ADDRESS`**: Private address of your Base operational key.

**Gnosis:**

* **`GNOSIS_NODE_NAME`**: Name of your node on Gnosis.
* **`GNOSIS_OPERATOR_FEE`**: The operator fee for your Gnosis node. Set to `0` if no fee is required.
* **`GNOSIS_MANAGEMENT_KEY_PUBLIC_ADDRESS`**: Public address of your Gnosis management key.
* **`GNOSIS_OPERATIONAL_KEY_PUBLIC_ADDRESS`**: Public address of your Gnosis operational key.
* **`GNOSIS_OPERATIONAL_KEY_PRIVATE_ADDRESS`**: Private address of your Gnosis operational key.

{% hint style="info" %}
- Keys (wallets) provided in this section **will not** be used for publishing operations.
- Parameters for at least one blockchain are required for the node to be deployed sucessfully.
- If the operational keys are not funded with the native token on the blockchain of choice, Node Engine will fail to create its blockchain profile.
{% endhint %}

{% hint style="warning" %}
The management and operational keys require a small amount of the native token, NEURO for Neuroweb, ETH for Base, and xDAI for Gnosis, depending on the blockchain you prepare them for.
{% endhint %}

**2.6 - MySQL password**

During the deployment process, the password you provide via `DB_PASSWORD` parameter will be set as the **root password** for the MySQL database. By default, the password is set to `otnodedb` but you can change it as you like.

{% hint style="danger" %}
MySQL user is set to **root**, which is a requirement for the installation. Do not update `DB_USERNAME` parameter inside the `.env`.
{% endhint %}

{% hint style="info" %}
🔐 This root password is critical for accessing and managing your Edge node’s database. Do not share it or lose it.
{% endhint %}

#### **2.7 - GitHub Credentials**

To deploy private GitHub repositories, you will need to provide a valid GitHub personal access token (PAT). This token grants the access to your private repositories, allowing deployment of your custom Edge Node services.

* **`REPOSITORY_USER`**: Your GitHub username.
* **`REPOSITORY_AUTH`**: Your GitHub personal access token (token with appropriate scopes such as `repo`).

{% hint style="info" %}
The **token must be valid** and have the necessary **permissions** to access your private repositories.

Ensure the token includes the **`repo`** scope, which provides access to private repositories and other related features.

Token example: `ghp_1234abcd5678efgh9012ijklmnop34567890`
{% endhint %}

#### **2.8 - Edge node services (your forked repository URLs)**

If you're deploying customized or forked versions of the Edge Node services, you can provide the URLs to your private repositories via parameters presented below. The installer will use these links to clone and deploy the services.

* **`EDGE_NODE_KNOWLEDGE_MINING_REPO`**: Link to your fork of the knowledge mining service repository.
* **`EDGE_NODE_DRAG_REPO`**: Link to your fork of the DRAG service repository.
* **`EDGE_NODE_API_REPO`**: Link to your fork of the Edge Node API repository.
* **`EDGE_NODE_UI_REPO`**: Link to your fork of the Edge Node user interface repository.
* **`EDGE_NODE_AUTH_SERVICE_REPO`**: Link to your fork of the authentication service repository.

{% hint style="info" %}
🔐 Make sure your GitHub access token has the `repo` scope and is valid for cloning private repositories. Use the same token and username in the form fields provided above.
{% endhint %}

{% hint style="success" %}
If none of the URL's are defined, the installer will use the boilerplate Edge node services.
{% endhint %}

#### **2.9 - OpenAI or Anthropic API keys**

Edge Node components require a large language model (LLM) to operate. To ensure full functionality, you must provide at least one of the supported external API keys below:

* [**OpenAI**](https://platform.openai.com/api-keys) **API Key** (`OPENAI_API_KEY`) – Used to access OpenAI’s GPT models.\
  Example: `sk-4hsR2exampleXv29NSHtDyzt0NlFgk1LXj6zS7`
* [**Anthropic**](https://console.anthropic.com/account/keys) **API Key** (`ANTHROPIC_API_KEY`) – Used to access Anthropic’s Claude models.\
  Example: `claude-56a8e5eexamplef27b5b6e47b1`

{% hint style="success" %}
🔐 Ensure that the API keys have the necessary usage quotas and permissions based on your expected workload. Always keep them secure and never share them publicly.
{% endhint %}

### **\[OPTIONAL] Additional Edge node features**

The Edge Node supports additional external services and tools that can be configured via the `.env` file before running the installer. Below is a list of supported services represented as configuration parameters:\


* **Unstructured API key** (`UNSTRUCTURED_API_URL`) **-** Enables parsing PDF documents and can be obtained from [https://unstructured.io/api-key-free](https://unstructured.io/api-key-free)&#x20;

### 3. Deployment

Once all configuration parameters have been populated inside the `.env` correctly, you can proceed with deploying your Edge Node solution by running the edge-node-installer with the command below:

```sh
bash edge-node-installer.sh
```

{% hint style="warning" %}
The installation process may take approximately 20–30 minutes, so feel free to grab a coffee and be sure not to interrupt the process during this time.
{% endhint %}

### 4. Monitor the deployment process

To monitor the installation progress, SSH into your server using new terminal tab, `cd` into **edge-node-installer** directory and run the following command:

```shell
bash service-status.sh
```

This script will display the installation progress and current status of each Edge Node service.

While services are still being installed, a loading spinner will be shown for each one (as shown on the image below).

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-05-09 at 14.38.38.png" alt=""><figcaption><p><em><strong>Installation in progress</strong></em></p></figcaption></figure>

Once all services are marked as **"Active"**, your Edge Node is fully operational and ready to use.

<div align="center" data-full-width="false"><figure><img src="../../../../.gitbook/assets/Screenshot 2025-05-09 at 14.39.57.png" alt=""><figcaption><p><em><strong>Edge node deployment finalized</strong></em></p></figcaption></figure></div>

{% hint style="warning" %}
⚠️ To prevent potential conflicts or interruptions, it is recommended to avoid performing other actions such as installing additional packages or modifying configurations on the server during the Edge Node installation process.
{% endhint %}

### 5. Access your Edge node interface

Upon successful installation, the Edge Node user interface will be accessible at `http://<your-server-ip>/login`. Replace `<your-server-ip>` with the actual public IP address of your deployed server.

**Default login credentials:**

* Username: my\_edge\_node
* Password: edge\_node\_pass

### 6. Control and Manage Edge Node Services

Below is a list of the deployed services and how to manage them using `systemd`. \
All Edge Node services are deployed as `systemd` units, making them easy to manage.

#### List of Services:

1. **Edge Node API -** `edge-node-api.service`
2. **Authentication Service** – `auth-service.service`
3. **Knowledge Mining API** – `ka-mining-api.service`
4. **DRAG API** – `drag-api.service.service`
5. **OTNode** – `otnode.service`

#### Managing Services:

For each service, you can perform the following actions using the respective systemd commands:

* **Check service status:** `systemctl status <service-name>`
* **Start a service (if it is not already running):** `systemctl start <service-name>`
* **Stop a service:** `systemctl stop <service-name>`
* **Restart a service:** `systemctl restart <service-name>`
* **View Service Logs:** `journalctl -f -u <service-name>`

### Need assistance?

In case any of the services show an 'Inactive' status, you can contact our developers for assistance. Please reach out via [Discord](https://discord.com/invite/xCaY7hvNwD) or email us at **tech@origin-trail.com**. \
Be sure to include the installation log file (`installation_process.log`), which can be found in the `/root/edge-node-installer/log/` directory.
