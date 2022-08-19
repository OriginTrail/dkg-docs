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
  endpoint: "http://127.0.0.1",
  port: 8900,
  useSSL: false,
  loglevel: "trace",
});

const result = await dkg.node.info();
console.log(JSON.stringify(result, null, 2));
```

In the code snippet above, after connecting to the node, the node info route will return the ot-node version. The result should look like this:

```json
{
  "version": "6.0.0-beta.2.0"
}
```

#### Create an asset

Asset presents a digital or physical object indexed on the DKG. Asset used in this tutorial is maintained by [schema.org](https://schema.org) can be found [here](https://schema.org/Product).

It follows the standard and contains an object of type `Product` __ with its description, name, image, and other details. An extensive documentation for Product class can be found here [https://schema.org/Product](https://schema.org/Product). The sample dataset values can be referred below:

<pre class="language-javascript"><code class="lang-javascript"><strong>const assertion = {
</strong>  "@context": "https://schema.org",
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
}</code></pre>

Index the asset with associated keywords. In this example, the keyword is `microwave`:

<pre class="language-javascript"><code class="lang-javascript"><strong>const { UAL } = await dkg.assets.create(assertion, {
</strong>    visibility: "public",
    holdingTimeInYears: 1,
    tokenAmount: 10,
    blockchain: {
      name: "otp",
      publicKey: PUBLIC_KEY,
      privateKey: PRIVATE_KEY,
    },
  })
console.log(UAL);</code></pre>

After returning the result, the asset's unique identifier (UAL) is logged. The complete response of the method is:

```javascript
{
  "UAL": "did:otp:0x6e002616adf12d4cc908976eb16a7646b6cd6596/2785",
  "assertionId": "0x8705b09bdca4ca23bf31f1048452cefea0b5f142ee72a7e09434ed4cc50a3b3e",
  "operation": {
    "operationId": "d97b4716-3feb-463c-acf5-9ca52cde3564",
    "status": "COMPLETED"
  }
}

```

#### Read an asset from the DKG

Data is persisted on the network by indexing and replicating on the DKG. Assets consist of building blocks entitled as assertions that are immutable and verifiable. Assets latest assertion could be resolved from the network by using UAL.

```javascript
const { assertion } = await dkg.assets.get(UAL);

console.log(JSON.stringify(data, null, 2));
```

The response response of the asset's data is:

```javascript
{
    "@context": "http://schema.org/",
    "@graph": [
      {
        "id": "_:c14n0",
        "type": "Product",
        "aggregateRating": {
          "id": "_:c14n4"
        },
        "description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
        "name": "Kenmore White 17\" Microwave",
        "offers": {
          "id": "_:c14n5"
        },
        "review": [
          {
            "id": "_:c14n2"
          },
          {
            "id": "_:c14n3"
          }
        ]
      },
      {
        "id": "_:c14n1",
        "type": "Rating",
        "bestRating": "100",
        "ratingValue": {
          "type": "xsd:double",
          "@value": "5.935915107714318E0"
        },
        "worstRating": "0"
      },
      {
        "id": "_:c14n2",
        "type": "Review",
        "author": "Ellie",
        "datePublished": "2011-04-01",
        "name": "Not a happy camper",
        "reviewBody": "The lamp burned out and now I have to replace it.",
        "reviewRating": {
          "id": "_:c14n6"
        }
      },
      {
        "id": "_:c14n3",
        "type": "Review",
        "author": "Lucas",
        "datePublished": "2011-03-25",
        "name": "Value purchase",
        "reviewBody": "Great microwave for the price. It is small and fits in my apartment.",
        "reviewRating": {
          "id": "_:c14n1"
        }
      },
      {
        "id": "_:c14n4",
        "type": "AggregateRating",
        "ratingValue": "1.1",
        "reviewCount": "11"
      },
      {
        "id": "_:c14n5",
        "type": "Offer",
        "availability": "https://schema.org/InStock",
        "price": "55.00",
        "priceCurrency": "USD"
      },
      {
        "id": "_:c14n6",
        "type": "Rating",
        "bestRating": "5",
        "ratingValue": "1",
        "worstRating": "1"
      }
    ]
  }
```



#### Update an asset on the DKG

Assets on the DKG can be updated by providing the latest state for the asset:

```javascript
const { UAL } = await dkg.assets.update(UAL, {
"@context": "https://schema.org",
"@type": "Product",
"description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
"name": "Kenmore Black 17\" Microwave",
"image": "kenmore-microwave-17in.jpg"
}, {
    visibility: "public",
    holdingTimeInYears: 1,
    tokenAmount: 10,
    blockchain: {
      name: "otp",
      publicKey: PUBLIC_KEY,
      privateKey: PRIVATE_KEY,
    },
  })
```

The result of the operation is the same as for the `create` operation. The updated asset has different name, so in order to present the changes, let's retrieve the data from the proxy:

```javascript
const { assertion } = await dkg.assets.get(UAL);

console.log(JSON.stringify(data, null, 2));
```

The latest state of the product is now:

<pre class="language-json5"><code class="lang-json5">{
  "@context": "https://schema.org",
  "@type": "Product",
  "description": "0.7 cubic feet countertop microwave. Has six preset cooking categories and convenience features like Add-A-Minute and Child Lock.",
<strong>  "name": "Kenmore Black 17\" Microwave",
</strong>  "image": "kenmore-microwave-17in.jpg"
}</code></pre>

#### Search for an entity or an assertion on the DKG (To be updated soon)

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

#### Executing SPARQL queries (To be updated soon)

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

More details about the library is available [here](https://github.com/OriginTrail/dkg.js).
