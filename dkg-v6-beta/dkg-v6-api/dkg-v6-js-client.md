# DKG v6 JS client

This page intends to introduce a basic flow using [dkg-client](https://github.com/OriginTrail/dkg-client/tree/v6/develop):

* publishing a dataset to the DKG
* resolving a dataset to the DKG
* searching for it via the search API
* querying using SPARQL
* validating triplets

### Installation

You can install DKG client in you project by executing next command in your project root directory:

```bash
npm install dkg-client@beta.1
```

### Initialization of client

To use DKG client we need to have OT-node v6 endpoint, you can run it locally or [setup a node](https://docs.origintrail.io/dkg-v6-upcoming-version/setup-instructions-dockerless) that will be part of public beta DKG.

In the code snippet below we will enter our node hostname and port, and after connecting to our node we will perform informations about node just to confirm that everything is working fine.

```javascript
const DKGClient = require('dkg-client');

const OT_NODE_HOSTNAME = '0.0.0.0';
const OT_NODE_PORT = '8900';

// initialize connection to your DKG Node
let options = { endpoint: OT_NODE_HOSTNAME, port: OT_NODE_PORT, useSSL: false, loglevel: 'info' };
const dkg = new DKGClient(options);

// get info about endpoint that you are connected to
dkg.nodeInfo().then(result => console.log(result));
```

### Publishing product dataset on DKG

**Dataset Description**

The dataset used in this tutorial is maintained by jsonld.com can be found here [https://jsonld.com/product/](https://jsonld.com/product/)&#x20;

It follows Schema.org as standard and contains an object of type _Product_ with its description, identifier, brand, rating and other details. An extensive documentation for Product class can be found here [https://schema.org/Product](https://schema.org/Product). The sample dataset values can be referred below:

```json
{
  "@context": "https://schema.org/",
  "@type": "Product",
  "name": "Executive Anvil",
  "image": "http://www.example.com/anvil_executive.jpg",
  "description": "Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.",
  "mpn": "925872",
  "brand": {
    "@type": "Thing",
    "name": "ACME"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.4",
    "reviewCount": "89"
  },
  "offers": {
    "@type": "Offer",
    "priceCurrency": "USD",
    "price": "119.99",
    "priceValidUntil": "2020-11-05",
    "itemCondition": "http://schema.org/UsedCondition",
    "availability": "http://schema.org/InStock",
    "seller": {
      "@type": "Organization",
      "name": "Executive Objects"
    }
  }
}
```

Save the above dataset as Product.json

#### Publishing the dataset

We can also publish the above Product dataset with the publish method in the client:

```javascript
options = { 
    filepath: '{LocalPATH}/Product.json', 
    assets: ['0x123456789123456789123456789'],
    keywords: ['Product', 'Executive Objects', 'ACME'],
    visibility: "public"
};

dkg.publish(options).then((result) => {
    console.log(JSON.stringify(result))
});
```

As a result, user will get the following response for publishing the dataset successfully.&#x20;

```javascript
{
  status: 'COMPLETED',
  data: {
    id: '0b2f32a380f61fda8a3b2461074183dfbc9e19c0cbb59275969e6370aa5b26cf',
    rootHash: '94ad72c79a88fd2da048cc8c4b3abbdc2cd507ab4b9fccfacd9eae0f8907dac3',
    signature: '0x2a036001d2ca32fb2e528d6e8c414ab86f5b000e87558ae9c75a74c46bcd4fc16d47e865412341640b3d81e05fd2e4ed9f96d63188ad28476b276ba1d7c06d581b',
    metadata: {
      type: 'Product',
      timestamp: '2021-12-30T13:08:14.770Z',
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

The assertion\_id_(id) above can be used for Resolve in next section._&#x20;

### Resolve an assertion on the DKG

Data are persisted on the network by publishing on the DKG. Data are published as assertions that are immutable and verifiable, which could be resolved using assertion ID. Assertion ID is signed hash of published triples which is calculated during the publish.

```javascript
options = {
    ids: [
        '066787bc7269c062fe73b0ebb004c258e07151777e6dfba027fea046df5caf7c',
        '0b2f32a380f61fda8a3b2461074183dfbc9e19c0cbb59275969e6370aa5b26cf'
    ]
};
    
dkg.resolve(options).then((result) => {
    console.log(JSON.stringify(result));
});
```

The result of above is the following:

```javascript
{
  "status": "COMPLETED",
  "data": [
    {
      "066787bc7269c062fe73b0ebb004c258e07151777e6dfba027fea046df5caf7c": {
        "metadata": {
          "dataHash": "ed13153fa4090eceedf6c1dd1aa030ec45ab75c2f9510c64a2014f1c6424e7dd",
          "issuer": "0xbd084ab97c704fe4a6d620cb7c30c0be0366646f",
          "timestamp": "2021-12-29T15:33:00.932Z",
          "type": "Product",
          "visibility": true
        },
        "blockchain": {
          "name": "polygon::testnet",
          "transactionHash": "0xa413f4e75f4e858663a45db717a800d2034334fac107791d47158884fe4a712b"
        },
        "assets": [
          "2cb2b246cae224b372d36f10ceae1447597fbb129b8a98c18465a6e2f65444cb"
        ],
        "keywords": [
          "Product",
          "executiveanvil",
          "product,executive objects,acme"
        ],
        "signature": "0xfaf131689de19ddebf8b1fc4068274d5d60fc9d050273515292152a4758f886251d80eeb9289fe07f662314b624187f7452a93f5147f5bc26630475b6698548d1c",
        "rootHash": "c9309614ff33632620fe3904364c92bd1b379ebf59ef16aec69153d92975387b",
        "id": "066787bc7269c062fe73b0ebb004c258e07151777e6dfba027fea046df5caf7c",
        "data": {
          "@context": "https://www.schema.org/",
          "@graph": [
            {
              "aggregateRating": {
                "id": "_:b1",
                "ratingValue": "4.4",
                "reviewCount": "89",
                "type": "AggregateRating"
              },
              "brand": {
                "id": "_:b2",
                "name": "ACME",
                "type": "Thing"
              },
              "description": "Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.",
              "image": "http://www.example.com/anvil_executive.jpg",
              "mpn": "925872",
              "name": "Executive Anvil",
              "offers": {
                "availability": "http://schema.org/InStock",
                "id": "_:b3",
                "itemCondition": "http://schema.org/UsedCondition",
                "price": "119.99",
                "priceCurrency": "USD",
                "priceValidUntil": "2020-11-05",
                "seller": {
                  "id": "_:b4",
                  "name": "Executive Objects",
                  "type": "Organization"
                },
                "type": "Offer"
              },
              "type": "Product"
            },
            {
              "id": "_:b1",
              "ratingValue": "4.4",
              "reviewCount": "89",
              "type": "AggregateRating"
            },
            {
              "id": "_:b2",
              "name": "ACME",
              "type": "Thing"
            },
            {
              "availability": "http://schema.org/InStock",
              "id": "_:b3",
              "itemCondition": "http://schema.org/UsedCondition",
              "price": "119.99",
              "priceCurrency": "USD",
              "priceValidUntil": "2020-11-05",
              "seller": {
                "id": "_:b4",
                "name": "Executive Objects",
                "type": "Organization"
              },
              "type": "Offer"
            },
            {
              "id": "_:b4",
              "name": "Executive Objects",
              "type": "Organization"
            }
          ]
        }
      }
    }
  ]
}
```

Data integrity could be verified by calculating _sha256(sha256(metadata)sha256(data))._

### Search for an entity or an assertion on the DKG

DKG can be searched by keywords for related assets and assertions. Search result consists of elements listed by score and issuer.

#### Search for entities:

```javascript
options = { query: 'ExecutiveAnvil', resultType: 'entities' };

dkg.search(options).then((result) => {
    console.log(JSON.stringify(result));
});
```

The result of Search API route is the following:

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

#### Search for assertions

```javascript
options = { query: 'ExecutiveAnvil', resultType: 'assertions' };

dkg.search(options).then((result) => {
    console.log(JSON.stringify(result));
});
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

### SPARQL query

Querying the DKG is done using the SPARQL query API. It is used to look up all datasets containing a specific identifier/Value.&#x20;

The SPARQL Construct query helps to get the response as a RDF sub-graph. In case users are interested to create their own application, this returned portable sub-graph contains all of the information needed to build a section of application. Then instead of many select queries to the full database, these queries can be run over the much smaller sub-graph returned by the construct query.

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

dkg.query(options).then((result) => {
    console.log(JSON.stringify(result));
});
```

The returned responses contain an array of all connected nodes for returned dataset which contain objects whose identifiers(or value) fit the given query.&#x20;

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

### Validation

Using DKG client you can validate triples that you got performing SPARQL queries. We have chosen two triplets from above query result and we will check their integrity:

```javascript
options = {
    nquads: [
        '<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasDataHash> \"019042b4b5cb5701579a4fd8e339bed0fa983b06920ed8cd4d5864ffcb01c801\" .',
        '<did:dkg:43a5f8c55600a36882f9bac7c69c05a3e0edd1293b56b8024faf3a29d8157435> <http://schema.org/hasIssuer> \"0xbd084ab97c704fe4a6d620cb7c30c0be0366646f\" .'
    ],
};

dkg.validate(options).then((result) => {
    console.log(JSON.stringify(result));
});
```

Expected output:

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

