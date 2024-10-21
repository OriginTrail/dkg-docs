---
description: Javascript library for the Decentralized Knowledge Graph.
---

# DKG Javascript SDK (dkg.js)

If you are looking to build applications leveraging [knowledge assets](../../../dkg-v6-current-version/dkg-basic-concepts.md) on the OriginTrail Decentralized Knowledge Graph (DKG), the dkg.js SDK library is the best place to start!

The DKG SDK is used together with an **OriginTrail gateway node** to build applications that interface with the OriginTrail Decentralized Network (the node is a dependency). Therefore you either need to run a gateway node on [your local environment](../setting-up-your-development-environment.md) or a [hosted OT-Node](../../run-a-v8-core-node-on-testnet/), in order to use the SDK.

### Installation

The library can be used both in the browser or in a NodeJS application.

#### Using dkg.js in the Browser

Use the prebuilt `dist/dkg.min.js`, or build the file on your own using the[ dkg.js](https://github.com/OriginTrail/dkg.js) repository:

```
npm run build
```

Then include `dist/dkg.min.js` in your html file. This will expose `DKG` on the window object:

```javascript
<script src='https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js'></script>
<script src='./dist/dkg.min.js'></script>
<script>
   window.addEventListener('load', async function () {
       // DKG object is available here
   });
</script>
```

{% hint style="info" %}
Make sure to also include web3.js library as it is a dependency for dkg.js.
{% endhint %}

#### Using dkg.js in NodeJS apps

Run the command to install dependency from the [NPM](https://www.npmjs.com/package/dkg.js) repository:

```bash
npm install dkg.js@8.0.0-alpha.2
```

Then include `dkg.js` in your project files. This will expose the `DKG` object:

```javascript
const DKG = require('dkg.js');
```

### :snowboarder:Quickstart

To use the DKG library, you need to connect to a running local or remote OT-Node.&#x20;

```javascript
const dkg = new DKG({
    environment: development, // or devnet, testnet
    endpoint: 'http://127.0.0.1',  // gateway node URI
    port: 8900,
    blockchain: {
        name: 'hardhat1:31337', // or base:8453
        publicKey: PUBLIC_KEY, // not required in browser, metamask used instead
        privateKey: PRIVATE_KEY, // not required in browser, metamask used instead
    },
});
​
const nodeInfo = await dkg.node.info(); 
// if successfully connected, the will return an object indicating the node version
// { 'version': '8.X.X' }
```

#### Create a Knowledge Asset

In this example, let’s create an example Knowledge Asset representing a Tesla Model X car. We will be using a Schema.org type **Car** for our data (detailed schema can be found on [https://schema.org/Car](https://schema.org/Car)). The sample content can be seen below:

```javascript
const publicAssertion = {
    '@context': 'https://schema.org',
    '@id': 'https://tesla.modelX/2321',
    '@type': 'Car',
    'name': 'Tesla Model X',
    'brand': {
        '@type': 'Brand',
        'name': 'Tesla'
    },
    'model': 'Model X',
    'manufacturer': {
        '@type': 'Organization',
        'name': 'Tesla, Inc.'
    },
    'fuelType': 'Electric',
    'numberOfDoors': 5,
    'vehicleEngine': {
        '@type': 'EngineSpecification',
        'engineType': 'Electric motor',
        'enginePower': {
        	'@type': 'QuantitativeValue',
        	'value': '416',
        	'unitCode': 'BHP'
        }
    },
    'driveWheelConfiguration': 'AWD',
    'speed': {
        '@type': 'QuantitativeValue',
        'value': '250',
        'unitCode': 'KMH'
    },
}

```

When you create the knowledge asset, the above JSON-LD object will be converted into an **assertion** (see more [here](../../../dkg-v6-current-version/dkg-basic-concepts.md)). When an assertion with public data is prepared, we can create an knowledge asset on DKG. `epochsNum` specifies for how many epochs the asset should be kept (an epoch is equal to three months).

```javascript
const result = await dkg.asset.create({
    public: publicAssertion,
  },
  { epochsNum: 2 }
);

console.log(result);
```

The complete response of the method will look like:

```javascript
{
  UAL: 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0',
  publicAssertionId: '0xde58cc52a5ce3a04ae7a05a13176226447ac02489252e4d37a72cbe0aea46b42',
  operation: {
    operationId: '5195d01a-b437-4aae-b388-a77b9fa715f1',
    status: 'COMPLETED'
  }
}
```

Before creating a new asset, you have the option to calculate the recommended bid amount to determine how much tokens you'll need to create an asset successfully. This can help you ensure that you have the necessary funds available. Optionally, you can specify bidSuggestionRange as low, mid,  high or all to adjust the suggested bid accordingly and satisfy the ask on desired number of nodes.

<pre class="language-javascript"><code class="lang-javascript"><strong>const bidSuggestion = await dkg.network.getBidSuggestion({
</strong>    public: publicAssertion,
  },
  { epochsNum: 2, bidSuggestionRange: low|mid|high|all }
);

const result = await dkg.asset.create({
    public: publicAssertion,
  },
  { tokenAmount: bidSuggestion, epochsNum: 2 }
);
</code></pre>

In case you want to create multiple different assets you can increase your allowance and then each time you initiate a publish, the step where a call to the blockchain is made to increase your allowance will be skipped, resulting in a faster publish time.

```javascript
await dkg.asset.increaseAllowance('1569429592284014000');

const result = await dkg.asset.create({
    public: publicAssertion,
  },
  { epochsNum: 2 }
);
```

After you've finished publishing data to the blockchain, you can decrease your allowance to revoke the authorization given to the contract to spend your tokens - so if you want to revoke all remaining authorization, it's a good practice to pass the same value that you used for increasing your allowance.

```javascript
await dkg.asset.decreaseAllowance('1569429592284014000');
```

Alternatively, you can set allowance to specific amount of tokens, increasing or decreasing it depending on your current allowance. To do so, you can utilize the following function:

```javascript
await dkg.asset.setAllowance('1000000000000000000');
```

Furthermore, you can always check your current allowance:

```javascript
const currentAllowance = await dkg.asset.getCurrentAllowance();

console.log(currentAllowance);
```

#### Read Knowledge Asset data from the DKG

To read knowledge asset data from the DKG we utilize the **get** protocol operation.

In this example we will get the latest state of the knowledge asset we published previously:

```javascript
const { UAL } = result;

const getAssetResult = await dkg.asset.get(UAL);

console.log(JSON.stringify(getAssetResult, null, 2));
```

The response of the get operation will be the assertion graph:

<pre class="language-javascript"><code class="lang-javascript">{
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

#### Querying knowledge asset data with SPARQL

Querying the DKG is done by using the SPARQL query language, which is very similar to SQL, applied to graph data (if you have SQL experience, SPARQL should be relatively easy to get started with - more information[ can be found here](https://www.w3.org/TR/rdf-sparql-query/)).

Let’s write simple query to select all subjects and objects in graph that have the **Model** property of Schema.org context:

```javascript
const result = await dkg.graph.query(
    `prefix schema: <http://schema.org/>
        select ?s ?modelName
        where {
            ?s schema:model ?modelName
        }`,
    'SELECT',
);

console.log(JSON.stringify(result, null, 2));
```

The returned response will contain an array of n-quads:

```javascript
{
  "status": "COMPLETED",
  "data": [
    {
      "s": "https://tesla.modelX/2321",
      "modelName": "\"Model X\""
    }
  ]
}
```

As the OriginTrail node leverages a fully fledged graph database (triple store supporting RDF), you can run arbitrary SPARQL queries on it.&#x20;

However, when it comes to querying the DKG, it is important to note that at the moment there are only options to query finalized and historical states. This means that any SPARQL queries that are run on the DKG will return data from the latest finalized state by default, or any previously finalized states, identifiable by their state hash.

There is a `graphLocation` option which determines where the query will be executed. The two available options are `LOCAL_KG` and `PUBLIC_KG`. The `LOCAL_KG` option is used to query data from the local knowledge graph which stores all private that is not shared with the network, while the `PUBLIC_KG` option is used to query all data on the node that is received from the network. By default, if the `graphLocation` option is not specified, the query will be executed on the local knowledge graph (`LOCAL_KG`).

Example:

```javascript
let options = {
    graphLocation: 'LOCAL_KG'
};

const result = await dkg.graph.query(
    `prefix schema: <https://schema.org/>
        select ?s ?modelName
        where {
            ?s schema:model ?modelName
        }`,
    'SELECT',
    options
);

console.log(JSON.stringify(result, null, 2));
```

**Create a Knowledge Asset with private data**

In addition to knowledge assets with public assertions, we can add private data to our knowledge asset by creating private assertions, which will contain data that we don’t want to expose publicly.

The sample assertion content for public assertion will be the same as before, just a bit reduced:

```javascript
const publicAssertion = {
    '@context': 'https://schema.org',
    '@id': 'https://tesla.modelX/2321',
    '@type': 'Car',
    'name': 'Tesla Model X',
    'brand': {
        '@type': 'Brand',
        'name': 'Tesla'
    },
    'model': 'Model X',
    'manufacturer': {
        '@type': 'Organization',
        'name': 'Tesla, Inc.'
    },
}
```

Sample private assertion:

<pre class="language-javascript"><code class="lang-javascript">const privateAssertion = {
<strong>    '@context': 'https://schema.org',
</strong><strong>    '@id': 'https://tesla.modelX/2321',
</strong>    'productionDate': '2015-09-29',
    'mileageFromOdometer': {
        '@type': 'QuantitativeValue',
    	'value': '25672',
    	'unitCode': 'KMT'
    },
}
</code></pre>

When assertions with public and private data are prepared, we can publish it on the DKG. It’s actually as simple as executing one function:&#x20;

```javascript
const result = await dkg.asset.create({
            public: publicAssertion,
            private: privateAssertion,      
      },
      {
            epochsNum: 2,
      }
);

console.log(result);
```

The complete response of the method will look like:

```javascript
{
    UAL: 'did:dkg:hardhat1:31337/0xa5cef543538b997b7a125cc849005b62a3da2271/1',
    publicAssertionId: '0xef11c3f4bc3331f5d1ad3ec8ddb63928913f7a4d546c6a03fe4485837ad4c494',
    operation: {
        operationId: '1c7e860a-219c-4a0c-896d-9c62e19e3fe4',
        status: 'COMPLETED'
    }
}

```

**Get Knowledge Asset private assertion from the DKG**

To read knowledge asset private assertion from the DKG we utilize the same get protocol operation as before, just now we will specify content type option to be private. Keep in mind, you can only get private assertions if your node owns them. This feature is to be further extended with knowledge marketplace tools for knowledge asset monetization.

```javascript
const { UAL } = createAssetResult;

const options = {
	contentType: "private"
};
const getAssetResult = await dkg.asset.get(UAL, options);

console.log(JSON.stringify(getAssetResult, null, 2));
```

The response of the get operation will be the assertion graph:

```javascript
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

```javascript
const getOwnerResult = await dkg.asset.getOwner(UAL);

console.log(getOwnerResult);
```

Owner of the Knowledge Asset:

```javascript
{
  UAL: 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0',
  owner: '0xBaF76aC0d0ef9a2FFF76884d54C9D3e270290a43',
  operation: { operationId: null, status: 'COMPLETED' }
}
```

#### Transfer Knowledge Asset ownership

It’s also possible to transfer ownership of the asset ERC721 token.

In this example we will transfer our Tesla ERC721 token to another wallet:

```javascript
const newOwner = "0x2ACa90078563133db78085F66e6B8Cf5531623Ad";

const assetTransferResult = await dkg.asset.transfer(UAL, newOwner);

console.log(assetTransferResult);
```

Result of the transfer operation:

```javascript
{
  UAL: 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/0',
  owner: '0x2ACa90078563133db78085F66e6B8Cf5531623Ad',
  operation: { operationId: null, status: 'COMPLETED' }
}
```

#### Check Knowledge Asset State Issuer

Since it's possible to transfer ownership of the Knowledge Asset and also update it, we can expect that different states of the asset can have different issuers.

Knowing index of the state we're interested in, it's possible to get issuer of this specific state.

In this example, we will get issuer of the previous state for the asset that has multiple states:

```javascript
const getStatesResult = await dkg.asset.getStates(UAL);
const previousStateIndex = getStatesResult.states.length - 2;

const getStateIssuerResult = await dkg.asset.getStateIssuer(UAL, previousStateIndex);

console.log(getStateIssuerResult);
```

&#x20;Result of the get issuer operation:

```javascript
{
  UAL: 'did:dkg:hardhat1:31337/0xb0d4afd8879ed9f52b28595d31b441d079b2ca07/0',
  issuer: '0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC',
  state: '0xe3a6733d7b999ca6f0d141afe3e38ac59223a4dfde7a5458932d2094ed4193cf',
  operation: { operationId: null, status: 'COMPLETED' }
}
```

In order to get latest state issuer, you can use this function:

```javascript
const getLatestStateIssuerResult = await dkg.asset.getLatestStateIssuer(UAL);
```

With the following result:

```javascript
{
  UAL: 'did:dkg:hardhat1:31337/0xb0d4afd8879ed9f52b28595d31b441d079b2ca07/0',
  issuer: '0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC',
  latestState: '0xe37350c9b0e2881af2e7e89a986e87f3d3158611b794bf75dcbb8d6e4aea7f95',
  operation: { operationId: null, status: 'COMPLETED' }
}
```

#### Estimate cost of the Knowledge Asset publishing

Before actual creation of the Knowledge Asset, we can estimate how much would it cost for publisher to host Knowledge Asset on the DKG for a specific period of time.

In order to do this, we can send a request to one of the DKG nodes, which would return suggested cost of the publishing (so that Knowledge Asset is accepted by at least 8 nodes on the DKG).

In order to estimate cost of the publishing, you should know the metadata of the public assertion, such as: assertion ID (Merkle Root) and size in bytes. Additionally, you need to provide number of epochs.

Don't know how to calculate assertion metadata? Don't you worry, in the following example we will go through all the steps from having just Knowledge Asset content to having estimated price.

```javascript
const knowledgeAssetContent = {
    public: {
        '@context': ['https://schema.org'],
        '@id': 'uuid:1',
        company: 'OT',
        user: {
            '@id': 'uuid:user:1',
        },
        city: {
            '@id': 'uuid:belgrade',
        },
    },
    private: {
        '@context': ['https://schema.org'],
        '@graph': [
            {
                '@id': 'uuid:user:1',
                name: 'Adam',
                lastname: 'Smith',
            },
            {
                '@id': 'uuid:belgrade',
                title: 'Belgrade',
                postCode: '11000',
            },
        ],
    },
};
```

In order to calculate public assertion metadata, we would use **assertion module**:

```javascript
const publicAssertionId = await dkg.assertion.getPublicAssertionId(knowledgeAssetContent);
const publicAssertionSize = await dkg.assertion.getSizeInBytes(knowledgeAssetContent);
```

Besides assertion ID and size, following functions are available in the **assertion module**:

* **formatGraph(knowledgeAssetContent)** - formats the content provided, producing both a public and, if available, a private assertion and a link to it in the public assertion.
* **getTriplesNumber(knowledgeAssetContent)** - calculates and returns the number of triples of the public assertion from the provided content.
* **getChunksNumber(knowledgeAssetContent)** - calculates and returns the number of chunks of the public assertion from the provided content.

After calculating public assertion metadata, we can get suggested publishing cost (in Wei), using the **network module**:

```javascript
const bidSuggestion = await dkg.network.getBidSuggestion(
    publicAssertionId,
    publicAssertionSize,
    { epochsNum: 2 },
);
```

#### **More on types of interaction with the DKG SDK**

We can divide operations done by SDK into 3 types:

* Node API request
* Smart contract call (non state-changing interaction)
* Smart contract transaction (state-changing interaction)

Non state-changing interactions with smart contracts are free and can be described as contract getters and don’t require transactions on the blockchain, meaning they do not incur transaction fees. Smart contract transactions are state-changing operations, meaning that they’re changing the state of the smart contract memory and it costs some amount in blockchain native gas tokens (such as ETH, NEURO, etc.).

In order to perform state-changing operations, you need to use a wallet funded with gas tokens.

You can use default keys from the example below for hardhat blockchain:

```javascript
const PRIVATE_KEY="0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80"
const PUBLIC_KEY="0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266"
```

{% hint style="warning" %}
Default keys above should not be used anywhere except in local environment for development.
{% endhint %}
