---
description: >-
  This section provides step-by-step instructions for deploying the DKG Edge
  Node using the Google Cloud Marketplace.
hidden: true
icon: cart-circle-check
cover: ../../../../.gitbook/assets/Edge Node GCP - docs visual11.png
coverY: 0
---

# Automated deployment via Google Cloud Marketplace

### Edge Node deployment process overview

This deployment method allows you to fully configure your Edge Node by filling out a solution form provided through the Google Cloud Marketplace. During the process, you’ll be guided through each required field and configure the following:

1. Your forked repository URLs
2. Edge Node names for each supported blockchain
3. Edge Node wallet keys
4. Publishing wallet keys
5. OpenAI or Anthropic API key

{% hint style="success" %}
Ensure you have a Google Cloud account with billing enabled and permissions to deploy Marketplace solutions.
{% endhint %}

## **Edge Node** deployment preparation

{% hint style="success" %}
With these requirements prepared, you'll be ready to quickly populate the solution form and proceed with the deployment of your Edge node.
{% endhint %}

**1. Edge Node keys (wallets):**

The Edge Node requires three types of keys:

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

**Useful links:**

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

**2. LLM functionality:**

Edge Node components require a large language model (LLM) to operate. To ensure full functionality, you must provide at least one of the supported external API keys below:

