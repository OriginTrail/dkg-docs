---
description: Python library for interacting with the Decentralized Knowledge Graph.
---

# DKG Python SDK (dkg.py)

If you are looking to build applications leveraging [knowledge assets](broken-reference) on the OriginTrail Decentralized Knowledge Graph (DKG), the dkg.py library is the best place to start!

The DKG SDK is used together with an **OriginTrail gateway node** to build applications that interface with the OriginTrail Decentralized Network (the node is a dependency). Therefore you either need to run a gateway node on [your local environment](../setting-up-your-development-environment.md) or a [hosted OT-Node](../../v8-dkg-core-node/run-a-v8-core-node-on-testnet/), in order to use the SDK.

### Installation

The library can be used in any Python application.

Run the command to install dkg.py library using pip:

```bash
pip install dkg==8.0.0a3
```

pip x:

```bash
pipx install dkg==8.0.0a3
```

or poetry:

```bash
poetry add dkg==8.0.0a3
```

Then import DKG, BlockchainProvider and NodeHTTPProvider classes inside your project:

```python
from dkg import DKG
from dkg.providers import BlockchainProvider, NodeHTTPProvider
```

### :snowboarder:Quickstart

To use the DKG library, you need to connect to a running local or remote OT-Node.&#x20;

```python
node_provider = NodeHTTPProvider(endpoint_uri="http://localhost:8900", api_version="v1")
blockchain_provider = BlockchainProvider(
    Environments.DEVELOPMENT.value, # or TESTNET, MAINNET
    BlockchainIds.HARDHAT_1.value,
)

dkg = DKG(node_provider, blockchain_provider)

print(dkg.node.info)
# if successfully connected, this should print the dictionary with node version
# { "version": "8.X.X" }
```

{% hint style="warning" %}
Make sure to create an .env file and add PRIVATE\_KEY variable to it so that the blockchain provider can pick it up.
{% endhint %}

The system supports multiple blockchain networks, which can be configured using the `BlockchainIds` constants. You can select the desired blockchain by specifying the corresponding constant. The available options are:

DKG mainnet options:

* Base: base:8453
* Gnosis: gnosis:100
* Neuroweb: otp:2043

DKG testnet options:

* Base: base:84532
* Gnosis: gnosis:10200
* Neuroweb: otp:20430

DKG devnet options:

* Base: base:84532
* Gnosis: gnosis:10200
* Neuroweb: otp:2160

Local options:

* Hardhat1: hardhat1:31337
* Hardhat2: hardhat2:31337

#### Create a Knowledge Asset

In this example, let’s create an example Knowledge Asset representing a city. The content contains both public and private assertions. Public assertions will be exposed publicly (replicated to other nodes) while private ones won't (stays on the node you published to only). If you have access to the particular node that has the data when you search for it using get or query you will see both public and private assertions.&#x20;

```python
const content = {
     public: {
            '@context': 'http://schema.org',
            '@id': 'https://en.wikipedia.org/wiki/New_York_City',
            '@type': 'City',
            name: 'New York',
            state: 'New York',
            population: '8,336,817',
            area: '468.9 sq mi',
     },
     private: {
        '@context': 'http://schema.org',
        '@id': 'https://en.wikipedia.org/wiki/New_York_City',
        '@type': 'CityPrivateData',
        crimeRate: 'Low',
        averageIncome: '$63,998',
        infrastructureScore: '8.5',
        relatedCities: [
            { '@id': 'urn:us-cities:info:los-angeles', name: 'Los Angeles' },
            { '@id': 'urn:us-cities:info:chicago', name: 'Chicago' },
        ],
     },
}
```

When you create the knowledge asset, the above JSON-LD object will be converted into an **assertion**. When an assertion with public data is prepared, we can create an knowledge asset on DKG. `epochs_number` specifies for how many epochs the asset should be kept (an epoch is equal to three months).

