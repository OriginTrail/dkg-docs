---
description: >-
  You can find a simple example of the DKG Edge Node usage below to help you get
  started.
---

# Usage example

This page demonstrates a **simple end-to-end example** of how you can process any kind of JSON data using the **example pipeline provided in the Knowledge Mining service**, and then **ask questions about that data** through the **AI Assistant** interface. The AI Assistant communicates directly with the **DRAG** (Decentralized Retrieval-Augmented Generation) module, for which we’ve also prepared a basic example to showcase its functionality.

> **Note:** This is a simplified example meant to demonstrate the concept and basic flow.

## Purpose of the Example

The goal of this example is to provide a quick and intuitive way to explore the potential of the **DKG Edge Node** through the UI. It’s designed to help you understand:

* How input data (in standard JSON format) can be processed through a Knowledge Mining pipeline to generate structured graph data in JSON-LD or N-Quads format.
* How this graph-structured output is published to the OriginTrail Decentralized Knowledge Graph (DKG) as a Knowledge Asset – making the data verifiable, discoverable, and ensuring data integrity and ownership.
* How AI-powered question answering is performed on top of these Knowledge Assets through the DRAG service, which builds RAG (Retrieval-Augmented Generation) systems on decentralized data using powerful LLMs.

## Focused on UI

To keep things as accessible as possible, this example focuses purely on **UI-based usage**. If you're looking to explore **programmatic interaction** with the services (e.g., building custom pipelines, publishing data, or querying via APIs), please refer to the dedicated **API Documentation** section.

#### Note on Simplicity

This example is intentionally basic and does **not represent a production-ready pipeline**. Instead, it serves to highlight what’s possible when using:

* Knowledge Mining Pipelines – for transforming raw inputs into semantically rich formats (e.g., JSON-LD).
* Edge Node API – for publishing structured data to the Decentralized Knowledge Graph (DKG).
* Edge Node DRAG – for creating RAG (Retrieval-Augmented Generation) applications based on verifiable, decentralized data.

The main idea is that users can **build their own Knowledge Mining workflows** tailored to their domain-specific data and leverage the DKG infrastructure for secure, decentralized, and intelligent knowledge applications.

## Interacting with the Web UI

You can access the user interface at _<mark style="color:blue;">http://your-nodes-ip-address</mark>_.&#x20;

### Logging in

When accessing your node endpoint, you will be redirected to the login page.

{% hint style="info" %}
The default login credentials are as follows:

**username:** my\_edge\_node

**password:** edge\_node\_pass
{% endhint %}

### Publishing a Knowledge Asset

We have prepared a simple example, which is processing JSON files that represent movies.

Example JSON for a movie:

```json
{
    "title": "The Terminator",
    "release_year": 1984,
    "genre": [
        "Action",
        "Sci-Fi",
        "Thriller"
    ],
    "director": "James Cameron",
    "writers": [
        "James Cameron",
        "Gale Anne Hurd",
        "William Wisher"
    ],
    "cast": [
        {
            "actor": "Arnold Schwarzenegger",
            "role": "The Terminator"
        },
        {
            "actor": "Linda Hamilton",
            "role": "Sarah Connor"
        },
        {
            "actor": "Michael Biehn",
            "role": "Kyle Reese"
        },
        {
            "actor": "Paul Winfield",
            "role": "Lieutenant Ed Traxler"
        }
    ],
    "plot": "A cyborg assassin, known as a Terminator, is sent back from the future to kill Sarah Connor, a woman whose unborn son will lead humanity in a war against machines. A soldier from the future is sent back to protect her.",
    "runtime": "107 minutes",
    "language": "English",
    "country": "USA",
    "imdb_rating": 8.1,
    "imdb_link": "https://www.imdb.com/title/tt0088247/"
}
```

{% hint style="info" %}
You can create any kind of JSON representing a book, movie, or music following the example above.
{% endhint %}

Go to _<mark style="color:blue;">http://your-nodes-ip-address/contribute</mark>_ and upload your JSON.

{% hint style="info" %}
If you are using WSL, the node's IP address will be the IP address of the virtual machine.
{% endhint %}

The Edge Node will:

1. Process your input file and create a JSON-LD out of it.
2. Publish the Knowledge Asset on the Decentralized Knowledge Graph (DKG) from that JSON-LD.

### Passing a query

After successfully creating the Knowledge Asset, go to _<mark style="color:blue;">http://your-nodes-ip-address/ai-assistant</mark>,_ and ask the AI Assistant a question about the movie (or other work) you put in the JSON to see how it works.

> If you don’t get a good answer right away, feel free to tweak  [JSON Knowledge pipeline](https://github.com/OriginTrail/edge-node-knowledge-mining/blob/main/dags/simple_json_to_jsonld.py) — this is just an **example pipeline**, and it may not work perfectly with every type of JSON structure out of the box.
