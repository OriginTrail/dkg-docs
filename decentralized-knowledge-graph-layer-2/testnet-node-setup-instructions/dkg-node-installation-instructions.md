# DKG Node installation instructions:

After acquiring TRAC and OTP tokens, teleporting TRAC to the OriginTrail Parachain network and mapping your wallets as per instructions provided above, you have all the pieces ready for the OriginTrail node installation process.

Currently the node can be run as a system process (Step 1). Follow the Discord channel announcements for availability of the Docker installation as well as cloud marketplace simple installers (such as the 1-click installer on DigitalOcean).

## 1. Setup instructions

Installation process will require the interaction with the installation script so please make sure that you have your wallet’s public and private keys ready.

### 1.1 - Login to the server as root. You cannot use sudo and run this script.

### 1.2 - Download one of the following installer scripts:

**Mainnet installer:**

```
cd /root/ && curl https://raw.githubusercontent.com/OriginTrail/ot-node/v6/release/mainnet/installer/installer.sh --output installer.sh && chmod +x installer.sh
```

#### **Testnet installer:**

```
cd /root/ && curl https://raw.githubusercontent.com/OriginTrail/ot-node/v6/release/testnet/installer/installer.sh --output installer.sh && chmod +x installer.sh
```

### 1.3 - **Firewall settings**:

OriginTrail node needs the following ports allowed in order to properly operate

* 8900 (your node API)
* 9000 (networking port for communication with other nodes)



{% hint style="warning" %}
The below provided installer script (_installer.sh_) will automatically enable UFW and open ports 22 (ssh), 8900 and 9000.\
\
If you're setting up the OriginTrail node in a cloud environment, please keep in mind that different cloud providers use different security practices when it comes to configuring firewalls on the servers. Make sure that enabling UFW will not cause any networking issues on your server or disable it upon installation is completed if you wish to configure firewall differently. &#x20;
{% endhint %}

### 1.4 - **Running the installer scripts**:

{% hint style="warning" %}
The provided installer script is designed for installing the OriginTrail node on **Ubuntu 20.04 LTS and 22.04 LTS** distributions.\
\
It is also possible to install the OriginTrail node on other systems but it would require  modifications to the installer script. If you have any such modifications in mind, we highly encourage your contributions so please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

#### **Both, mainnet and testnet:**

```
./installer.sh
```

If your installation has been successful, your node will show the “**Node is up and running!**” log as shown in the example image below:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-29 at 18.40.45.png" alt=""><figcaption><p>Example of a successfully installed node</p></figcaption></figure>

### **1.4 Setup finalization - setting the node stake and service ask parameters**

Once the OriginTrail node starts, **several blockchain transactions need to be executed for your node to become an active part of the network and start hosting the DKG Knowledge assets**. These transactions are needed to set the required TRAC stake for your node (50 000 TRAC at this time) and set the node service ask. Both values are set in TRAC tokens.

{% hint style="warning" %}
**50000** **TRAC** is the minimum amount of TRAC on the OriginTrail DKG Mainnet for your node to become eligble for DKG hosting and rewards. More information is available in the following OriginTrail [OT-RFC-14](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-14%20DKG%20v6%20TRAC%20Tokenomics.pdf).
{% endhint %}

\
You can set the node stake and ask settings in two ways. The first option is to use the Houston application and the second is to do it by running a few npm scripts directly on the server where your nodes is installed.

### Setting up node stake and service ask via Houston (Recommended):

[Houston](houston-origintrail-node-control-center.md) is the OriginTrail node user interface (command center) that allows you to execute certain operations regarding your node on the blockchain. There are two ways to run Houston:

1. Via a hosted application, which is available at the following link: [https://houston.origintrail.io/](https://houston.origintrail.io/) or
2. Run Houston Web application locally by following the setup [instructions](dkg-node-installation-instructions.md#setup-houston-locally).

More  information on Houston can be found [here](houston-origintrail-node-control-center.md)\
\
**Setting your node service ask**\
Navigate to the "Service tokenomics" page within the Houston application, enter the service ask amount, denominated in TRAC and click "Update ask" button. This will trigger the transaction signing process with Metamask.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-29 at 18.44.29.png" alt="" width="320"><figcaption><p>Node service ask setting interface</p></figcaption></figure>

**Staking TRAC to your node**

Navigate to the "Service tokenomics" section within Houston application, enter the stake amount in TRAC and click "Add stake" button. This will again trigger the transaction signing process with Metamask, this time requiring two transactions to complete the process of TRAC staking to your node.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-29 at 18.44.49.png" alt="" width="375"><figcaption><p>Node stake settings interface</p></figcaption></figure>

## <mark style="color:green;">Congratulations! You have just set up your OriginTrail DKG node!</mark>

### **OriginTrail node useful terminal commands (aliases):**

**Startting your node:** _otnode-start_&#x20;

**Stopping the node:** _otnode-stop_&#x20;

**Restarting the node:** _otnode-restart_&#x20;

**Showing node logs:** _otnode-logs_&#x20;

**Openning the node config:** _otnode-config_

###

### Alternative way of setting up STAKE and ASK via npm scripts (NOT recommended):

It is possible to use npm scripts to setup both node stake and service ask directly from the server where your node was installed, **however this process requires you to provide your node admin wallet key on the script.** We don't recommend using this process for obvious security implications. It is however practical in setting up nodes in development environments (see also [Development environment setup](../setting-up-your-development-environment.md)).

**Setting TRAC stake for your node:**

{% hint style="warning" %}
**Please make sure that you replace the public and private key values accordingly as well as the stake value before execution.**
{% endhint %}

Example command:&#x20;

```
npm run set-stake -- --rpcEndpoint=https://astrosat-parachain-rpc.origin-trail.network/ --stake=50000 --operationalWalletPrivateKey=0x92962c43dd7cb66d9d37c174388558eb57a722d33f65f91398a5a2714c36fdc4 --managementWalletPrivateKey=0x6f9a4cd2714f8a56950ad96742d2e6efcd0319a259a47cf56775c6d63e731e67 --hubContractAddress=0x5fA7916c48Fe6D5F1738d12Ad234b78c90B4cAdA 
```

**Set your node ask using the set-ask npm script:**&#x20;

{% hint style="warning" %}
This script should be run from the ot-node directory.
{% endhint %}

Example command:&#x20;

Note: Use the operational private key for "--private-key" parameter in set-ask script



If you have come this far and your node logs are not showing any errors, you're node is successfully set up!&#x20;

###

### **OriginTrail node commands:**

## Monitoring node operations & rewards

Over the course of time your node will provide different services to the DKG users as part of the DKG Service market (e.g. your node will receive requests from the network, such as requests to index assets or fetch their state). To be able to provide these services, your node needs to maintain assets (and their associated assertions) in their original form and occasionally provide proofs of utility to the blockchain. Therefore it is essential that you keep your node running with as high uptime as possible so it is able to answer requests and perform its activities. More details on the functioning of the service market and tokenomics behind it can be found in [OT-RFC-14](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-14%20DKG%20v6%20TRAC%20Tokenomics.pdf).

**It is essential that you familiarise yourself with the tokenomics of v6 and the services your node will be performing. A good understanding will be crucial for you to set up your node tokenomics settings in a way that you find optimal for your node.** The OriginTrail V6 service market is an open market and requires all OriginTrail Nodes to provide a public “service ask” amount in TRAC.

The OriginTrail V6 node also needs to maintain a constant connection to the blockchains it operates with via dedicated blockchain RPC endpoints (it supports multiple RPC endpoints for one blockchain, which allows for resiliency in case of RPC downtime).