```python
create_asset_result = dkg.asset.create(
    content=content,
    options={
        "epochs_num": 6
    },
)
print(create_asset_result)

```

The complete response of the method will look like:

```python
{
    "UAL": "did:dkg:otp:2043/0x8f678eb0e57ee8a109b295710e23076fa3a443fe/572238",
    "datasetRoot": "0xd7a2dd6d747d2f8d2d0f76cc6fa04ebf383a368249cc24a701788f271a41df4d",
    "signatures": [
        {
            "identityId": 131,
            "v": 28,
            "r": "0x583598a701e4c54a1e47e6ff2f0cf0a9660d1749f3e413408ccd3ff5ca2288dc",
            "s": "0x131c07215977c4d681dc30cc32d9e8c1644825b932fb72cf035bb62f0963d2a5",
            "vs": "0x931c07215977c4d681dc30cc32d9e8c1644825b932fb72cf035bb62f0963d2a5"
        },
    ],
    "operation": {
        "mintKnowledgeAsset": {
            "transactionHash": "0x04efacfc576578836c6736f376d23930bb01accd38df31414ff7b5e35861d8f2",
            "transactionIndex": 1,
            "blockHash": "0x98bf84f7cb05f5742213ed305d9e99b59f6c874b6abf10312fc5062bc32f14ac",
            "from": "0x0E1405adD312D97d1a0A4fAA134C7113488D6ceA",
            "to": "0xc8cf8064d7fc7cF42d51Ca5B28218472157F3d90",
            "blockNumber": 7459414,
            "cumulativeGasUsed": 572870,
            "gasUsed": 537962,
            "contractAddress": null,
            "logs": [
             ],
            "logsBloom": "0x000002000000000000000000000000000000000000000000000008004000000000008000000000080000000000000000000000000000000000000000000c0000000000000008000008000008000000000040000000042000004000000000200000000000020100000000000000000808000000000802828000000010000000004000000000000000000000200000000000000000000000000000000200000000000000000000000002001a00000000000000000000000000080000000000001100000042000000000000000000040000000400000001000000000000000060000000080000000000020000000000010000000000000000000000000802000000",
            "status": 1,
            "effectiveGasPrice": 8,
            "type": 2
        },
        "publish": {
            "operationId": "a1709e45-0a0e-44c8-8c67-19edb4baefaa",
            "status": "COMPLETED"
        },
        "finality": {
            "status": "FINALIZED"
        },
        "numberOfConfirmations": 6,
        "requiredConfirmations": 3
    }
}

```

In case you want to create multiple different assets you can increase your allowance and then each time you initiate a publish, the step where a call to the blockchain is made to increase your allowance will be skipped, resulting in a faster publish time.

```python
dkg.asset.increase_allowance(1569429592284014000)

result = dkg.asset.create(
    content=content,
    options={
        "epochs_num": 6
    },
)
```

After you've finished publishing data to the blockchain, you can decrease your allowance to revoke the authorization given to the contract to spend your tokens - so if you want to revoke all remaining authorization, it's a good practice to pass the same value that you used for increasing your allowance.

```python
dkg.asset.decrease_allowance(1569429592284014000)
```

#### Read Knowledge Asset data from the DKG

To read knowledge asset data from the DKG we utilize the **get** protocol operation.

In this example we will get the latest state of the knowledge asset we published previously:

```python
ual = create_asset_result.get("did:dkg:otp:2043/0x8f678eb0e57ee8a109b295710e23076fa3a443fe/572238")

get_asset_result = dkg.asset.get(ual)

print(get_asset_result)
```

The response of the get operation will be the assertion graph:

