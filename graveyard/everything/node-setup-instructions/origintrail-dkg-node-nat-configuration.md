---
description: >-
  In the following section, we will go trough the steps required to configure
  your OriginTrail DKG node NAT, ensuring optimal libp2p communication and
  effective participation in the network.
---

# OriginTrail DKG node NAT configuration

## What is **Network Address Translation (**&#x4E;AT) and libp2p?

libp2p is a peer-to-peer (P2P) networking framework that enables the development of P2P applications. **OriginTrail's DKG node** utilizes libp2p for networking, enabling seamless communication within the OriginTrail decentralized network.&#x20;

**NAT (Network Address Translation)** poses a significant challenge for P2P networks like OriginTrail DKG. Devices behind NAT are typically not directly reachable from devices outside the local network due to the translation of private IP addresses to a single public IP address. This creates hurdles for libp2p-based applications, as direct communication between nodes becomes difficult or impossible.\
\
Configuring libp2p properly is essential regardless of the cloud provider you are using to run your OriginTrail DKG node. Without proper configuration, your nodes may encounter communication issues, hindering their ability to participate effectively in the OriginTrail DKG network. By addressing NAT traversal and ensuring proper exposure of public IP addresses, you can overcome these challenges and enable seamless communication between DKG nodes.

## How to configure your OriginTrail DKG node NAT?

By adding a few parameters to the node's configuration file `.origintrail_noderc`, you can ensure proper NAT traversal and optimal libp2p communication.

### **Step 1: Get the IP address of your OriginTrail node:**

Log in to your cloud provider's console and navigate to the dashboard or management interface for your instance. Find the public IP address of your instance. This is the IP address that other nodes will use to communicate with your OriginTrail node.

{% hint style="info" %}
Make sure that you have a static IP address assigned to OriginTrail node instance. \
Most cloud providers require you to reserve and associate the IP address to the instance.&#x20;
{% endhint %}

{% hint style="danger" %}
Assigning a static IP to your server is crucial to prevent network communication issues caused by IP address changes during server reboots.
{% endhint %}



### **Step 2: Update your OriginTrail DKG node configuration:**

Navigate to the directory of your OriginTrail node (ot-node), open your configuration (.origintrail\_node) file and configure your **"network"** module as shown below:\


```json
{
   "modules":{
      "blockchain":{
         "implementation":{
            <YOUR_BLOCKCHAIN_CONFIGURATION>
         }
      },
      "tripleStore":{
         "implementation":{
            <YOUR_TRIPPLE_STORE_CONFIGURATION>
         }
      },
      "network":{
         "implementation":{
            "libp2p-service":{
               "config":{
                  "nat":{
                     "enabled":true,
                     "externalIp":"<ORIGINTRAIL_NODE_PUBLIC_IP>"
                  }
               }
            }
         }
      }
   },
   "auth":{
      "ipWhitelist":[
         "::1",
         "127.0.0.1"
      ]
   }
}
```

### **Step 3: Restart you OriginTrail node:**

As we have previously learned, each update of the OriginTrail node configuration must be followed by the restart. Restart your node by running the following command:

```
systemctl restart otnode.service && journalctl -u otnode --output cat -f
```

or

```
otnode-restart && otnode-logs
```

and wait for your node to print the "Node is up and running!".&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-16 at 17.39.32.png" alt=""><figcaption><p>OriginTrail node started successfully</p></figcaption></figure>
