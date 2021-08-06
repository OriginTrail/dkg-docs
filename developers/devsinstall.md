---
description: All you need to know about sharing your data via the DKG
---

# Publishing data to the DKG

### How is data shared in the Decentralized Knowledge Graph

Traditionally knowledge graphs ingest information from various sources using custom data pipelines for knowledge graph building. As an example, the Google knowledge graph is populated exclusively by Google software by ingesting information from from websites and other online resources.

In contrast to that, OriginTrail is a permissionless system, so **anybody can add data to the Decentralized Knowledge Graph** by publishing it on the network. This means that queries performed on the DKG will be executed on records from all participants, with several characteristics:

* each graph element has an associated, verifiable publisher identity \(DID\)
* each published dataset has a corresponding set of cryptographic proofs on a blockchain \(multiple are supported\), using which every graph element can be verified for integrity \(provenance from a particular dataset and immutability\)
* each dataset has a specified data lifespan \(and might be pruned on the network after it's expiry\)
* semantic data can be queried based on IRIs \(more in [Querying](querying.md) section\)

Another key differentiator of the DKG is that it is comprised of two "levels"

* public decentralized DKG as shared state
* private, node-specific KGs, connected with the DKG \(shareable by the data owner\)

Dapps can use just the public DKG, just private KG \(they can access\), or can use both synergistically. More information is available in the [querying](querying.md) section.

{% hint style="info" %}
This section assumes you have [set up your development environment](setting-up-development-environment.md).
{% endhint %}

### Publishing data using the DKG client library

The DKG client library is a wrapper around the node API, abstracting the details and making it easier to use the DKG. There are two ways to publish data to the DKG via the DKGclient - the simplest way is using _simplePrepare_, and the more robust way is following the import-publish scheme.

#### Using simplePrepare

```javascript
// first initialize connection to your DKG Node
dkg.init(OT_NODE_HOSTNAME,OT_NODE_PORT,false);


// prepare a simple dataset for publishing, containing one entity
const simpleDataset = dkg.simplePrepare({
    identifier_type: 'YOUR_TYPE', // e.g. DID, SGTIN, URL etc
    identifier_value: '12345',
    properties:{
        hello: 'world'
    }
});


// publishing a dataset
dkg.publish(simpleDataset).then((publish_result)=>{
    console.log(publish_result);
});
```

The above code will prepare a simple dataset comprised of a single object with an associated identifier, identifier type and some properties, and the _publish_ method will import & publish it via the DKG node. Make sure to initialize the connection to the dkg using the _init_ function first. To publish multiple objects, follow the next step

#### Without simplePrepare

Below is an example of a linked data OT-JSON serialization, with two objects and their defined relation in a @graph array. \(OT-JSON is an internal serialization format and is intended for protocol level communication, while specific standard data models such as RDF, GS1 EPCIS, JSON-LD are translated to it via _transpilers_\).

```javascript
const dataset = {
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



// publishing a dataset

dkg.publish(dataset).then((publish_result)=>{
    console.log(publish_result);
});
```

#### Using the direct node API

Publish the above dataset in two steps, by putting it in a _file.json._ First we use the _**import**_ API

```javascript
POST http://NODE_IP:PORT/api/latest/import
body {
 form-data {
  "file": "file.json"
  "standard_id": "GRAPH"
 }
}
```

As a response you will get a handler\_id. This will be used to inquire about operation execution on the OT node.

```javascript
{
  "handler_id": "a9102052-c9b1-4093-81d8-91f97685a9bf"
}
```

The import route ingests different _standard\_ids_, being a GRAPH in this example. Currently the following data models are supported:

| Standard | standard\_id |
| :--- | :--- |
| GS1 EPCIS 1.2 | GS1-EPCIS |
| W3C Web of Things | WOT |
| Generic OT-JSON serialization | GRAPH |

The import operation can last for some time, so to check for it's operational status, query the import result API

```javascript
GET http://NODE_IP:PORT/api/latest/import/result/{handler_id}
```

An example response would look like this

```javascript
{
  "data": {
    "data_hash": "0xea05797aa2de1f1e09fea368e5538664383a879186e22bfde6f39396b7599b1c",
    "dataset_id": "0x317a39f0c0bc7f24e4a27c53fca8d180156f0704351b4fd6454e981e1eb1b0a5",
    "import_time": 15869480,
    "otjson_size_in_bytes": 9915,
    "root_hash": "0x415c2b16c4ee7442161d0f1f05ccd41c71b4c770862491aec22297063fb68d8e"
  },
  "status": "PENDING"
}
```

The status field will be in _COMPLETED_ state when the import is done, otherwise it will be _PENDING_. Once import is complete, you can observe the dataset id, graph root hash, original input dataset hash, import time and size.

At this moment, the dataset has been ingested and processed by your node, which in this case is considered a DC node. To publish it on the network, use the _replicate_ route using the dataset id obtained from the import result call. 

{% hint style="info" %}
Note: publishing datasets on the network requires TRAC tokens, available on the desired blockchain. Please refer to supported blockchains and their associated identifiers \(such as _xdai:mainnet_\) in the [Developer reference](references.md).
{% endhint %}

```javascript
POST http://NODE_IP:PORT/api/latest/replicate
body{
 raw{
  "dataset_id": "0x317a39f0c0bc7f24e4a27c53fca8d180156f0704351b4fd6454e981e1eb1b0a5",
  "blockchain_id": "xdai:mainnet"
 }
}
```

In the same pattern, as this operation can last for some time on the network, we can query the current status by calling the replicate route with the corresponding handler\_id returned by the _replicate_ API response:

```javascript
GET http://NODE_IP:PORT/api/latest/replicate/{handler_id}
```

Note that importing and replication can be done separately and at different times.

### What kinds of datasets can be published?

The node application layer envisions support for multiple data conversion services \(transpilers\), which enable anyone to create a converter and share it in an interoperable way with the rest of the network. New data models are expected to be added over time to help share multi-modal data through a shared, verifiable graph interface. More information on how to create converters will be available in a specific section.

### How do my published datasets get stored on the ODN?

Publishing a dataset creates a network data holding offer on the ODN and the node will start a negotiation process with other nodes using the protocol’s incentivized replication procedure. If the replication fails to be completed for any reason, the data field in the replication result call will contain an appropriate error message, and the status field will have the value “FAILED”. Once when replication process is complete the ODN offer details are written on the blockchain.

### How about private data?

The ODN is designed to support private \(non-replicated\) graph data, connected with the public DKG. In this way the DKG enables data that cannot be shared publicly to be part of the same global graph and accessible at the discretion of the data owner. At this point in time, it is possible to add permissioned data as a property object in the OT-JSON graph objects, by including a _permissioned\_data_ property as indicated below. Permissioned data trading and monetization features are currently in development, with support for blockchain purchase verification by implementing the [FairSwap](https://eprint.iacr.org/2018/740.pdf) blockchain protocol.

```javascript
{
  "@graph":[
    {
      "@id": "id",
      "@type": "otObject",
      "identifiers":[
        {
          "@type": "id",
          "@value": "some_value"
        }
      ],
      "properties":{
        "foo": "bar",
        "permissioned_data":{
          "data":
          {
            "key1": "value1",
            "key2": "value2"
          }
        }
      },
      "relations":[]
    }
  ]
}
```

The upcoming v6 update will extend the permissioning options to whole subgraphs and RDF triples.

### 

### What are connectors?

Connectors are a special type of vertex in the graph that enable traversing data from different data creators within a single trail request.

When creating a connector it is required to specify a connection identifier and the ERC-725 identity address of the data creator for whom the connection is intended.

If the connector vertices have matching identifiers, and the connector vertices were created by the corresponding dataset creators \(which is determined by the dataset creator’s identity address\), an additional set of two “connector” graph edges is created to enable a cryptographically verifiable connection between the two respective subgraphs.

Note that the connection between two connector vertices will only be created if both data creators specified the other’s ERC-725 node identity in the connector

> **Example:** Data creator Alice replicates a dataset containing a connector CONN1 designated for a data creator Bob. When Bob adds a dataset containing a connector CONN1 designated for Alice to the local knowledge graph, a pair of edges \(one for each direction\) with relation type `CONNECTION_DOWNSTREAM` will be created between two connector vertices.

For specific information on how to create connectors depending on the data standard, see [Data Structure Guidelines](data-structure-guidelines.md)



