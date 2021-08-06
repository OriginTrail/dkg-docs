---
description: >-
  Get familiar with the basic functionalities of the new OriginTrail
  Decentralized Network v4 (Freedom-Gemini) client.
---

# Hello Trail tutorial

Welcome to the introductory tutorial on utilizing the OriginTrail Decentralized Network v4 \(Freedom-Gemini\) client in your applications! This is the first in an array of guides and tutorials for application developers and system integrators on how to use the functionalities of the ODN to empower your supply chain applications with the ODN Trusted Knowledge Graph.

We will begin in the spirit of the usual developer learning experience with a “_Hello World”_ example. However, since we are talking about the ODN, the more appropriate name is “_**Hello Trail.”**_ You will learn **how to import data to your node, publish the dataset on the network** and get the referenced object’s history via your OriginTrail Node.

## OriginTrail 101 <a id="0ee8"></a>

OriginTrail is a neutral, open-source protocol built to establish high interoperability, interconnectivity and trust in data sharing between supply chain IT systems. It can be observed as a layer 2 data interoperability network which operates in conjunction with the L1 blockchain.

It is designed to take the load of storing and exchanging large datasets for supply chain applications off the L1 networks, thus lowering the cost \(at the moment of writing this tutorial, storing 1kB of data on Ethereum mainnet would cost roughly $1\) and enabling database-grade features for linked data in a decentralized manner. For this purpose, the OriginTrail protocol utilizes a specific data replication mechanism with the goal of building a _privacy-first decentralized knowledge graph_, effectively bypassing the constraints of underlying blockchain networks imposed by the nature of consensus mechanisms. The blockchain is therefore utilized for dataset fingerprinting and maintaining the necessary game-theoretical mechanisms within the OriginTrail Decentralized Network \(ODN\). Because of this design, OriginTrail is being used today in production with Ethereum at the current scale of roughly 15 TPS.

