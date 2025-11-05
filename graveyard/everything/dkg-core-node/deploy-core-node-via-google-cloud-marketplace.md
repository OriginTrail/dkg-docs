---
hidden: true
---

# Deploy Core node via Google Cloud marketplace

### Core Node deployment process overview

This deployment method allows you to fully configure your Coore Node by filling out a solution form provided through the Google Cloud Marketplace. During the process, you’ll be guided through each required field and configure the following:

1. Core node names for each supported blockchain
2. Core Node wallet keys

{% hint style="success" %}
Ensure you have a Google Cloud account with billing enabled and permissions to deploy Marketplace solutions.
{% endhint %}

## **Core node** deployment preparation

{% hint style="success" %}
With these requirements prepared, you'll be ready to quickly populate the required form inputs and proceed with the deployment of your Core node.
{% endhint %}

**1. Core Node keys (wallets):**

The Core Node requires two types of keys:

* Management keys
* Operational keys

It is assumed that you are familiar with the wallet preparation process for each supported blockchain. If not, please check the following section related to funding of keys in [Preparation of DKG Core node deployment](run-a-v8-core-node-on-testnet/preparation-for-v8-dkg-core-node-deployment.md#id-3.-funding-your-keys) on testnet.

{% hint style="success" %}
If you're deploying on **mainnet**, ensure that:

* You have access to TRAC tokens on the blockchains where you intend to deploy your Edge Node
* You understand how to bridge TRAC tokens to **Gnosis** or **Base**, or use **Teleport** to transfer them to **NeuroWeb**.
* Your operational and management keys are properly funded with both TRAC and the native token, depending on the blockchain to which you are deploying your node.
{% endhint %}

**Useful documentation:**

* A list of exchanges where TRAC tokens can be acquired is available on our [official website](https://origintrail.io/get-started/trac-token).
* TRAC Teleport to Neuroweb is explained [here](../teleport-instructions-neuroweb.md).
* Bridging TRAC to Base is explained [here](../../../dkg-knowledge-hub/learn-more/connected-blockchains/base-blockchain/#bridging-trac-to-base).
* Bridging TRAC to Gnosis is explained [here](../../../dkg-knowledge-hub/learn-more/connected-blockchains/gnosis-chain/#bridging-trac-to-gnosis).
* Neuroweb mainnet explorer is available [here](https://neuroweb.subscan.io/).
* Neuroweb testnet explorer is available [here](https://neuroweb-testnet.subscan.io/).
* Base Sepolia explorer is available [here](https://sepolia.basescan.org/).
* Base mainnet explorer is available [here](https://basescan.org/).
* Gnosis Chiado explorer is available [here](https://gnosis-chiado.blockscout.com/).
* Gnosis mainnet explorer is available [here](https://gnosisscan.io/).\


## Deployment guide (step by step)

With all prerequisites in place, you can proceed to populate the required form inputs and deploy your Core Node by following the steps below.

### **1. Log in to Google Cloud Console**

Access your [Google Cloud Console](https://console.cloud.google.com/) using your credentials.

### **2. Navigate to the Marketplace**

In the main menu, go to **Marketplace**, then search for **"OriginTrail node"** in the search bar

### **3. Configure Virtual Machine Parameters:**

* Choose your desired deployment region,&#x20;
* Machine type,&#x20;
* Disk size and other instance-related options

{% hint style="info" %}
The deployment page comes with recommended machine type and storage options preselected for optimal Edge node performance. For Core node deployments, you can start with reduced hardware, **4GB RAM** and **2 CPU** cores, which is the bare minimum suitable for handling regular or minor workloads. \
You can scale up the resources later if needed.
{% endhint %}

### **4. Configure your Core node**

You can now proceed with populating the form and prepare for the deployment of your Core node.

**4.1 - Deployment mode**

{% hint style="success" %}
This field determines how the Edge Node services are managed after installation. Since we are focusing on deploying a Core node, leave it set to **"production"** mode, which is the default.
{% endhint %}

**4.2 - Blockchain environment**

Choose between **`mainnet`** or **`testnet`**. Ensure that your Core Node wallets are properly funded according to the blockchain environment where you intend to deploy your node.\


**4.3 - Core node configuration (ot-node service)**

This section allows you to configure your node’s name for each supported blockchain, as well as define the management and operational keys (wallets).

* **Node Name**: You can configure the **same node name** for all supported blockchains. This name will help identify your node across all chains.
* **Management wallet (Public EVM key)**: This key grants administrative control, enabling you to configure parameters such as ASK, operator fees, and other settings.\
  You can use the **same management key** across all supported blockchains and this key should funded with the **native token** of each respective blockchain in order to be able to perform updates.
* **Operational wallet (Public EVM key)**: This key is used by the node to perform various blockchain operations.
* **Operational wallet (Private EVM key):** Your operational wallet's private key\
  **Note**: The operational keys **must be different** for each blockchain.

{% hint style="warning" %}
- Inputs for at least one blockchain configuration must be populated (NeuroWeb, Base, or Gnosis) for the successful deployment of the Core Node.
- If the operational keys are not funded with the native token on the blockchain of choice, node will fail to create its blockchain profile.
- The management and operational keys require a small amount of the native token, NEURO for Neuroweb, ETH for Base, and xDAI for Gnosis, depending on the blockchain you prepare them for.
{% endhint %}

**4.4 - MySQL password**

During the deployment process, the password you provide in this field will be set as the **root password** for the MySQL database installed on your Core Node server.&#x20;

{% hint style="info" %}
🔐 This root password is critical for accessing and managing your Core node’s database. Do not share it or lose it.
{% endhint %}

### 5. Deployment

Once all parameters have been filled out correctly in the form, you can proceed with deploying your Core Node.&#x20;

{% hint style="success" %}
Static IP address will be assigned to your server automatically and the firewall will be configured as required by the setup.
{% endhint %}

Your Core Node installation will be located at:\
`~/edge_node/ot-node/`

### 6. Monitor the deployment process

The Google Cloud Marketplace deployment is generally oriented toward **DKG Edge Node** setups, with the **Core Node** being one of its components. As a result, the deployment process will install **all Edge Node components by default**, which may take approximately **20–30 minutes** to complete. However, the server will become available for **SSH access within a few minutes** after the deployment.

To monitor the installation progress, SSH into your server, `cd` into the **edge-node-installer** directory and run the following command:

```shell
bash service-status.sh
```

While services are still being installed, a loading spinner will be shown for each one (as shown on the image below).

<figure><img src="../../../.gitbook/assets/Screenshot 2025-05-09 at 14.38.38.png" alt=""><figcaption><p><em><strong>Installation in progress</strong></em></p></figcaption></figure>

When all services are marked as **"Active"**, this confirms that the **installation process has been finalized**.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-05-09 at 14.39.57.png" alt=""><figcaption><p><em><strong>Edge node deployment finalized</strong></em></p></figcaption></figure>

Since you are planning to run only the **Core Node (`otnode`)**, the following **Edge Node services are not required**. Once the installation is completed, make sure to **stop and disable the following Edge Node services** using the commands provided below:

{% hint style="danger" %}
Do not disable or stop any services during the installation process but only after the successful finalization of the setup.&#x20;
{% endhint %}

```sh
systemctl stop edge-node-api && systemctl disable edge-node-api 
systemctl stop auth-service.service && systemctl disable auth-service.service
systemctl stop ka-mining-api.service && systemctl disable ka-mining-api.service
systemctl stop drag-api.service && systemctl disable drag-api.service
systemctl stop airflow-webserver && systemctl disable airflow-webserver
systemctl stop airflow-scheduler && systemctl disable airflow-scheduler    
```

{% hint style="success" %}
Installed Edge Node components will not interfere with or affect your Core Node's performance in any way once they are stopped and disabled.
{% endhint %}

{% hint style="warning" %}
⚠️ To prevent potential conflicts or interruptions, it is recommended to avoid performing other actions such as installing additional packages or modifying configurations on the server during the Edge Node deployment process.
{% endhint %}

### 8. Control and Manage Core Node Service

Core node will be deployed and ran as `systemd` unit on your instance, making it easy to manage.

#### Managing Core node service:

For each service, you can perform the following actions using the respective systemd commands:

* **Check service status:** `systemctl status otnode.service`
* **Start a service (if it is not already running):** `systemctl start otnode.service`
* **Stop a service:** `systemctl stop otnode.service`
* **Restart a service:** `systemctl restart otnode.service`
* **View Service Logs:** `journalctl -f -u otnode.service`

## Need assistance?

In case any of the services show an 'Inactive' status, you can contact our developers for assistance. Please reach out via [Discord](https://discord.com/invite/xCaY7hvNwD) or email us at **tech@origin-trail.com**. \
Be sure to include the installation log file (`installation_process.log`), which can be found in the `/root/edge-node-installer/log/` directory.
