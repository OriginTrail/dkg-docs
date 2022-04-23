---
description: Javascript library for the Decentralized Knowledge Graph.
---

# Javascript SDK (dkg.js)

If you are looking to build Web3 applications on the OriginTrail DKG, the dkg.js SDK library is the best place to start!

The DKG SDK is used together with an OriginTrail node (the node is it's dependency). Therefore you either need to run a node on [your local environment](../setting-up-your-development-environment.md) or a [hosted OT-Node](../testnet-node-setup-instructions/), in order to use the SDK.&#x20;

{% hint style="info" %}
This library operates with OriginTrail nodes starting with v6.
{% endhint %}

### Installation

The library can be used both in the browser or in a NodeJS application.

#### In the Browser

Use the prebuilt `dist/dkg.min.js`, or build using the [DKG.js](https://github.com/OriginTrail/dkg.js) repository:

```
npm run build
```

Then include `dist/dkg.min.js` in your html file. This will expose `DKG` on the window object:

```javascript
<script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
<script src="./dist/dkg.min.js"></script>
<script>
    window.addEventListener('load', async function () {
        // TODO
    });
</script>
```

{% hint style="info" %}
Make sure to also include Web3.js library as it is a dependency for DKG.js!
{% endhint %}

#### In NodeJS apps

Run the command to install dependency from the [NPM](https://www.npmjs.com/package/dkg.js) repository:

```bash
npm install dkg.js
```

Then include `dkg.js` in your node file. This will expose `DKG` on as a variable:

```javascript
const DKG = require('dkg.js');
```

### :snowboarder:Quickstart

To use the DKG library, you need to connect to a running local or remote OT-Node.&#x20;

```javascript
const dkg = new DKG({ 
            endpoint: '127.0.0.1', 
            port: '8900', 
            useSSL: false,
            loglevel: 'trace' 
    });

var result = await dkg.nodeInfo();
console.log(JSON.stringify(result, null, 2));
```

In the code snippet above, you enter the node's hostname, port, type of protocol, and log level.  After connecting to the node, it will log the informations about node, like:

```json
{
  "version": "6.0.0-beta.1.30",
  "auto_update": false,
  "telemetry": false
}
```

The library has `assets` and `native` modules. Assets module is intended for handling assets on the network, while native module is intended for basic protocol operations on the network, such as searching, executing queries and retrieving proofs.

#### Create an asset

Asset presents a digital or physical object indexed on the DKG. Asset used in this tutorial is maintained by [schema.org](https://schema.org) can be found [here](https://schema.org/Product).

It follows the standard and contains an object of type `Product` __ with its description, name, image, and other details. An extensive documentation for Product class can be found here [https://schema.org/Product](https://schema.org/Product). The sample dataset values can be referred below:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "3.5",
    "reviewCount": "11"
  },
  "description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
  "name": "Kenmore White 17\" Microwave",
  "image": "kenmore-microwave-17in.jpg",
  "offers": {
    "@type": "Offer",
    "availability": "https://schema.org/InStock",
    "price": "55.00",
    "priceCurrency": "USD"
  },
  "review": [
    {
      "@type": "Review",
      "author": "Ellie",
      "datePublished": "2011-04-01",
      "reviewBody": "The lamp burned out and now I have to replace it.",
      "name": "Not a happy camper",
      "reviewRating": {
        "@type": "Rating",
        "bestRating": "5",
        "ratingValue": "1",
        "worstRating": "1"
      }
    },
    {
      "@type": "Review",
      "author": "Lucas",
      "datePublished": "2011-03-25",
      "reviewBody": "Great microwave for the price. It is small and fits in my apartment.",
      "name": "Value purchase",
      "reviewRating": {
        "@type": "Rating",
        "bestRating": "5",
        "ratingValue": "4",
        "worstRating": "1"
      }
    }
  ]
}
```

Index the asset with associated keywords. In this example, the keyword is `microwave`:

```javascript
var result = await dkg.assets.create({
    "@context": "https://schema.org",
    "@type": "Product",
    "aggregateRating": {
    "@type": "AggregateRating",
        "ratingValue": "3.5",
        "reviewCount": "11"
},
    "description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
    "name": "Kenmore White 17\" Microwave",
    "image": "kenmore-microwave-17in.jpg",
    "offers": {
    "@type": "Offer",
        "availability": "https://schema.org/InStock",
        "price": "55.00",
        "priceCurrency": "USD"
},
    "review": [
    {
        "@type": "Review",
        "author": "Ellie",
        "datePublished": "2011-04-01",
        "reviewBody": "The lamp burned out and now I have to replace it.",
        "name": "Not a happy camper",
        "reviewRating": {
            "@type": "Rating",
            "bestRating": "5",
            "ratingValue": "1",
            "worstRating": "1"
        }
    },
    {
        "@type": "Review",
        "author": "Lucas",
        "datePublished": "2011-03-25",
        "reviewBody": "Great microwave for the price. It is small and fits in my apartment.",
        "name": "Value purchase",
        "reviewRating": {
            "@type": "Rating",
            "bestRating": "5",
            "ratingValue": "4",
            "worstRating": "1"
        }
    }]
}, {
    keywords: ['microwave'],
    visibility: 'public'
})
let ual = result.data.metadata.UALs[0];
console.log(ual);
```

After returning the result, the asset's unique identifier (UAL) is logged. The complete response of the method is:

```javascript
{
  status: 'COMPLETED',
  data: {
    id: '0b2f32a380f61fda8a3b2461074183dfbc9e19c0cbb59275969e6370aa5b26cf',
    rootHash: '94ad72c79a88fd2da048cc8c4b3abbdc2cd507ab4b9fccfacd9eae0f8907dac3',
    signature: '0x2a036001d2ca32fb2e528d6e8c414ab86f5b000e87558ae9c75a74c46bcd4fc16d47e865412341640b3d81e05fd2e4ed9f96d63188ad28476b276ba1d7c06d581b',
    metadata: {
      type: 'Product',
      UALs: ['aa1bd80f61fda8a3b2461074183dfbc9e19c0cbb59275969e6370aa5b26cf']
      timestamp: '2022-30-30T13:08:14.770Z',
      issuer: '0xbd084ab97c704fe4a6d620cb7c30c0be0366646f',
      visibility: true,
      dataHash: 'ed13153fa4090eceedf6c1dd1aa030ec45ab75c2f9510c64a2014f1c6424e7dd'
    },
    blockchain: {
      name: 'polygon::testnet',
      transactionHash: '0x2450007ccaec94e18f2d0ed20e776f05aa43ab6f8480d3ee2d77c61bece71184'
    }
  }
}

```

#### Read an asset from the DKG

Data are persisted on the network by indexing and replicating on the DKG. Assets consist of building blocks entitled as assertions that are immutable and verifiable. Assets could be resolved from the network by using UAL:

```javascript
var productProxy = await dkg.assets.get(ual);

const productData = await productProxy.data.valueOf;
console.log(JSON.stringify(productData));
```

The proxy object can access any property in an object **except an array** (which is case in this tutorial), like:

```javascript
await productProxy.data.name
```

The response response of the asset's data is:

```javascript
{
    "@context": "https://www.schema.org/",
    "@graph": [
        {
            "aggregateRating": {
                "id": "_:b1",
                "ratingValue": "3.5",
                "reviewCount": "11",
                "type": "AggregateRating"
            },
            "description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
            "name": "Kenmore White 17\" Microwave",
            "offers": {
                "availability": "https://schema.org/InStock",
                "id": "_:b2",
                "price": "55.00",
                "priceCurrency": "USD",
                "type": "Offer"
            },
            "proof": {
                "account": "0xE6976A991A9C32aB665E1118Fd7cfDB58A23116d",
                "hash": "0x7bc087f4ef9d0dc15fef823bff9c78cc5cca8be0a85234afcfd807f412f40877",
                "id": "_:b3",
                "signature": "0x13a970137bd89ac8e812aafd049f74c1fa7138b9ed1b94a177a9c02af063038b39086b110b6751d3f18b4ba39cbeaaf506fed386828144f1826a4215a4499abc1c"
            },
            "review": [
                {
                    "author": "Ellie",
                    "datePublished": "2011-04-01",
                    "id": "_:b4",
                    "name": "Not a happy camper",
                    "reviewBody": "The lamp burned out and now I have to replace it.",
                    "reviewRating": {
                        "bestRating": "5",
                        "id": "_:b6",
                        "ratingValue": "1",
                        "type": "Rating",
                        "worstRating": "1"
                    },
                    "type": "Review"
                },
                {
                    "author": "Lucas",
                    "datePublished": "2011-03-25",
                    "id": "_:b5",
                    "name": "Value purchase",
                    "reviewBody": "Great microwave for the price. It is small and fits in my apartment.",
                    "reviewRating": {
                        "bestRating": "5",
                        "id": "_:b7",
                        "ratingValue": "4",
                        "type": "Rating",
                        "worstRating": "1"
                    },
                    "type": "Review"
                }
            ],
            "type": "Product"
        },
        {
            "id": "_:b1",
            "ratingValue": "3.5",
            "reviewCount": "11",
            "type": "AggregateRating"
        },
        {
            "availability": "https://schema.org/InStock",
            "id": "_:b2",
            "price": "55.00",
            "priceCurrency": "USD",
            "type": "Offer"
        },
        {
            "account": "0xE6976A991A9C32aB665E1118Fd7cfDB58A23116d",
            "hash": "0x7bc087f4ef9d0dc15fef823bff9c78cc5cca8be0a85234afcfd807f412f40877",
            "id": "_:b3",
            "signature": "0x13a970137bd89ac8e812aafd049f74c1fa7138b9ed1b94a177a9c02af063038b39086b110b6751d3f18b4ba39cbeaaf506fed386828144f1826a4215a4499abc1c"
        },
        {
            "author": "Ellie",
            "datePublished": "2011-04-01",
            "id": "_:b4",
            "name": "Not a happy camper",
            "reviewBody": "The lamp burned out and now I have to replace it.",
            "reviewRating": {
                "bestRating": "5",
                "id": "_:b6",
                "ratingValue": "1",
                "type": "Rating",
                "worstRating": "1"
            },
            "type": "Review"
        },
        {
            "author": "Lucas",
            "datePublished": "2011-03-25",
            "id": "_:b5",
            "name": "Value purchase",
            "reviewBody": "Great microwave for the price. It is small and fits in my apartment.",
            "reviewRating": {
                "bestRating": "5",
                "id": "_:b7",
                "ratingValue": "4",
                "type": "Rating",
                "worstRating": "1"
            },
            "type": "Review"
        },
        {
            "bestRating": "5",
            "id": "_:b6",
            "ratingValue": "1",
            "type": "Rating",
            "worstRating": "1"
        },
        {
            "bestRating": "5",
            "id": "_:b7",
            "ratingValue": "4",
            "type": "Rating",
            "worstRating": "1"
        }
    ]
}
```

If JSON-LD type is supported on the network, the document should be framed according to the frame document. Otherwise, the result is framed by using the default (empty) frame document, as shown above.

#### Update an asset on the DKG

Assets on the DKG can be updated by providing the latest state for the asset:

```javascript
var result = await dkg.assets.update({
"@context": "https://schema.org",
"@type": "Product",
"description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
"name": "Kenmore Black 17\" Microwave",
"image": "kenmore-microwave-17in.jpg"
}, ual, {
        keywords: ['microwave'],
        visibility: 'public'
    })
```

The result of operation is the same as for `create` operation. The updated asset has different name, so in order to present the changes, let's retrieve the data from the proxy:

```javascript
console.log(await productProxy.data.valueOf);
```

The latest state of the product is:

```json5
{
    "@context": "https://www.schema.org/",
    "@graph": [
        {
            "description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
            "name": "Kenmore Black 17\" Microwave",
            "proof": {
                "account": "0xE6976A991A9C32aB665E1118Fd7cfDB58A23116d",
                "hash": "0x7bc087f4ef9d0dc15fef823bff9c78cc5cca8be0a85234afcfd807f412f40877",
                "id": "_:b1",
                "signature": "0x13a970137bd89ac8e812aafd049f74c1fa7138b9ed1b94a177a9c02af063038b39086b110b6751d3f18b4ba39cbeaaf506fed386828144f1826a4215a4499abc1c"
            },
            "type": "Product"
        },
        {
            "account": "0xE6976A991A9C32aB665E1118Fd7cfDB58A23116d",
            "hash": "0x7bc087f4ef9d0dc15fef823bff9c78cc5cca8be0a85234afcfd807f412f40877",
            "id": "_:b1",
            "signature": "0x13a970137bd89ac8e812aafd049f74c1fa7138b9ed1b94a177a9c02af063038b39086b110b6751d3f18b4ba39cbeaaf506fed386828144f1826a4215a4499abc1c"
        }
    ]
}
```

#### Search for an entity or an assertion on the DKG

DKG can be searched by keywords for related assets and assertions. Search result consists of elements listed by score and issuer.&#x20;

Entity search returns latest state of assets indexed by provided keywor:

```javascript
var result = dkg.search({ query: 'ExecutiveAnvil', resultType: 'entities' });
console.log(JSON.stringify(result));
```

The result the search is the following:

```javascript
{
    "@context": {
        "@vocab": "http://schema.org/",
        "goog": "http://schema.googleapis.com/",
        "resultScore": "goog:resultScore",
        "detailedDescription": "goog:detailedDescription",
        "EntitySearchResult": "goog:EntitySearchResult",
        "kg": "http://g.co/kg"
    },
    "@type": "ItemList",
    "itemListElement": [
        {
            "@type": "EntitySearchResult",
            "result": {
                "@id": "f7fb9c597ec04c1a7a6c1b03f5ef365ac7b47416b23e4c0772195175258266b8",
                "@type": "PRODUCT",
                "@context": "https://www.schema.org/",
                "@graph": [
                    {
                        "type": "Product",
                        "aggregateRating": {
                            "id": "_:b1",
                            "type": "AggregateRating",
                            "ratingValue": "4.4",
                            "reviewCount": "89"
                        },
                        "brand": {
                            "id": "_:b2",
                            "type": "Thing",
                            "name": "ACME"
                        },
                        "description": "Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.",
                        "image": "http://www.example.com/anvil_executive.jpg",
                        "mpn": "925872",
                        "name": "Executive Anvil",
                        "offers": {
                            "id": "_:b3",
                            "type": "Offer",
                            "availability": "http://schema.org/InStock",
                            "itemCondition": "http://schema.org/UsedCondition",
                            "price": "119.99",
                            "priceCurrency": "USD",
                            "priceValidUntil": "2020-11-05",
                            "seller": {
                                "id": "_:b4",
                                "type": "Organization",
                                "name": "Executive Objects"
                            }
                        }
                    },
                    {
                        "id": "_:b1",
                        "type": "AggregateRating",
                        "ratingValue": "4.4",
                        "reviewCount": "89"
                    },
                    {
                        "id": "_:b2",
                        "type": "Thing",
                        "name": "ACME"
                    },
                    {
                        "id": "_:b3",
                        "type": "Offer",
                        "availability": "http://schema.org/InStock",
                        "itemCondition": "http://schema.org/UsedCondition",
                        "price": "119.99",
                        "priceCurrency": "USD",
                        "priceValidUntil": "2020-11-05",
                        "seller": {
                            "id": "_:b4",
                            "type": "Organization",
                            "name": "Executive Objects"
                        }
                    },
                    {
                        "id": "_:b4",
                        "type": "Organization",
                        "name": "Executive Objects"
                    }
                ]
            },
            "issuers": [
                "0xbd084ab97c704fe4a6d620cb7c30c0be0366646f"
            ],
            "assertions": [
                "6b02bc68a44c255c0738b94a72a41ae2c0959e7e6a53554f90ec75ed6d7921de"
            ],
            "nodes": [
                "QmdD6AuWRoVpAjkxEtBgeUDUBaddNT3SD2cZo8sMV5CMn6"
            ],
            "resultScore": 0
        }
    ]
}
```

Assertion search returns assertions metadata of assets indexed by provided keyword:

```javascript
var result = dkg.search({ query: 'ExecutiveAnvil', resultType: 'assertions' });
console.log(JSON.stringify(result));
```

The result of Search API route is the following:

```json
{
    "@context": {
        "@vocab": "http://schema.org/",
        "goog": "http://schema.googleapis.com/",
        "resultScore": "goog:resultScore",
        "detailedDescription": "goog:detailedDescription",
        "EntitySearchResult": "goog:EntitySearchResult",
        "kg": "http://g.co/kg"
    },
    "@type": "ItemList",
    "itemListElement": [
        {
            "@type": "AssertionSearchResult",
            "result": {
                "@id": "6b02bc68a44c255c0738b94a72a41ae2c0959e7e6a53554f90ec75ed6d7921de",
                "metadata": {
                    "issuer": "0xbd084ab97c704fe4a6d620cb7c30c0be0366646f",
                    "type": "Product",
                    "timestamp": "2021-12-27T16:06:57.912Z",
                    "visibility": true,
                    "dataHash": "ed13153fa4090eceedf6c1dd1aa030ec45ab75c2f9510c64a2014f1c6424e7dd"
                },
                "signature": "0xbe37c15aa21835b9fe50b5225cfb61cd8ab3f06374705a91f5a5989105d2d2ec151c8bbb5d0f07c8508d37c77a15ac08456342d156ae52ced4520c15cb94eee91c",
                "rootHash": "45f04483daac38828d634d404e1a12d60d7b4749813edea7fd8b1701a725f37e"
            },
            "nodes": [
                "QmdD6AuWRoVpAjkxEtBgeUDUBaddNT3SD2cZo8sMV5CMn6"
            ],
            "resultScore": 0
        }
    ]
}
```

#### Executing SPARQL queries

Querying the DKG is done by using the SPARQL queries. The SPARQL construct query helps to get the response as a RDF graph. In case you are interested to create your own application, it will return portable graph described by the query:

```javascript
options = {
    query: `PREFIX schema: <http://schema.org/>
            CONSTRUCT { ?s ?p ?o }
            WHERE {
                GRAPH ?g {
                ?s ?p ?o .
                ?s schema:hasVisibility ?v
            }
        }`
};

var result = await dkg.query(options)
console.log(JSON.stringify(result));
```

The returned responses contain an array of n-quads with predicate `schema:hasVisibility`:

```javascript
{
  "status": "COMPLETED",
  "data": {
    "response": [
      "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasDataHash> \"019042b4b5cb5701579a4fd8e339bed0fa983b06920ed8cd4d5864ffcb01c801\" .",
      "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasIssuer> \"0xbd084ab97c704fe4a6d620cb7c30c0be0366646f\" .",
      "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasSignature> \"0x1303593aa18a94c54d85649915809f6f3849bd28ad3780b1ce458086f8547e10665dd3d8f2900724853fc5b6c34599d68657fa0f5bb3c7542f02673fc6e609b41b\" .",
      "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasTimestamp> \"2021-12-14T12:43:10.742Z\" .",
      "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasType> \"default\" .",
    ]
  }
}
```

#### Validate data integrity

Validate triples that you got performing SPARQL queries. We have chosen two triplets from above query result and we will check their integrity:

```javascript
options = {
    nquads: [
        '<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasDataHash> \"019042b4b5cb5701579a4fd8e339bed0fa983b06920ed8cd4d5864ffcb01c801\" .',
        '<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasIssuer> \"0xbd084ab97c704fe4a6d620cb7c30c0be0366646f\" .'
    ],
};

var result = await dkg.validate(options);
console.log(JSON.stringify(result));
```

The result presents an array that for each element indicates if the root hash matched or not:

```json
[
  {
    "triple": "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasDataHash> \"019042b4b5cb5701579a4fd8e339bed0fa983b06920ed8cd4d5864ffcb01c801\" .",
    "valid": true
  },
  {
    "triple": "<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasIssuer> \"0xbd084ab97c704fe4a6d620cb7c30c0be0366646f\" .",
    "valid": true
  }
]
```

More details about the library is available [here](https://github.com/OriginTrail/dkg.js).
