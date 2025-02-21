---
description: >-
  You can find a simple example of the DKG Edge Node usage below to help you get
  started.
---

# Usage example

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