```python
{
    "assertion": [
        {
            "@id": "https://ontology.origintrail.io/dkg/1.0#metadata-hash:0x5cb6421dd41c7a62a84c223779303919e7293753d8a1f6f49da2e598013fe652",
            "https://ontology.origintrail.io/dkg/1.0#representsPrivateResource": [
                {
                    "@id": "uuid:a7a27a50-7180-4949-b9d7-48ab931b9650"
                }
            ]
        },
        {
            "@id": "https://ontology.origintrail.io/dkg/1.0#metadata-hash:0x6a2292b30c844d2f8f2910bf11770496a3a79d5a6726d1b2fd3ddd18e09b5850",
            "https://ontology.origintrail.io/dkg/1.0#representsPrivateResource": [
                {
                    "@id": "uuid:43e30a8d-fc1e-41e1-a4b4-4d419c21108a"
                }
            ]
        },
        {
            "@id": "https://ontology.origintrail.io/dkg/1.0#metadata-hash:0xc1f682b783b1b93c9d5386eb1730c9647cf4b55925ec24f5e949e7457ba7bfac",
            "https://ontology.origintrail.io/dkg/1.0#representsPrivateResource": [
                {
                    "@id": "uuid:eec71df5-bb62-48cb-b196-9804aff60f51"
                }
            ]
        },
        {
            "@id": "urn:us-cities:info:new-york",
            "http://schema.org/name": [
                {
                    "@value": "New York"
                }
            ],
            "http://schema.org/area": [
                {
                    "@value": "468.9 sq mi"
                }
            ],
            "http://schema.org/population": [
                {
                    "@value": "8,336,817"
                }
            ],
            "http://schema.org/state": [
                {
                    "@value": "New York"
                }
            ],
            "@type": [
                "http://schema.org/City"
            ]
        },
        {
            "@id": "uuid:e63489c8-618b-494c-8fbb-f22ab0537b89",
            "https://ontology.origintrail.io/dkg/1.0#privateMerkleRoot": [
                {
                    "@value": "0xaac2a420672a1eb77506c544ff01beed2be58c0ee3576fe037c846f97481cefd"
                }
            ]
        }
    ],
    "operation": {
        "get": {
            "operationId": "9918220b-5175-44c3-b43a-3544610be560",
            "status": "COMPLETED"
        }
    }
}


```

#### Querying knowledge asset data with SPARQL

Querying the DKG is done by using the SPARQL query language, which is very similar to SQL, applied to graph data (if you have SQL experience, SPARQL should be relatively easy to get started with - more information[ can be found here](https://www.w3.org/TR/rdf-sparql-query/)).

Let’s write simple query to select all subjects and objects in graph that have the **Model** property of Schema.org context:

```python
query_operation_result = dkg.graph.query(
    """
    PREFIX SCHEMA: <http://schema.org/>
    SELECT ?s ?stateName
    WHERE {
        ?s schema:state ?stateName .
    }
    """
)

print(query_graph_result)
```

The returned response will contain an array of n-quads:

```python
{
  "status": "COMPLETED",
  "data": [
    {
      "s": "urn:us-cities:info:new-york",
      "stateName": "\"New York\""
    }
  ]
}
```

As the OriginTrail node leverages a fully fledged graph database (triple store supporting RDF), you can run arbitrary SPARQL queries on it.&#x20;

#### **More on types of interaction with the DKG SDK**

We can divide operations done by SDK into 3 types:

* Node API request
* Smart contract call (non state-changing interaction)
* Smart contract transaction (state-changing interaction)

Non state-changing interactions with smart contracts are free and can be described as contract getters and don’t require transactions on the blockchain, meaning they do not incur transaction fees. Smart contract transactions are state-changing operations, meaning that they’re changing the state of the smart contract memory and it costs some amount in blockchain native gas tokens (such as ETH, NEURO, etc.).

In order to perform state-changing operations, you need to use a wallet funded with gas tokens.

You can use default keys from the example below for hardhat blockchain:

```python
PRIVATE_KEY = "0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80"
PUBLIC_KEY = "0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266"
```

{% hint style="warning" %}
Default keys above should not be used anywhere except in local environment for development.
{% endhint %}
