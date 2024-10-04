# DKG node installation

After preparing all the requirements for running your OriginTrail DKG node which includes wallets, tokens and RPC endpoints, you are now ready to start the installer and launch your OriginTrail DKG node.

At this stage, there are two approaches when it comes to deploying the OriginTrail DKG node:

1. Downloading and running the installer (instructions provided below)
2. DigitalOcean 1-click deployment (available on DigitalOcean marketplace)
   * Mainnet 1-click deployment: Currently unavailable (Coming soon)
   * Testnet 1-click deployment: Currently unavailable (Coming soon)

{% hint style="info" %}
Make sure that you follow our communication channels closely for all the updates regarding additional options of launching and running the OriginTrail DKG node.
{% endhint %}

## 1. Running the installer (installation script)

{% hint style="info" %}
By executing this installer your node will be deployed as a Linux system service (systemctl process). &#x20;
{% endhint %}

The installation process will require interaction with the installer script via the terminal. Please ensure that you have all the necessary requirements for the node ready to be inserted into the prompt before running the installer.&#x20;

* Wallets and their private keys
* Funds on the wallets
* RPC endpoint

{% hint style="info" %}
In order to avoid any installation issues, please run the installer on a clean Ubuntu 20.04 or 22.04 server.
{% endhint %}

## 1.1 - Download OriginTrail DKG node installer:

Ensure that you're logged in as root. Then, execute the following command in order to download the installation script and grant it executable access:

```
cd /root/ && curl -k -o installer.sh https://raw.githubusercontent.com/OriginTrail/ot-node/v6/develop/installer/installer.sh && chmod +x installer.sh
```

### 1.2 - **Firewall configuration**:

OriginTrail node needs the following ports to be opened in order to properly operate.

* 8900 (default node API endpoint)
* 9000 (networking port for communication with other nodes)

{% hint style="warning" %}
Installer will automatically enable UFW and open ports 22 (ssh), 8900 and 9000.\
\
Please keep in mind that different cloud providers use different security practices when it comes to configuring firewalls on the servers. \
Make sure that enabling UFW will not cause any networking issues on your server or disable it after the installation process is completed if you wish to configure firewall settings differently (ex. via cloud provider's console). &#x20;
{% endhint %}

### 1.3 - **Running the installer script**:

{% hint style="info" %}
The provided installer script is designed for installing the OriginTrail node on **Ubuntu 20.04 LTS and 22.04 LTS** distributions.\
\
It is also possible to install the OriginTrail node on other systems, but it would require  modifications to the installer script. If you have any such modifications in mind, we highly encourage your contributions. Please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

#### **During the installation process, OriginTrail node installer will execute the following actions:**

* Check for the Ubuntu OS version compatibility
* Deploy OriginTrail node directory and install all required modules
* Configure and enable OriginTrail node service
* Enable and configure UFW (firewall)
* Install required Node.js version together with NPM
* Install and enable MySQL service
* Configure MySQL user password for the OriginTrail node operational database (based on your inputs)
* Install and enable BlazeGraph service (Graph database)

{% hint style="warning" %}
Do not run the installer with "sudo".
{% endhint %}

#### Execute the installer by running:

```
./installer.sh
```
