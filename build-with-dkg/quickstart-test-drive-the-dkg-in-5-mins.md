---
icon: flag-checkered
---

# Quickstart (test drive the DKG in 5 mins)

Welcome to your first hands-on experience with the **OriginTrail Decentralized Knowledge Graph (DKG)**! In just a few minutes, you'll **publish and retrieve your first** [**Knowledge Asset**](broken-reference) **(KA)** using [public DKG nodes](../useful-resources/public-nodes.md)—no setup required.

***

### What You’ll Do

You’ll use the [**DKG SDK**](chatdkg-builder-toolkit/dkg-sdk/) (JavaScript or Python) to:

* Connect to a public DKG node
* Publish a simple **Knowledge Asset**
* Retrieve that KA by querying the graph

{% hint style="info" %}
**No need to run your own node** — this quickstart uses public infrastructure so you can dive in instantly.
{% endhint %}

***

### What You’ll Need

* **Node.js** (for JavaScript SDK) or **Python** (3.8+)
* A Web3 wallet (e.g., MetaMask) with:
  * **Test TRAC tokens**
  * **Test Neuro tokens**
* A **public DKG node endpoint** which you can find [**here**](../useful-resources/public-nodes.md)

{% hint style="info" %}
Join our [Discord server](https://discord.com/channels/460837319025623050/1292225028330623108) and use our **faucet bot** to get free Test TRAC and Neuro tokens.\
Just type `!help` in the `#faucet-bot` channel to see the available commands and get started!
{% endhint %}

### Step 1: Install the SDK

Choose your preferred language:

**JavaScript (Node.js):**

```
npm install dkg.js@latest
```

**Python:**

```
pip install dkg
```

{% hint style="info" %}
Learn more about SDK in the [SDK Overview](chatdkg-builder-toolkit/dkg-sdk/)
{% endhint %}

### Step 2: Publish Your First Knowledge Asset

Here’s a super-simple JSON-LD Knowledge Asset:

```json
{
  "@context": "https://schema.org/",
  "@type": "CreativeWork",
  "name": "Hello DKG",
  "description": "My first Knowledge Asset on the Decentralized Knowledge Graph!"
}

```

Use the JavaScript SDK to publish it:

```javascript
import DKG from '../index.js';
import { BLOCKCHAIN_IDS, ENVIRONMENTS } from '../constants.js';
import 'dotenv/config';

const ENVIRONMENT = ENVIRONMENTS.TESTNET;
const OT_NODE_HOSTNAME = 'https://v6-pegasus-node-02.origin-trail.network';
const OT_NODE_PORT = '8900';
const PUBLIC_KEY = 'HERE-GOES-THE-ADDRESS-OF-YOUR-WALLET';

// IMPORTANT: Don't forget to add your PRIVATE_KEY to the .env file.
const DkgClient = new DKG({
    environment: ENVIRONMENT,
    endpoint: OT_NODE_HOSTNAME,
    port: OT_NODE_PORT,
    blockchain: {
        name: BLOCKCHAIN_IDS.NEUROWEB_TESTNET,
        publicKey: PUBLIC_KEY,
        privateKey: process.env.PRIVATE_KEY,
    },
    maxNumberOfRetries: 300,
    frequency: 2,
    contentType: 'all',
    nodeApiVersion: '/v1',
});

(async () => {
    const content = {
        public: {
            '@context': 'https://www.schema.org',
            '@id': 'urn:first-ka:info:hello-dkg',
            '@type': 'CreativeWork',
            'name': 'Hello DKG',
            'description': 'My first Knowledge Asset on the Decentralized Knowledge Graph!'
        },
    };

    const create_result = await DkgClient.asset.create(content, {
        epochsNum: 2,
        minimumNumberOfFinalizationConfirmations: 3,
        minimumNumberOfNodeReplications: 1,
    });

    console.log(JSON.stringify(create_result));
})();
```

Or you can use the Python SDK

```python
import json
import time

from dkg import DKG
from dkg.providers import BlockchainProvider, NodeHTTPProvider
from dkg.constants import Environments, BlockchainIds

node_provider = NodeHTTPProvider(
    endpoint_uri="https://v6-pegasus-node-02.origin-trail.network:8900",
    api_version="v1",
)
# make sure that you have PRIVATE_KEY in .env so the blockchain provider can load it
blockchain_provider = BlockchainProvider(
    Environments.DEVELOPMENT.value,
    BlockchainIds.HARDHAT_1.value,
)

config = {
    "max_number_of_retries": 300,
    "frequency": 2,
}
dkg = DKG(node_provider, blockchain_provider, config)

def print_json(json_dict: dict):
    print(json.dumps(json_dict, indent=4))
    
content = {
    "public": {
        '@context': 'https://www.schema.org',
        '@id': 'urn:first-ka:info:hello-dkg',
        '@type': 'CreativeWork',
        'name': 'Hello DKG',
        'description': 'My first Knowledge Asset on the Decentralized Knowledge Graph!'
    }
}

create_asset_result = dkg.asset.create(
    content=content,
    options={
        "epochs_num": 2,
        "minimum_number_of_finalization_confirmations": 3,
        "minimum_number_of_node_replications": 1,
        "token_amount": 100,
    },
)

print_json(create_asset_result)
```

### Step 3: Query & Retrieve the KA

Now that you've published your first Knowledge Asset, let's query the DKG to retrieve it using SPARQL.

Here’s how to fetch the `name` and `description` from your KA:

```javascript
const queryOperationResult = await DkgClient.graph.query(
    `
    PREFIX schema: <http://schema.org/>
    SELECT ?s ?name ?description
    WHERE {
        ?s schema:name ?name ;
           schema:description ?description .
    }
    `,
    'SELECT',
);

console.log('Query results:', queryOperationResult);
```

### What's Next?

**Explore the ChatDKG builder toolkit**

Everything you need to build with the DKG: publish and query knowledge, deploy autonomous AI agents, and launch decentralized knowledge ecosystems with paranets—[all from a unified toolkit](https://docs.origintrail.io/build-with-dkg/chatdkg-builder-toolkit).

**Build with your Edge Node**

Take control of your stack: deploy agents, paranets, and private Knowledge Assets on your own infrastructure—[fully customizable and privacy-first](dkg-edge-node/).

You’re now on the path to building a **semantic, decentralized, and AI-ready knowledge ecosystem**.