To learn more about how OriginTrail operates, check out the [OriginTrail technology page](https://tech.origintrail.io/protocol), ask questions in the community [Discord](https://discordapp.com/invite/FCgYk2S) group, check out the core development team’s [blog](https://medium.com/origintrail) and engage in the [official project Github repository](https://github.com/OriginTrail/ot-node).

## Prerequisites to Get Started <a id="2d12"></a>

In order to successfully complete this tutorial, you **will need to set up an OriginTrail node client**. We recommend you start by running an OriginTrail testnet node, which you can run in both a local environment \(i.e. your laptop\) and a VPS. Detailed instructions on how to set up a node can be found here: [https://tech.origintrail.io/node-setup-testnet](https://tech.origintrail.io/node-setup-testnet).

## Publishing & Viewing a Dataset <a id="2441"></a>

Let’s introduce a basic dataset:

```text
{
  "@graph": [
    {
      "@id": "SOME_OBJECT_IDENTIFIER",
      "@type": "otObject",
      "identifiers": [
        {
          "@type": "id",
          "@value": "SOME_OBJECT_IDENTIFIER"
        }
      ],
      "properties": {},
      "relations": []
    },
    {
      "@id": "OBJECT_DESCRIPTION_ID",
      "@type": "otObject",
      "identifiers": [
        {
          "@type": "OBJECT_DESCRIPTION_IDENTIFIER",
          "@value": "OBJECT_DESCRIPTION_ID"
        }
      ],
      "properties": {
        "message": "Hello trail!",
        "another_key": "This is another value"
      },
      "relations": [
        {
          "@type": "otRelation",
          "relationType": "IDENTIFIED_BY",
          "linkedObject": {
            "@id": "SOME_OBJECT_IDENTIFIER"
          },
          "direction": "direct"
        }
      ]
    }
  ]
}
```

This is a generic graph dataset supported natively by the OriginTrail node client, which describes two linked _otObjects,_ one representing an **identifier** \(i.e. a standardized supply chain identifier such as a GS1 barcode or datamatrix\), and the other presenting associated metadata, in this case containing the message _“Hello trail”_. In a specific supply chain use case, this would be information on specific supply chain events, business locations and electronic product codes.

OriginTrail supports a multitude of data models \(i.e. supply chain standards such as G1 EPCIS, CBV etc, the W3C Web of Things data model etc\), with extensible support due to the flexible native OT-JSON data model supported by the protocol, based on JSON-LD. For the purposes of this tutorial, it is important to understand that we are working with two linked objects, one being identified by the other in a very simple graph structure.

To introduce this dataset to the network, we first need to **import** it to the node using the import command. This command initiates the import process and returns an internally-generated handler ID, which is a UUID. Using this handler ID, you can check the status of the import process, which can take a certain amount of time, depending on the file size.

```text
POST http://NODE_IP:PORT/api/latest/importbody {
 form-data {
  file: file.json
  standard_id: GRAPH
 }
}
```

To check the status of the initiated import, make the following request to your node API:

```text
GET http://NODE_IP:PORT/api/latest/import/result/{handler_id}
```

Once the import is completed, the node will return the specific _**dataset ID**_, graph _**root hash**_, _**data size**_ and other useful values related to the dataset. When a file has been imported, the status will be _COMPLETED_. Before that, it will be _PENDING_.

Finally, to replicate the imported dataset on the network, trigger the replication process by calling the replicate API call. With this command, you will initiate an offer on the OriginTrail network and your node will start negotiating with other nodes on the replication procedure.

```text
POST http://NODE_IP:PORT/api/latest/replicatebody{
 raw{
  dataset_id: "0x34c4de6905954fc9706e9dd0177d60dc22ab6775ed72d91965b28d149dc773da",
 }
}
```

The replication process includes several steps which we will go deeper into in the following tutorials. For now it is important that you wait for it to finish and to verify that it has been completed. To do that, use the handler\_id returned by the replicate call and call:

```text
GET http://NODE_IP:PORT/api/latest/replicate/{handler_id}
```

The replication process can last for several minutes and is determined by the _dc\_choose\_time_ setting in the node configuration file \(more information on the settings can be found in the [node documentation](http://docs.origintrail.io/)\). The process involves fingerprinting the dataset on the Ethereum blockchain \(immutably writing its graph merkle root hash\) and incentivising the data holder \(DH\) nodes for storing the dataset in their local storage \(depending on the network size, a large portion of the network is expected to opportunistically store the dataset due to potential future incentivisation\).

## Reading the Data from Your Node <a id="bf74"></a>

To get back the data regarding the specific “trail” of the object you are observing in the supply chain — in this case with the ID “_SOME\_OBJECT\_IDENTIFIER” —_ we will use the Trail API. It will traverse the object graph based on specific criteria \(depth and connection types\). When the graph traversal is completed, the call will return an array of OT-JSON objects.

```text
POST http://NODE_IP:PORT/api/latest/trail
 body
 {
  raw 
  {
   {
    "identifier_types": ["id"],
    "identifier_values": ["SOME_OBJECT_IDENTIFIER"],
    "depth": 10,
    "connection_types": []
   }
 }
}
```

Use this call to determine the historical graph of the object in the node database. In a real-life supply chain use case, the Trail call will return the whole **“trail of events”** that have been published on the network regarding this specific object, regardless of the number of parties “mentioning” this object in their datasets. Once the amount of exchanged datasets about this specific object in the supply chain grows \(a typical scenario would be multiple companies sharing data over the network\) more information about this object will be returned by the trail call. It additionally allows further specifications such as specific knowledge graph traversal criteria, which we will go deeper into in future tutorials.

The Trail call deserves its own detailed tutorial as it involves several topics around proving dataset integrity, issuer identity and valid connections in the trail response, all of which will be explained in the coming tutorials in greater depth.

An example response for the trail call in this case would be:

```text
[
    {
        "datasets": [
            "0x34c4de6905954fc9706e9dd0177d60dc22ab6775ed72d91965b28d149dc773da"
        ],
        "otObject": {
            "@id": "SOME_OBJECT_IDENTIFIER",
            "@type": "otObject",
            "identifiers": [
                {
                    "@type": "id",
                    "@value": "SOME_OBJECT_IDENTIFIER"
                }
            ],
            "properties": {},
            "relations": []
        }
    },
    {
        "datasets": [
            "0x34c4de6905954fc9706e9dd0177d60dc22ab6775ed72d91965b28d149dc773da"
        ],
        "otObject": {
            "@id": "OBJECT_DESCRIPTION_ID",
            "@type": "otObject",
            "identifiers": [
                {
                    "@type": "OBJECT_DESCRIPTION_IDENTIFIER",
                    "@value": "OBJECT_DESCRIPTION_ID"
                }
            ],
            "properties": {
                "another_key": "This is another value",
                "message": "Hello trail!"
            },
            "relations": [
                {
                    "@type": "otRelation",
                    "direction": "direct",
                    "linkedObject": {
                        "@id": "SOME_OBJECT_IDENTIFIER"
                    },
                    "relationType": "IDENTIFIED_BY"
                }
            ]
        }
    }
]
```

Congratulations! You have now learned to perform the basic I/O operations on your OriginTrail node. In the coming weeks, we will publish further tutorials on how to discover objects and look up datasets over the network, check their integrity and work with the historical trail of supply chain objects spanning multiple datasets.

Expect more tutorials on how to use the OT node in the future. For the main OriginTrail documentation, please see [https://docs.origintrail.io](https://docs.origintrail.io/).

If any questions came up for you during the tutorial or you would like to share your opinion, the best place to start is by discussing it with our tech community on the [OriginTrail Discord server](https://discord.gg/FCgYk2S?source=post_page---------------------------).  


