---
description: >-
  Configuration file (.origintrail_noderc) should be located in your "ot-node"
  directory. Inside of your .origintrail_noderc file you can configure certain
  parameters such as:
---

# DKG v6 node configuration

**"blockchainTitle":**\
Title of the blockchain your node will use.

****

**"networkId":**\
Network/Blockchain identity you wish your node to connect to.

****

**"rpcEndpoints":**\
Endpoint/URL which your node will use in order to communicate with blockchain. OriginTrail v6 Beta node is currently running on **Polygon Mumbai (testnet)** network**.**\
****Polygon Mumbai RPC: [https://matic-mumbai.chainstacklabs.com/](https://matic-mumbai.chainstacklabs.com/).

****

**"publicKey":**\
Operational wallet address which your node will use. At this time, it needs MATIC test tokens for **Polygon Mumbai (testnet)** so please make sure it is funded in order for your node to function properly.

****

**"graphDatabase":**\
Currently, OriginTrail v6 Beta node uses **Blazegraph** as graphDatabase for both dockerless and dockerized versions.

Please make sure that your **graphDatabase** section in configuration file is properly set as shown below.

```
"graphDatabase": {
    "implementation": "Blazegraph",
    "url": "http://localhost:9999/blazegraph",
    "username": "admin",
    "password": ""
},
```

****

**"networkId":**\
When you start your node for the first time, it will generate its network identity and populate the "network" block automatically. Leave it blank as shown in the example file at the end of this page. When the network identity for your node is generated, your configuration file will look as shown below:

```
"network": {
    "privateKey": "CAAS4AQwggJcAgEAAoGBAMM/4ShUnuFPxY..."
},
```

{% hint style="warning" %}
Do not remove or edit your network identity.
{% endhint %}



**"ipWhitelist":**\
Whitelist desired IP addresses here in order to access you node trough the API.&#x20;

```
"ipWhitelist":[
      "::1",
      "127.0.0.1",
      "..."
]
```

Please check the DKG v6 API documentation [here](https://docs.origintrail.io/dkg-v6-beta/dkg-v6-api).



OriginTrail v6 node configuration file example:

```
{
   "blockchain":[
      {
         "blockchainTitle":"Polygon",
         "networkId":"polygon::testnet",
         "rpcEndpoints":[
            "https://matic-mumbai.chainstacklabs.com/"
         ],
         "publicKey":"0x123123123...",
         "privateKey":"ec0e6c36bd88342..."
      }
   ],
   "graphDatabase": {
       "implementation": "Blazegraph",
       "url": "http://localhost:9999/blazegraph",
       "username": "admin",
       "password": ""
      },
   },
   "logLevel":"trace",
   "rpcPort":8900,
   "network":{
      
   },
   "ipWhitelist":[
      "::1",
      "127.0.0.1",
      "<whitelist_IP_here>"
   ]
}
```
