---
description: Python library for interacting with the Decentralized Knowledge Graph.
---

# DKG Python SDK (dkg.py)



{% hint style="danger" %}
dkg.py library is currently in beta. The beta version is intended for testing and evaluation purposes only. It is not recommended for use in a production environment where stability and reliability are crucial.
{% endhint %}

If you are looking to build applications leveraging [knowledge assets](../dkg-basic-concepts.md) on the OriginTrail Decentralized Knowledge Graph (DKG), the dkg.py library is the best place to start!

The DKG SDK is used together with an **OriginTrail gateway node** to build applications that interface with the OriginTrail Decentralized Network (the node is a dependency). Therefore you either need to run a gateway node on[ your local environment](https://docs.origintrail.io/decentralized-knowledge-graph-layer-2/setting-up-your-development-environment) or a[ hosted OT-Node](https://docs.origintrail.io/decentralized-knowledge-graph-layer-2/testnet-node-setup-instructions), in order to use the SDK.

{% hint style="info" %}
Running a gateway node is not the same as running a **full (DKG hosting) node**, which requires 50 000 TRAC tokens to be posted as stake collateral. Running a gateway node requires no tokens to be posted as collateral.
{% endhint %}

### Installation

The library can be used in any Python application.

Run the command to install dkg.py library using pip:

```bash
pip install dkg
```

pip x:

```bash
pipx install dkg
```

or poetry:

```bash
poetry add dkg
```

Then import DKG, BlockchainProvider and NodeHTTPProvider classes inside your project:

```python
from dkg import DKG
from dkg.providers import BlockchainProvider, NodeHTTPProvider
```

### :snowboarder:Quickstart

To use the DKG library, you need to connect to a running local or remote OT-Node.&#x20;

```python
node_provider = NodeHTTPProvider("http://localhost:8900")
blockchain_provider = BlockchainProvider(
    "http://localhost:8545",
    PRIVATE_KEY,
)

dkg = DKG(node_provider, blockchain_provider)

print(dkg.node.info)
# if successfully connected, this should print the dictionary with node version
# { "version": "6.X.X" }
```

#### Create a Knowledge Asset

In this example, let’s create an example Knowledge Asset representing a Tesla Model X car. We will be using a Schema.org type **Car** for our data (detailed schema can be found on [https://schema.org/Car](https://schema.org/Car)). The sample content can be seen below:

```python
public_assertion = {
    "@context": "https://schema.org",
    "@id": "https://tesla.modelX/2321",
    "@type": "Car",
    "name": "Tesla Model X",
    "brand": {"@type": "Brand", "name": "Tesla"},
    "model": "Model X",
    "manufacturer": {"@type": "Organization", "name": "Tesla, Inc."},
    "fuelType": "Electric",
    "numberOfDoors": 5,
    "vehicleEngine": {
        "@type": "EngineSpecification",
        "engineType": "Electric motor",
        "enginePower": {
            "@type": "QuantitativeValue",
            "value": "416",
            "unitCode": "BHP",
        },
    },
    "driveWheelConfiguration": "AWD",
    "speed": {"@type": "QuantitativeValue", "value": "250", "unitCode": "KMH"},
}
```

When you create the knowledge asset, the above JSON-LD object will be converted into an **assertion** (see more [here](../dkg-basic-concepts.md)). When an assertion with public data is prepared, we can create an knowledge asset on DKG.&#x20;

```python
create_asset_result = dkg.asset.create(
    {
        "public": public_assertion,
    },
    epochs_number=2,
)

print(create_asset_result)
```

The complete response of the method will look like:

```python
{
  "UAL": "did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0",
  "publicAssertionId": "0xde58cc52a5ce3a04ae7a05a13176226447ac02489252e4d37a72cbe0aea46b42",
  "operation": {
    "operationId": "5195d01a-b437-4aae-b388-a77b9fa715f1",
    "status": "COMPLETED"
  }
}
```

In case you want to create multiple different assets you can increase your allowance and then each time you initiate a publish, the step where a call to the blockchain is made to increase your allowance will be skipped, resulting in a faster publish time.

```python
dkg.asset.increase_allowance(1569429592284014000)

result = dkg.asset.create(
  {
    "public": publicAssertion,
  },
  epochs_number=2,
)
```

After you've finished publishing data to the blockchain, you can decrease your allowance to revoke the authorization given to the contract to spend your tokens - so if you want to revoke all remaining authorization, it's a good practice to pass the same value that you used for increasing your allowance.

```python
dkg.asset.decrease_allowance(1569429592284014000)
```

Alternatively, you can set allowance to specific amount of tokens, increasing or decreasing it depending on your current allowance. To do so, you can utilize the following function:

```python
dkg.asset.set_allowance(1000000000000000000)
```

Furthermore, you can always check your current allowance:

```python
current_allowance = dkg.asset.get_current_allowance()

print(current_allowance)
```

#### Read Knowledge Asset data from the DKG

To read knowledge asset data from the DKG we utilize the **get** protocol operation.

In this example we will get the latest state of the knowledge asset we published previously:

```python
ual = create_asset_result["UAL"]

get_asset_result = dkg.asset.get(ual)

print(get_asset_result)
```

The response of the get operation will be the assertion graph:

<pre class="language-python"><code class="lang-python">{
  "assertion": [
    {
      "@id": "_:c14n0",
      "http://schema.org/name": [
        {
          "@value": "Tesla, Inc."
        }
      ],
      "@type": [
        "http://schema.org/Organization"
      ]
    },
    {
      "@id": "_:c14n1",
      "http://schema.org/unitCode": [
        {
          "@value": "KMH"
        }
      ],
      "http://schema.org/value": [
        {
          "@value": "250"
        }
      ],
      "@type": [
        "http://schema.org/QuantitativeValue"
      ]
    },
    {
      "@id": "_:c14n2",
      "http://schema.org/enginePower": [
        {
          "@id": "_:c14n4"
        }
      ],
      "http://schema.org/engineType": [
        {
          "@value": "Electric motor"
        }
      ],
      "@type": [
        "http://schema.org/EngineSpecification"
      ]
    },
    {
      "@id": "_:c14n3",
      "http://schema.org/name": [
        {
          "@value": "Tesla"
        }
      ],
      "@type": [
        "http://schema.org/Brand"
      ]
    },
    {
      "@id": "_:c14n4",
      "http://schema.org/unitCode": [
        {
          "@value": "BHP"
        }
      ],
      "http://schema.org/value": [
        {
          "@value": "416"
        }
      ],
      "@type": [
        "http://schema.org/QuantitativeValue"
      ]
    },
    {
      "@id": "https://tesla.modelX/2321",
      "http://schema.org/brand": [
        {
          "@id": "_:c14n3"
        }
      ],
      "http://schema.org/driveWheelConfiguration": [
        {
          "@value": "AWD"
        }
      ],
<strong>      "http://schema.org/fuelType": [
</strong>        {
          "@value": "Electric"
        }
      ],
      "http://schema.org/manufacturer": [
        {
          "@id": "_:c14n0"
        }
      ],
      "http://schema.org/model": [
        {
          "@value": "Model X"
        }
      ],
      "http://schema.org/name": [
        {
          "@value": "Tesla Model X"
        }
      ],
      "http://schema.org/numberOfDoors": [
        {
          "@value": "5",
          "@type": "http://www.w3.org/2001/XMLSchema#integer"
        }
      ],
      "http://schema.org/speed": [
        {
          "@id": "_:c14n1"
        }
      ],
      "http://schema.org/vehicleEngine": [
        {
          "@id": "_:c14n2"
        }
      ],
      "@type": [
        "http://schema.org/Car"
      ],
      "https://dkg.private": [
        {
          "@value": "0x0742b8172dd827e2b2905b4968df1e5d1213071cbcba0b04378a4931c904e9b1"
        }
      ]
    }
  ],
  "assertionId": "0xde58cc52a5ce3a04ae7a05a13176226447ac02489252e4d37a72cbe0aea46b42",
  "operation": {
    "operationId": "5f343130-bf0f-471e-8fda-9b400f0aa392",
    "status": "COMPLETED"
  }
}

</code></pre>

#### Update Knowledge Asset data

Knowledge assets can be updated by using the **update** function. In this example we will update the previously published knowledge asset to reflect the features of the Tesla S model. The updated content can be seen below:

```python
updated_public_assertion = {
    "@context": "https://schema.org",
    "@id": "https://tesla.modelS/2322",
    "@type": "Car",
    "name": "Tesla Model S",
    "brand": {"@type": "Brand", "name": "Tesla"},
    "model": "Model S",
    "manufacturer": {"@type": "Organization", "name": "Tesla, Inc."},
    "fuelType": "Electric",
}
```

The function call for updating a knowledge asset receives a UAL (the same one that the previous create returned) and is of same structure as for knowledge asset creation:

```python
update_asset_result = dkg.asset.update(ual, {"public": updated_public_assertion})

print(update_asset_result)
```

The returned response will contain the UAL and operation status:

```python
{
  "UAL": "did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0",
  "operation": {
    "operationId": "50fd6920-e084-433b-a518-26bf326a7b5a",
    "status": "COMPLETED"
  }
}
```

After an update is finalized, a user can get the updated asset state by invoking the get operation.

**Note on state finality**

Similar to distributed databases, the OriginTrail Decentralized Knowledge Graph applies replication mechanisms and needs mechanisms to reach a consistent state on the network for knowledge assets. In OriginTrail DKG, state consistency is reconciled using the blockchain, which hosts state proofs for knowledge assets as well as replication commit information from DKG nodes. This means that updates for an existing knowledge asset are accepted by the network nodes (similar to the way nodes accept knowledge assets on creation) and can operate with all accepted states.

There are three phases for a state of a knowledge asset:

* LATEST: which indicates the Knowledge Asset state pending for an update, awaiting commits from DKG nodes. Once commits are received, the state transitions to LATEST\_FINALIZED.
* LATEST\_FINALIZED: latest committed state, accepted by the network.
* HISTORICAL: any previously finalized state, identifiable by its state hash.

The user is able to specify if he wants to get the latest or latest finalized state. Example:

```python
asset = dkg.asset.get(ual, state="LATEST_FINALIZED")
```

Application builders are able to get all above states, however querying the DKG (via query functions) will only return the cumulative finalized state, for consistency reasons.

#### Querying knowledge asset data with SPARQL

Querying the DKG is done by using the SPARQL query language, which is very similar to SQL, applied to graph data (if you have SQL experience, SPARQL should be relatively easy to get started with - more information[ can be found here](https://www.w3.org/TR/rdf-sparql-query/)).

Let’s write simple query to select all subjects and objects in graph that have the **Model** property of Schema.org context:

```python
query_graph_result = dkg.graph.query(
    """
    PREFIX SCHEMA: <http://schema.org/>
    SELECT ?s ?modelName
    WHERE {
        ?s schema:model ?modelName
    }
    """,
    repository="publicCurrent",
)

print(query_graph_result)
```

The returned response will contain an array of n-quads:

```python
[{'s': 'https://tesla.modelX/2321', 'modelName': '"Model X"'}]
```

As the OriginTrail node leverages a fully fledged graph database (triple store supporting RDF), you can run arbitrary SPARQL queries on it.&#x20;

However, when it comes to querying the DKG, it is important to note that at the moment there are only options to query finalized and historical states. This means that any SPARQL queries that are run on the DKG will return data from the latest finalized state by default, or any previously finalized states, identifiable by their state hash.

To query for full (private+public data) historical states in the DKG, you need to use the `repository: 'privateHistory'` option when making the SPARQL query. Here's an example of how to do that:

```python
query_graph_result = dkg.graph.query(
    """
    PREFIX SCHEMA: <http://schema.org/>
    SELECT ?s ?modelName
    WHERE {
        ?s schema:model ?modelName
    }
    """,
    repository="privateHistory",
)

print(query_graph_result)
```

To query the full latest finalized state of the DKG, the `'privateCurrent'` option should be passed for the repository parameter. It's important to note that this is also the default behavior if the repository parameter is not specified in the SPARQL query.

There are 4 repositories available:

* **privateHistory (default)** - private and public data of the historical states.
* **publicHistory** - public data of the historical states.
* **privateCurrent** - private and public data of the latest finalized state.
* **publicCurrent** - public data of the latest finalized state.

**Query for Historical State of the Knowledge Asset**

Sometimes we want to get data of historical state of the Knowledge Asset. To do so, we can use the following query:

```python
state_id = "0xd721c7aa159430f23b30f9fda5fe906eacce6f468a72cb08448bcb2828ba54f3"

query_graph_result = dkg.graph.query(
    f"""
    PREFIX SCHEMA: <http://schema.org/>
    CONSTRUCT {{ ?s ?p ?o }}
    WHERE {{
        {{
            GRAPH <assertion:{state_id}>
            {{ ?s ?p ?o . }}
        }}
    }}
    """,
    repository="privateHistory",
)

print(query_graph_result)
```

**Create a Knowledge Asset with private data**

In addition to knowledge assets with public assertions, we can add private data to our knowledge asset by creating private assertions, which will contain data that we don’t want to expose publicly.

The sample assertion content for public assertion will be the same as before, just a bit reduced:

```python
public_assertion = {
    "@context": "https://schema.org",
    "@id": "https://tesla.modelX/2321",
    "@type": "Car",
    "name": "Tesla Model X",
    "brand": {"@type": "Brand", "name": "Tesla"},
    "model": "Model X",
    "manufacturer": {"@type": "Organization", "name": "Tesla, Inc."},
}
```

Sample private assertion:

```python
private_assertion = {
    "@context": "https://schema.org",
    "@id": "https://tesla.modelX/2321",
    "productionDate": "2015-09-29",
    "mileageFromOdometer": {
        "@type": "QuantitativeValue",
        "value": "25672",
        "unitCode": "KMT",
    },
}
```

When assertions with public and private data are prepared, we can publish it on the DKG. It’s actually as simple as executing one function:&#x20;

```python
create_asset_result = dkg.asset.create(
    {
        "public": public_assertion,
        "private": private_assertion,
    },
    epochs_number=2,
)

print(create_asset_result)
```

The complete response of the method will look like:

```python
{
    "UAL": "did:dkg:hardhat1:31337/0xa5cef543538b997b7a125cc849005b62a3da2271/1",
    "publicAssertionId": "0xef11c3f4bc3331f5d1ad3ec8ddb63928913f7a4d546c6a03fe4485837ad4c494",
    "operation": {
        "operationId": "1c7e860a-219c-4a0c-896d-9c62e19e3fe4",
        "status": "COMPLETED"
    }
}

```

**Get Knowledge Asset private assertion from the DKG**

To read knowledge asset private assertion from the DKG we utilize the same get protocol operation as before, just now we will specify content\_visibility option to be private. Keep in mind, you can only get private assertions if your node owns them. This feature is to be further extended with knowledge marketplace tools for knowledge asset monetization.

```python
ual = create_asset_result["UAL"]

get_asset_result = dkg.asset.get(ual, content_visibility="private")

print(get_asset_result)
```

The response of the get operation will be the assertion graph:

```python
{
  "operation": {
    "queryPrivate": {
      "operationId": "30734787-3779-4a02-8b79-82102c508327",
      "status": "COMPLETED"
    }
  },
  "assertion": [
    {
      "@id": "_:c14n0",
      "http://schema.org/unitCode": [
        {
          "@value": "KMT"
        }
      ],
      "http://schema.org/value": [
        {
          "@value": "25672"
        }
      ],
      "@type": [
        "http://schema.org/QuantitativeValue"
      ]
    },
    {
      "@id": "https://tesla.modelX/2321",
      "http://schema.org/mileageFromOdometer": [
        {
          "@id": "_:c14n0"
        }
      ],
      "http://schema.org/productionDate": [
        {
          "@value": "2015-09-29",
          "@type": "http://schema.org/Date"
        }
      ]
    }
  ],
  "assertionId": "0x0742b8172dd827e2b2905b4968df1e5d1213071cbcba0b04378a4931c904e9b1"
}
```

#### Check Knowledge Asset Owner

Thanks to the blockchain representation of the Knowledge Assets it’s possible to check the owner of the Knowledge Asset by checking the ownership record of its NFT token, representing the asset on-chain.

In order to do this, we should execute the function below:

```python
owner = dkg.asset.get_owner(ual)

print(owner)
```

Owner of the Knowledge Asset:

```python
{
  "UAL": "did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0",
  "owner": "0xBaF76aC0d0ef9a2FFF76884d54C9D3e270290a43",
  "operation": { "operationId": None, "status": "COMPLETED" }
}
```

#### Transfer Knowledge Asset ownership

It’s also possible to transfer ownership of the asset ERC721 token.

In this example we will transfer our Tesla ERC721 token to another wallet:

```python
new_owner = "0x2ACa90078563133db78085F66e6B8Cf5531623Ad"

asset_transfer_result = dkg.asset.transfer(ual, new_owner)

print(asset_transfer_result)
```

Result of the transfer operation:

```python
{
  "UAL": "did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0",
  "owner": "0x2ACa90078563133db78085F66e6B8Cf5531623Ad",
  "operation": { "operationId": None, "status": "COMPLETED" }
}
```

#### Estimate cost of the Knowledge Asset publishing

Before actual creation of the Knowledge Asset, we can estimate how much would it cost for publisher to host Knowledge Asset on the DKG for a specific period of time.

In order to do this, we can send a request to one of the DKG nodes, which would return suggested cost of the publishing (so that Knowledge Asset is accepted by at least 8 nodes on the DKG).

In order to estimate cost of the publishing, you should know the metadata of the public assertion, such as: assertion ID (Merkle Root) and size in bytes. Additionally, you need to provide number of epochs.

Don't know how to calculate assertion metadata? Don't you worry, in the following example we will go through all the steps from having just Knowledge Asset content to having estimated price.

```python
knowledge_asset_content = {
    "public": {
        "@context": ["http://schema.org"],
        "@id": "uuid:1",
        "company": "OT",
        "user": {"@id": "uuid:user:1"},
        "city": {"@id": "uuid:belgrade"},
    },
    "private": {
        "@context": ["http://schema.org"],
        "@graph": [
            {"@id": "uuid:user:1", "name": "Adam", "lastname": "Smith"},
            {"@id": "uuid:belgrade", "title": "Belgrade", "postCode": "11000"},
        ],
    },
}
```

In order to calculate public assertion metadata, we would use **assertion module**:

```python
public_assertion_id = dkg.assertion.get_public_assertion_id(knowledge_asset_content)
public_assertion_size = dkg.assertion.get_size(knowledge_asset_content)
```

Besides assertion ID and size, following functions are available in the **assertion module**:

* **format\_graph(knowledge\_asset\_content)** - formats the content provided, producing both a public and, if available, a private assertion and a link to it in the public assertion.
* **get\_triples\_number(knowledge\_asset\_content)** - calculates and returns the number of triples of the public assertion from the provided content.
* **get\_chunks\_number(knowledge\_asset\_content)** - calculates and returns the number of chunks of the public assertion from the provided content.

After calculating public assertion metadata, we can get suggested publishing cost using the **network module**:

```python
bid_suggestion = dkg.network.get_bid_suggestion(
    public_assertion_id,
    public_assertion_size,
    2,
)
```

#### **More on types of interaction with the DKG SDK**

We can divide operations done by SDK into 3 types:

* Node API request
* Smart contract call (non state-changing interaction)
* Smart contract transaction (state-changing interaction)

Non state-changing interactions with smart contracts are free and can be described as contract getters and don’t require transactions on the blockchain, meaning they do not incur transaction fees. Smart contract transactions are state-changing operations, meaning that they’re changing the state of the smart contract memory and it costs some amount in blockchain native gas tokens (such as ETH, OTP, etc.).

In order to perform state-changing operations, you need to use a wallet funded with gas tokens.

You can use default keys from the example below for hardhat blockchain:

```python
PRIVATE_KEY = "0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80"
PUBLIC_KEY = "0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266"
```

{% hint style="warning" %}
Default keys above should not be used anywhere except in local environment for development.
{% endhint %}
