---
description: This page will guide you trough the V8 DKG Core Node installation process
---

# V8 DKG Core Node installation

The installation process involves interacting with the installer through the terminal. To proceed, you should have all the required inputs ready, as they will be required by the installer:

* Ubuntu 20.04, 22.04 or 24.04 instance
* Admin and operational keys and their private keys
* Funds on the wallets
* RPC endpoints
* Firewall configured

Detailed instructions for the above requirements are available [here](preparation-for-v8-dkg-core-node-deployment.md).

## 1. **How the installer works**:

{% hint style="info" %}
The provided installer is designed to install the OriginTrail node on **Ubuntu 20.04 LTS, 22.04 LTS and 24.04 LTS** distributions.\
\
It is also possible to install the OriginTrail node on other systems, but it would require modifications to the installer. If you have any such modifications in mind, we highly encourage your contributions. Please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

### **During the installation process, the OriginTrail node installer will execute the following actions:**

* Check for the Ubuntu OS version compatibility
* Install the required Node.js version together with NPM
* Deploy the OriginTrail node directory and install all required modules
* Configure and enable OriginTrail node service (as systemctl)
* Configure your nodes .origintrail\_noderc file based on the provided inputs:
  * Admin and operational keys,
  * Node shares token name and symbol
  * Operator fee (value between 0 - 100 based on your choice)
  * RPC endpoint&#x20;
* Install and enable MySQL service and create operationaldb for the node
* Configure MySQL user password for the OriginTrail node operational database (based on your inputs)
* Install and enable Triple store database

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Installer interaction</p></figcaption></figure>

### Installer video tutorial (slightly outdated):

Before proceeding, make sure to check our quick video tutorial, which explains the process of interacting with the installer.

{% embed url="https://www.youtube.com/watch?v=RZvIx27I8Ts" %}
V8 incentivized DKG Core Node deployment process
{% endembed %}

## 2. Download OriginTrail V8 DKG Core Node installer:

Ensure that you're logged in as root. Then, execute the following command in order to download the installer and grant it executable access:

```sh
cd /root/ && curl -k -o installer.sh https://raw.githubusercontent.com/OriginTrail/ot-node/v8/develop/installer/installer.sh && chmod +x installer.sh
```

## 3. Execute the installer by running:

```
./installer.sh
```

{% hint style="info" %}
Do not run the installer with "sudo".
{% endhint %}



## 4. Verify V8 DKG Core Node installation:

If your installation has been successful, your node will show the “**Node is up and running!**” log, as shown in the example image below:

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption><p>V8 DKG Core node successful initialization</p></figcaption></figure>

<mark style="color:green;">**`Congratulations, your V8 DKG Core Node is up and running!`**</mark>



### **Useful commands:**

**Starting your node:** `otnode-start` or `systemctl start otnode`

**Stopping the node:** `otnode-stop` or `systemctl stop otnode`

**Restarting the node:** `otnode-restart`  or `systemctl restart otnode`

**Showing node logs:** `otnode-logs`  or `journalctl -u otnode --output cat -fn 100`

**Opening the node config:** `otnode-config` or `nano /root/ot-node/.origintrail_noderc`



## Need help?

If you encounter any issues during the installation process or have questions regarding any of the above topics, jump into our official [Discord](https://discord.gg/xCaY7hvNwD) and ask for assistance.

Follow our official channels for updates:&#x20;

* [X](https://x.com/origin_trail)&#x20;
* [Medium](https://medium.com/origintrail)&#x20;
* [Telegram](https://t.me/origintrail)