* [**OpenAI**](https://platform.openai.com/api-keys) **API Key** – Used to access OpenAI’s GPT models.\
  Example: `sk-4hsR2exampleXv29NSHtDyzt0NlFgk1LXj6zS7...`
* [**Anthropic**](https://console.anthropic.com/account/keys) **API Key** – Used to access Anthropic’s Claude models.\
  Example: `claude-56a8e5eexamplef27b5b6e47b1...`

{% hint style="success" %}
🔐 Ensure that the API keys have the necessary usage quotas and permissions based on your expected workload. Always keep them secure and never share them publicly.
{% endhint %}

## Deployment guide (step by step)

With all prerequisites in place, you can proceed to populate the solution form on Google Cloud Marketplace and deploy your Edge Node by following the steps below.

### **1. Log in to Google Cloud Console**

Access your [Google Cloud Console](https://console.cloud.google.com/) using your credentials.

### **2. Navigate to the Marketplace**

In the main menu, go to **Marketplace**, then search for **"OriginTrail node"** in the search bar

### **3. Configure Virtual Machine Parameters:**

* Choose your desired deployment region,&#x20;
* Machine type,&#x20;
* Disk size and other instance-related options

{% hint style="success" %}
The deployment page comes with recommended machine type and storage options already selected for optimal performance. You can adjust them if needed, but they are sufficient for most standard use cases.&#x20;
{% endhint %}

### **4. Configure your Edge Node**

You can now proceed with populating the Edge Node solution form and prepare for the deployment.

**4.1 - Deployment mode**

This field determines how the Edge Node services are handled post-installation. You can choose between two options:

* **`development`** – Installs all required services as **systemd units**, but does **not** enable or start them automatically. This mode is ideal for manual setup, debugging, or testing.
* **`production`** – Installs the services as **systemd units**, and automatically enables and starts them once the installation is complete. This is the recommended option for live environments where the node should be operational immediately.

{% hint style="success" %}
By default, this parameter is set to "production" for Google Cloud Marketplace deployments.
{% endhint %}

**4.2 - Blockchain environment**

Choose between **`mainnet`** or **`testnet`**. \


**4.3 - Publishing blockchain**

Specify the blockchain that will be used for publishing Knowledge Assets. Enter one of the currently supported options: `neuroweb`, `base`, or `gnosis`.



**4.4 - Publishing keys**

You must provide public and private key pairs for up to three wallets that will be used for publishing Knowledge Assets to the selected blockchain defined in "**Publishing blockchain"** input. \
The keys should be funded with both the **TRAC token** and the **native token** of the blockchain passed via **Publishing blockchain** form input.&#x20;

* `EVM Address 01 (Public Key)`: Public key for the first publishing wallet. <mark style="color:red;">**\[mandatory]**</mark>
* `EVM Address 01 (Private Key)`: Private key for the first publishing wallet. <mark style="color:red;">**\[mandatory]**</mark>
* `EVM Address 02 (Public Key)`: Public key for the second publishing wallet.
* `EVM Address 02 (Private Key)`: Private key for the second publishing wallet.
* `EVM Address 03 (Public Key)`: Public key for the third publishing wallet.
* `EVM Address 03 (Private Key)`: Private key for the third publishing wallet.

{% hint style="success" %}
If you're deploying on **mainnet**, ensure the following:

* **"Blockchain Environment"** parameter in the form is changed to `mainnet`
* Ensure that you've bridged TRAC to Base or Gnosis, or used TRAC Teleport if Neuroweb is your blockchain of choice.
{% endhint %}

**4.5 - Node Engine configuration (ot-node service)**

{% hint style="warning" %}
Ensure your Edge Node creates its profile on the blockchain defined in "**Publishing blockchain"** (**neuroweb** by default)**.** Choose between `neuroweb`, `base` and `gnosis` blockchains.
{% endhint %}

This section allows you to configure your node’s name for each supported blockchain, as well as define the management and operational keys (wallets).

* **Node Name**: You can configure the **same node name** for all supported blockchains. This name will help identify your node across all chains.
* **Management wallet (Public EVM key)**: This key grants administrative control, enabling you to configure parameters such as ASK, operator fees, and other settings.\
  You can use the **same management key** across all supported blockchains and this key should funded with the **native token** of each respective blockchain in order to be able to perform updates.
* **Operational wallet (Public EVM key)**: This key is used by the node to perform various blockchain operations.
* **Operational wallet (Private EVM key):** Your operational wallet's private key\
  **Note**: The operational keys **must be different** for each blockchain.

{% hint style="warning" %}
- Inputs for at least one blockchain configuration must be populated (NeuroWeb, Base, or Gnosis) for the successful deployment of the Edge Node.
- If the operational keys are not funded with the native token on the blockchain of choice, the node will fail to create its blockchain profile.
- The management and operational keys require a small amount of the native token, NEURO for Neuroweb, ETH for Base, and xDAI for Gnosis, depending on the blockchain you prepare them for.
{% endhint %}

**4.6 - MySQL password**

During the deployment process, the password you provide in this field will be set as the **root password** for the MySQL database installed on your Edge Node server.

{% hint style="info" %}
🔐 This root password is critical for accessing and managing your Edge node’s database. Do not share it or lose it.
{% endhint %}

**4.7 - Github credentials**

To deploy private GitHub repositories, you will need to provide a valid GitHub personal access token (PAT). This token grants access to your private repositories, allowing deployment of your custom Edge Node services.

* **"GitHub username":** Your GitHub username.
* **"GitHub token":** Your GitHub personal access token (token with appropriate scopes such as `repo`).

{% hint style="info" %}
The **token must be valid** and have the necessary **permissions** to access your private repositories.

Ensure the token includes the **`repo`** scope, which provides access to private repositories and other related features.

Token example: `ghp_1234abcd5678efgh9012ijklmnop34567890`
{% endhint %}



**4.8 - Edge node services (your forked repository URLs)**

If you are deploying customized or forked versions of the Edge Node services, you can provide the URLs to your private repositories in the corresponding form fields. The deployment process will use these URLs to clone and install your services as part of the setup.

* **Knowledge Mining Service Repository URL** – Link to your fork of the Knowledge Mining service
* **DRAG Service Repository URL** – Link to your fork of the DRAG service
* **Edge Node API Repository URL** – Link to your fork of the Edge Node API
* **Edge Node UI Repository URL** – Link to your fork of the Edge Node user interface
* **Authentication Service Repository URL** – Link to your fork of the Authentication service

{% hint style="info" %}
🔐 Make sure your GitHub access token has the `repo` scope and is valid for cloning private repositories. Use the same token and username in the form fields provided above.
{% endhint %}

{% hint style="success" %}
If none of the URLs are defined, the installer will use the boilerplate Edge node services.
{% endhint %}

\
**4.9 - OpenAI or Anthropic API key:**

Edge Node components require a large language model (LLM) to operate. To ensure full functionality, you must provide at least one of the supported external API keys below:

* [**OpenAI**](https://platform.openai.com/api-keys) **API Key** – Used to access OpenAI’s GPT models.\
  Example: `sk-4hsR2exampleXv29NSHtDyzt0NlFgk1LXj6zS7`
* [**Anthropic**](https://console.anthropic.com/account/keys) **API Key** – Used to access Anthropic’s Claude models.\
  Example: `claude-56a8e5eexamplef27b5b6e47b1`

{% hint style="success" %}
🔐 Ensure that the API keys have the necessary usage quotas and permissions based on your expected workload. Always keep them secure and never share them publicly.
{% endhint %}

### **\[OPTIONAL] Additional Edge node features**

The Edge Node supports additional external services and tools that can be configured via the `.env` file before running the installer. Below is a list of supported services represented as configuration parameters:\


* **Unstructured API key -** Enables parsing PDF documents and can be obtained from [https://unstructured.io/api-key-free](https://unstructured.io/api-key-free)&#x20;

### 5. Deployment

Once all parameters have been filled out correctly in the form, you can proceed with deploying your Edge Node.&#x20;

The server will become available for SSH access within a few minutes, even though the full installation of all Edge Node services may take approximately **20–30 minutes** to complete.

{% hint style="success" %}
Static IP address will be assigned to your server automatically and the firewall will be configured as required by the setup.
{% endhint %}

### 6. Monitor the deployment process

To monitor the installation progress, SSH into your server, `cd` into the **edge-node-installer** directory and run the following command:

```shell
bash service-status.sh
```

This script will display the installation progress and current status of each Edge Node service.

While services are still being installed, a loading spinner will be shown for each one (as shown in the image below).

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-05-09 at 14.38.38.png" alt=""><figcaption><p><em><strong>Installation in progress</strong></em></p></figcaption></figure>

Once all services are marked as **"Active"**, your Edge Node is fully operational and ready to use.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-05-09 at 14.39.57.png" alt=""><figcaption><p><em><strong>Edge node deployment finalized</strong></em></p></figcaption></figure>

{% hint style="warning" %}
⚠️ To prevent potential conflicts or interruptions, it is recommended to avoid performing other actions such as installing additional packages or modifying configurations on the server during the Edge Node deployment process.
{% endhint %}

### 7. Access your Edge node interface

Upon successful installation, the Edge Node user interface will be accessible at `http://<your-server-ip>/login`. Replace `<your-server-ip>` with the actual public IP address of your deployed server.

**Default login credentials:**

* Username: my\_edge\_node
* Password: edge\_node\_pass

### 8. Control and Manage Edge Node Services

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

## Need assistance?

In case any of the services show an 'Inactive' status, you can contact our developers for assistance. Please reach out via [Discord](https://discord.com/invite/xCaY7hvNwD) or email us at **tech@origin-trail.com**. \
Be sure to include the installation log file (`installation_process.log`), which can be found in the `/root/edge-node-installer/log/` directory.

