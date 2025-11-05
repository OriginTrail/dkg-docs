# Custom DKG Python agent

This guide explains how to build a custom agent implementation using the [dkg.py](../../build-a-dkg-node-ai-agent/advanced-features-and-toolkits/dkg-sdk/dkg-v8-py-client/) SDK. AI agents can leverage the Decentralized Knowledge Graph (DKG) to create knowledge-graph-based, collective, persistent memory for individual agents or agentic swarms.

## Overview of dkg.py

dkg.py is a Python library for interacting with the DKG. It enables the creation, querying, and retrieval of structured knowledge assets stored in a decentralized and verifiable manner.

### Key Operations:

1. Create: Publish a knowledge asset to the DKG.
2. Query: Search for knowledge assets using structured queries.
3. Get: Retrieve a specific knowledge asset by its identifier.

Set up DKG.py as per the instructions [here](../../build-a-dkg-node-ai-agent/advanced-features-and-toolkits/dkg-sdk/dkg-v8-py-client/).

## **Use Case: AI Agent Memory**

### Creating Memory

AI agents can store structured knowledge or memory by creating knowledge assets in the DKG. For example, an agent can record user interactions or task results:

```python
memory_asset={
    "@context": "http://schema.org",
    "@type": "SocialMediaPosting",
    headline: "<describe memory in a short way, as a title here>",
    articleBody:
        "Check out this amazing project on decentralized cloud networks! @DecentralCloud #Blockchain #Web3",
    author: {
        "@type": "Person",
        "@id": "uuid:john:doe",
        name: "John Doe",
        identifier: "@JohnDoe",
        url: "https://twitter.com/JohnDoe",
    },
    dateCreated: "yyyy-mm-ddTHH:mm:ssZ",
    interactionStatistic: [
        {
            "@type": "InteractionCounter",
            interactionType: {
                "@type": "LikeAction",
            },
            userInteractionCount: 150,
        },
        {
            "@type": "InteractionCounter",
            interactionType: {
                "@type": "ShareAction",
            },
            userInteractionCount: 45,
        },
    ],
    mentions: [
        {
            "@type": "Person",
            name: "Twitter account mentioned name goes here",
            identifier: "@TwitterAccount",
            url: "https://twitter.com/TwitterAccount",
        },
    ],
    keywords: [
        {
            "@type": "Text",
            "@id": "uuid:keyword1",
            name: "keyword1",
        },
        {
            "@type": "Text",
            "@id": "uuid:keyword2",
            name: "keyword2",
        },
    ],
    about: [
        {
            "@type": "Thing",
            "@id": "uuid:thing1",
            name: "Blockchain",
            url: "https://en.wikipedia.org/wiki/Blockchain",
        },
        {
            "@type": "Thing",
            "@id": "uuid:thing2",
            name: "Web3",
            url: "https://en.wikipedia.org/wiki/Web3",
        },
        {
            "@type": "Thing",
            "@id": "uuid:thing3",
            name: "Decentralized Cloud",
            url: "https://example.com/DecentralizedCloud",
        },
    ],
    url: "https://twitter.com/JohnDoe/status/1234567890",
}

response = dkg.asset.create(memory_asset)
print("Memory Asset UAL:", response["UAL"])
```

### Querying Memory

Retrieve specific memories using queries based on metadata or content:

```python
query = """
SELECT DISTINCT ?headline ?articleBody
    WHERE {
      ?s a <http://schema.org/SocialMediaPosting> .
      ?s <http://schema.org/headline> ?headline .
      ?s <http://schema.org/articleBody> ?articleBody .


      OPTIONAL {
        ?s <http://schema.org/keywords> ?keyword .
        ?keyword <http://schema.org/name> ?keywordName .
      }


      OPTIONAL {
        ?s <http://schema.org/about> ?about .
        ?about <http://schema.org/name> ?aboutName .
      }


      FILTER(
        CONTAINS(LCASE(?headline), "example_keyword") ||
        (BOUND(?keywordName) && CONTAINS(LCASE(?keywordName), "example_keyword")) ||
        (BOUND(?aboutName) && CONTAINS(LCASE(?aboutName), "example_keyword"))
      )
    }
    LIMIT 10
"""

results = dkg.graph.query(query)
print("Retrieved Memories:", results)
```

### Retrieving Specific Memories

Use the get operation to fetch detailed information about a memory:

```python
response = dkg.asset.get(response.get("UAL"))
print("Memory Details:", response)

```

## Conclusion

Using dkg.py, AI agents can create persistent, verifiable, and decentralized memory. This functionality enables advanced use cases like long-term interaction tracking, knowledge storage, and retrieval. Start building smarter AI agents with dkg.py today!

For further assistance, refer to the rest of the documentation or contact the core development team.

\
