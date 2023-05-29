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

### 1.3 - **Firewall**:

OriginTrail node needs the following ports allowed in order to properly operate:

* 8900 (API)
* 9000 (Libp2p)

**This installer will enable UFW and open ports 22 (ssh), 8900 and 9000.**&#x20;

{% hint style="warning" %}
Different cloud providers use different best practices when it comes to configuring firewall on the servers. Make sure that enabling UFW will not cause any networking issues on your server or disable it upon installation is completed if you wish to configure firewall differently. &#x20;
{% endhint %}

### 1.4 - **Running the installer scripts**:

#### **Both, mainnet and testnet:**

```
./installer.sh
```

If your installation has been successful, your node will show the “**Node is up and running!**” log as shown in the example image below:

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-16 at 18.29.58.png" alt=""><figcaption><p>OriginTrail V6 node stated</p></figcaption></figure>

### **1.4 Setting the stake and ask**

Once the node starts, **you will need to execute two setup transactions for your node to become active**. We have prepared two scripts that are used from the command line (but both these transactions will be executable with a click of a button from Houston very soon). These two transactions are needed to set stake for your node (50 000 TRAC as minimum for the node to operate) and set the node ask (in TRAC tokens).

Set your node stake using the **set-stake** npm script (run from ot-node folder):&#x20;

```
npm run set-stake -- --rpcEndpoint=<rpc_enpoint> --stake=<stake_in_TRAC> --operationalWalletPrivateKey=<private_key> --managementWalletPrivateKey=<private_key> --hubContractAddress=<hub_contract_address> 
```

Example for mainnet:&#x20;

{% hint style="warning" %}
**50000** **TRAC** is the default value for stake, even though node-runners are free to change this value. 50000 is the minimum required for node to become active, but when Delegated Staking will go live, delegations will also be summed up.
{% endhint %}

```
npm run set-stake -- --rpcEndpoint=https://astrosat-parachain-rpc.origin-trail.network/ --stake=50000 --operationalWalletPrivateKey=0x92962c43dd7cb66d9d37c174388558eb57a722d33f65f91398a5a2714c36fdc4 --managementWalletPrivateKey=0x6f9a4cd2714f8a56950ad96742d2e6efcd0319a259a47cf56775c6d63e731e67 --hubContractAddress=0x5fA7916c48Fe6D5F1738d12Ad234b78c90B4cAdA 
```

Set your node ask using the **set-ask** npm script (run from ot-node folder):&#x20;

```
npm run set-ask -- --rpcEndpoint=<rpc_enpoint> --ask=<ask_in_kb_per_epoch_in_TRAC> --privateKey=<operational_wallet_private_key> --hubContractAddress=<hub_contract_address>
```

Example for mainnet:&#x20;

{% hint style="warning" %}
**0.00375 $TRAC / (KB \* epoch)** is the default value on the Trace Labs nodes, even though node-runners are free to choose any other value.
{% endhint %}

```
npm run set-ask -- --rpcEndpoint=https://astrosat-parachain-rpc.origin-trail.network/ --ask=0.00375 --privateKey=0x6f9a4cd2714f8a56950ad96742d2e6efcd0319a259a47cf56775c6d63e731e67 --hubContractAddress=0x5fA7916c48Fe6D5F1738d12Ad234b78c90B4cAdA 
```

Note: Use the operational private key for "--private-key" parameter in set-ask script

### **OriginTrail node commands:**

**Start node:** _otnode-start_&#x20;

**Stop node:** _otnode-stop_&#x20;

**Restart node:** _otnode-restart_&#x20;

**Show node logs:** _otnode-logs_&#x20;

**Open node configuration:** _otnode-config_

## Monitoring node operations & rewards

Over the course of time your node will provide different services to the DKG users as part of the DKG Service market (e.g. your node will receive requests from the network, such as requests to index assets or fetch their state). To be able to provide these services, your node needs to maintain assets (and their associated assertions) in their original form and occasionally provide proofs of utility to the blockchain. Therefore it is essential that you keep your node running with as high uptime as possible so it is able to answer requests and perform its activities. More details on the functioning of the service market and tokenomics behind it can be found in [OT-RFC-14](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-14%20DKG%20v6%20TRAC%20Tokenomics.pdf).

**It is essential that you familiarise yourself with the tokenomics of v6 and the services your node will be performing. A good understanding will be crucial for you to set up your node tokenomics settings in a way that you find optimal for your node.** The OriginTrail V6 service market is an open market and requires all OriginTrail Nodes to provide a public “service ask” amount in TRAC.

The OriginTrail V6 node also needs to maintain a constant connection to the blockchains it operates with via dedicated blockchain RPC endpoints (it supports multiple RPC endpoints for one blockchain, which allows for resiliency in case of RPC downtime).



