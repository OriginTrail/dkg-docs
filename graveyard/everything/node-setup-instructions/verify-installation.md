# Verify installation

If your installation has been successful, your node will show the “**Node is up and running!**” log as shown in the example image below:

<figure><img src="../../../.gitbook/assets/Screenshot 2023-05-29 at 18.40.45.png" alt=""><figcaption><p>Example of a successfully installed node</p></figcaption></figure>

## <mark style="color:green;">Congratulations! You have just set up your OriginTrail DKG node!</mark>

### **OriginTrail DKG node useful commands:**

**Starting your node:** _otnode-start_&#x20;

**Stopping the node:** _otnode-stop_&#x20;

**Restarting the node:** _otnode-restart_&#x20;

**Showing node logs:** _otnode-logs_&#x20;

**Opening the node config:** _otnode-config_

## Monitoring node operations & rewards

Over the course of time your node will provide different services to the DKG users as part of the DKG Service market (e.g. your node will receive requests from the network, such as requests to index assets or fetch their state). To be able to provide these services, your node needs to maintain assets (and their associated assertions) in their original form and occasionally provide proofs of utility to the blockchain. Therefore it is essential that you keep your node running with as high uptime as possible, so it is able to answer requests and perform its activities. More details on the functioning of the service market and tokenomics behind it can be found in [OT-RFC-14](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-14%20DKG%20v6%20TRAC%20Tokenomics.pdf).

**It is essential that you familiarise yourself with the tokenomics of v6 and the services your node will be performing. A good understanding will be crucial for you to set up your node tokenomics settings in a way that you find optimal for your node.** The OriginTrail V6 service market is an open market and requires all OriginTrail Nodes to provide a public “service ask” amount in TRAC.

The OriginTrail V6 node also needs to maintain a constant connection to the blockchains it operates with via dedicated blockchain RPC endpoints (it supports multiple RPC endpoints for one blockchain, which allows for resiliency in case of RPC downtime).
