# Example flow: Publishing Product Dataset, Resolving, Searching on the DKG and Querying via SPARQL

This page intends to introduce a basic flow of:

* publishing a dataset to the DKG
* resolving a dataset to the DKG
* searching for it via the search API
* querying using SPARQL

More instructions will be provided through the documentation in the following updates.

### How to publishing product dataset on DKG?

**Dataset Description**

The dataset is maintained by jsonld.com can be found here [https://jsonld.com/product/](https://jsonld.com/product/)&#x20;

It follows Schema.org as standard and contains an object of type _Product_ with its description, identifier, brand, rating and other details. An extensive documentation for Product class can be found here [https://schema.org/Product](https://schema.org/Product). The sample dataset values can be referred below:

```
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

Save the above dataset as Product.json (to be passed in API).

#### Publishing via Publish API

In this tutorial, we are going to publish the above Product dataset with the Publish API:

```javascript
POST http://NODE_IP:PORT/publish

//Save the above dataset as Product.json and pass the path in files variables
payload= {
'assets': '["0x123456789123456789123456789"]',
'keywords': '["Product", "Executive Objects", "ACME"]',
'visibility': 'true'}

files=[
  ('file',('Product.json',open('{LocalPATH}/Product.json','rb'),'application/json'))
]
```

#### Getting Assertion\_ID after successful publish operation

On successful publish, the response will generate a handler\_id which can be further used as a parameter for below API:

```javascript
POST http://NODE_IP:PORT/publish/result/${handler_id}
```

As a result, user will get the following response for publishing the dataset successfully. The assertion\_id(id) can be used for Resolve in next section.&#x20;

```javascript
{
    "status": "COMPLETED",
    "data": {
        "id": "f44199fdc034a105a538e5f8f86fb0418b5ac6b80a537176d55e900ce53720b9",
        "rootHash": "f29afc26528610294a426015a30fdac7cefaf32f6002cf8f934bce14e951566a",
        "signature": "0x44694dc8f3ea5abcf0054a5437e517eefad6aab7e9aaf881227dcd253237a7961e9fb11a7d99af9e7baba885626f70ead66c3e3b9d57595ff57a263b0560ac101c",
        "metadata": {
            "type": "Person",
            "timestamp": "2021-12-24T10:20:12.881Z",
            "issuer": "0xbd084ab97c704fe4a6d620cb7c30c0be0366646f",
            "visibility": true,
            "dataHash": "c8817ca24382818180a978fb1e628904ea4abd0a9d526ad2ca0aa9ad552b4283"
        }
    }
}
```

## How to resolve an assertion on the DKG?

Data are persisted on the network by publishing on the DKG. Data are published as assertions that are immutable and verifiable, which could be resolved using assertion ID. Assertion ID is signed hash of published triples which is calculated during the publish.

#### Resolving via Resolve API

In this tutorial, we are going to resolve the above Product assertion with the Resolve API using /resolve and /resolve/result API routes:

```
GET http://NODE_IP:PORT/resolve?ids={assertion_id}
```

The above will generate a handler\_id which can be used in API below to get Resolve result.

```
curl --location --request GET 'http://127.0.0.1:8901/resolve/result/${handler_id}'
```

The result of Resolve API route is the following:

```
{
    "metadata": {
        "dataHash": "ed13153fa4090eceedf6c1dd1aa030ec45ab75c2f9510c64a2014f1c6424e7dd",
        "issuer": "0xbd084ab97c704fe4a6d620cb7c30c0be0366646f",
        "timestamp": "2021-12-27T16:06:57.912Z",
        "type": "Product",
        "visibility": true
    },
    "blockchain": {
        "name": "polygon::testnet",
        "transactionHash": "0x16dbb9117d566a9ecc62dabb3175782a425e466b4abfa138986f357cacc9909f"
    },
    "assets": [
        "f7fb9c597ec04c1a7a6c1b03f5ef365ac7b47416b23e4c0772195175258266b8"
    ],
    "keywords": [
        "Product",
        "0x1242356452",
        "executive anvil"
    ],
    "signature": "0xbe37c15aa21835b9fe50b5225cfb61cd8ab3f06374705a91f5a5989105d2d2ec151c8bbb5d0f07c8508d37c77a15ac08456342d156ae52ced4520c15cb94eee91c",
    "rootHash": "45f04483daac38828d634d404e1a12d60d7b4749813edea7fd8b1701a725f37e",
    "id": "6b02bc68a44c255c0738b94a72a41ae2c0959e7e6a53554f90ec75ed6d7921de",
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
```

Data integrity could be verified by calculating _sha256(sha256(metadata)sha256(data))._

## How to search for an entity or an assertion on the DKG?

DKG can be searched by keywords for related assets and assertions. Search result consists of elements listed by score and issuer.

#### Searching for an entity via Search API

In this tutorial, we are going to search the above Product entity using /entities:search and /entities:search/result API routes:

```
curl --location --request GET 'http://127.0.0.1:8901/entities:search?prefix=true&limit=20&query=ExecutiveAnvil'
```

The result of Search API route is the following:

```
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

#### Searching for an assertion via Search API

In this tutorial, we are going to search the above Product entity using /entities:search and /entities:search/result API routes:

```
curl --location --request GET 'http://127.0.0.1:8901/assertions:search?prefix=true&limit=20&query=ExecutiveAnvil'
```

The result of Search API route is the following:

```
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

### How to run SPARQL queries on DKG?

The DKG querying entails both data discovery and graph querying. Therefore OriginTrail implements a set of protocols for discovery and exchange which cover a wide array of possible scenarios. This section covers querying through SPARQL constrict.

### SPARQL query

Querying the DKG is done using the SPARQL query API. It is used to look up all datasets containing a specific identifier/Value.&#x20;

The SPARQL Construct query helps to get the response as a RDF sub-graph. In case users are interested to create their own application, this returned portable sub-graph contains all of the information needed to build a section of application. Then instead of many select queries to the full database, these queries can be run over the much smaller sub-graph returned by the construct query.

**Using the API with a sample construct query (Dataset having seller with name 'Executive Objects')**

```
POST http://NODE_IP:PORT/query?type=construct

//provide all the connected properties and values for an object having sellername 
//'Executive Objects'

payload=
{'query': 'PREFIX schema: <http://schema.org/>
construct { ?s ?p ?o}
WHERE { 
GRAPH ?g {?s ?p ?o .
    ?s schema:offers / schema:seller/ schema:name "Executive Objects" .
}
}'}
}' \
```

The returned responses contain query\_id which can be used to fetch responses from network query.

To view responses call the query response API, as a parameter use query\_id returned from network query API call.

```javascript
GET http://NODE_IP:PORT/query/result/{query_id}
```

The returned responses contain an array of all connected nodes for returned dataset which contain objects whose identifiers(or value) fit the given query.&#x20;

```javascript
{
    "status": "COMPLETED",
    "data": {
        "response": [
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://schema.org/Product> .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/description> \"Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.\" .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/name> \"Executive Anvil\" .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/aggregateRating> _:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n4 .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/brand> _:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n2 .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/image> <http://www.example.com/anvil_executive.jpg> .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/mpn> \"925872\" .",
            "_:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n0 <http://schema.org/offers> _:genid2dfbcb2d181a59423e9a3ec6cf297826782dc14n3 .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://schema.org/Product> .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/description> \"Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.\" .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/name> \"Executive Anvil\" .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/aggregateRating> _:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n4 .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/brand> _:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n2 .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/image> <http://www.example.com/anvil_executive.jpg> .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/mpn> \"925872\" .",
            "_:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n0 <http://schema.org/offers> _:genid2d7b11008feb8e454cafcdb8b6d5666d722dc14n3 .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://schema.org/Product> .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/description> \"Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.\" .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/name> \"Executive Anvil\" .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/aggregateRating> _:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n4 .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/brand> _:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n2 .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/image> <http://www.example.com/anvil_executive.jpg> .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/mpn> \"925872\" .",
            "_:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n0 <http://schema.org/offers> _:genid2d35b7d44ec4b6485aacfbe6cb27db3eca2dc14n3 ."
        ]
    }
}
```

****

###
