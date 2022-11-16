# DKG Node installation instructions:

After acquiring TRAC and OTP tokens, teleporting TRAC to the OriginTrail Parachain network and mapping your wallets as per instructions provided above, you have all the pieces ready for the OriginTrail node installation process.

Currently the node can be run as a system process (Step 1). Follow the Discord channel announcements for availability of the Docker installation as well as cloud marketplace simple installers (such as the 1-click installer on DigitalOcean).



## 1. Setup instructions (Dockerless)

Dockerless installation will only require the interaction with the installation script so please make sure that you have your wallet’s public and private keys ready.

### 1.1 - Login to the server as root. You cannot use sudo and run this script.

### 1.2 - Download one of the following installer scripts:

#### ****

**Mainnet installer:**

```
Coming soon…
```

#### **Testnet installer:**

```
cd /root/ && curl https://raw.githubusercontent.com/OriginTrail/ot-node/v6/release/testnet/installer/installer.sh --output installer.sh && chmod +x installer.sh
```

### 1.3 - **Running the installer scripts**:

#### **Mainnet:**

```
Coming soon…
```

#### **Testnet:**

```
./installer.sh
```

If your installation has been successful, your node will show the “**Node is up and running!**” log as shown in the example image below:

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-16 at 18.29.58.png" alt=""><figcaption><p>OriginTrail V6 node stated</p></figcaption></figure>

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



