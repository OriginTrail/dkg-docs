---
description: >-
  Create your first Knowledge Asset on OriginTrail Decentralized Knowledge Graph
  using the DKG Python SDK
icon: python
---

# Quickstart with Python

## 🚀 Step 1: Set up your project and install the SDK

### 1.1 Create your project folder

1. Create a new folder on your computer named `OT-DKG-Quickstart`
2. Open the folder in your code editor:
   * **VS Code**: File → Open Folder → Select `OT-DKG-Quickstart`
   * **Cursor**: File → Open → Select `OT-DKG-Quickstart`

### 1.2 Open a terminal in your project folder

* **VS Code**: Right-click the folder in Explorer → "Open in Integrated Terminal"
* **Cursor**: Click the folder → "Open Terminal Here"

### 1.3 Initialize project and install SDK

```bash
# Create a virtual environment
python -m venv env

# Activate virtual environment
# On Mac/Linux:
source env/bin/activate
# On Windows:
env\Scripts\activate

# Install the DKG SDK
pip install dkg
```

### 1.4 Set up your private key

1. Create a new file named `.env` in your project root
2. Add your wallet's private key:

```
PRIVATE_KEY="your_private_key_here"
```

{% hint style="warning" %}
**Note**: Replace `your_private_key_here` with your actual private key. Never share this file or commit it to version control!
{% endhint %}

> **How to get your private key from MetaMask**:
>
> 1. Open MetaMask
> 2. Click the three dots menu
> 3. Select "Account Details"
> 4. Click "Export Private Key"
> 5. Enter your password and copy the key

## 📝 Step 2: Publish your first knowledge asset

A Knowledge Asset (KA) is structured data stored on the DKG. Let's create a simple one!

### Example Knowledge Asset

Here's an example of Klowledge Asset written in JSON-LD format.



<pre class="language-json"><code class="lang-json"><strong>{
</strong>  "@context": "https://schema.org/",
  "@type": "CreativeWork",
  "@id": "urn:first-dkg-ka:info:hello-dkg",
  "name": "Hello DKG",
  "description": "My first Knowledge Asset on the Decentralized Knowledge Graph!"
}
</code></pre>

{% hint style="info" %}
💡 Tip: You can customize the `name` and `description` fields with your own content! Make sure to also change the last part of the `@id` (e.g., from "hello-dkg" to "my-asset-name") to keep your asset unique for querying later!
{% endhint %}

### Python implementation

1. Create a new file named `publish_ka.py` in your project folder
2. Copy and paste this code, replacing the content part with your custom values if you'd like:

```python
import json
import time

from dkg import DKG
from dkg.providers import BlockchainProvider, NodeHTTPProvider
from dkg.constants import BlockchainIds

node_provider = NodeHTTPProvider(
    endpoint_uri="https://v6-pegasus-node-02.origin-trail.network:8900",
    api_version="v1",
)

blockchain_provider = BlockchainProvider(
    BlockchainIds.NEUROWEB_TESTNET.value,
)

config = {
    "max_number_of_retries": 300,
    "frequency": 2,
}
dkg = DKG(node_provider, blockchain_provider, config)

content = {
    "public": {
        "@context": "https://www.schema.org",
        "@id": "urn:first-dkg-ka:info:hello-dkg",
        "@type": "CreativeWork",
        "name": "Hello DKG",  # 🎯 Remember this name for querying!
        "description": "My first Knowledge Asset on the Decentralized Knowledge Graph!"
    }
}

print("Publishing Knowledge Asset...")

create_asset_result = dkg.asset.create(content, {
    "epochs_num": 2,
    "minimum_number_of_finalization_confirmations": 3,
    "minimum_number_of_node_replications": 1
})

print("Success! Your Knowledge Asset has been published:")
print(json.dumps(create_asset_result, indent=4))
```

3. Run the script by entering the following into the terminal:

```bash
python publish_ka.py
```

{% hint style="info" %}
**Note**: On some systems, like Mac and Linux, you may need to use `python3` instead of `python` , depending on your setup
{% endhint %}

{% hint style="info" %}
⏳ **Note**: Publishing might take 30-60 seconds. You'll see a success message with details about your KA!
{% endhint %}

## 🔍 Step 3: Query & Retrieve Your Knowledge Asset

Now let's retrieve your published Knowledge Asset using a SPARQL query.

1. Create a new file in your project folder named `query_ka.py` , paste in the code below, and update the query name if you changed the name of the KA when creating it:

```python
import json
import os
from dkg import DKG
from dkg.providers import BlockchainProvider, NodeHTTPProvider
from dkg.constants import BlockchainIds

node_provider = NodeHTTPProvider(
    endpoint_uri="https://v6-pegasus-node-02.origin-trail.network:8900",
    api_version="v1",
)

blockchain_provider = BlockchainProvider(
    BlockchainIds.NEUROWEB_TESTNET.value,
)

config = {
    "max_number_of_retries": 300,
    "frequency": 2,
}

dkg = DKG(node_provider, blockchain_provider, config)

# ⚠️ IMPORTANT: Update "hello dkg" if you changed the name when publishing!
query = '''
    PREFIX schema: <http://schema.org/>
    SELECT ?s ?name ?description
    WHERE {
        ?s schema:name ?name ;
           schema:description ?description .
        FILTER(LCASE(?name) = "hello dkg")
    }
'''

print("Querying for your Knowledge Asset...")

try:
    query_result = dkg.graph.query(query)
    print("Found your Knowledge Asset!")
    print(json.dumps(query_result, indent=4))
except Exception as e:
    print(f"Error querying the asset: {e}")
    print("Tip: Make sure the name in your query matches the name you used when publishing!")
```

2. Run the query by entering the following into your terminal:&#x20;

```bash
python query_ka.py
```

{% hint style="info" %}
**Note**: On some systems, like Mac and Linux, you may need to use `python3` instead of `python` , depending on your setup
{% endhint %}

#### ⚠️ Query Troubleshooting

If your query returns no results:

1. **Check the name**: Ensure the name in your SPARQL query exactly matches what you published
2. **Wait a moment**: Sometimes it takes a few seconds for the KA to be fully indexed
3. **Verify publication**: Check that your publish script completed successfully

Example: If you changed the name to "My Custom KA", update your query:

```sparql
FILTER(LCASE(?name) = "my custom ka")
```

## 🎉 Congratulations!

You've successfully:

* Published your first Knowledge Asset to the DKG
* Created a verifiable, ownable asset that you control
* Retrieved it using a SPARQL query
* Learned the basics of the OriginTrail SDK

Your **Knowledge Asset now lives on the DKG**, where it's:

* **Owned by you -** secured by your wallet
* **Verifiable -** anyone can cryptographically verify you as the publisher
* **Discoverable -** can be found by anyone while you maintain ownership

## 🚀 What's Next?

Now that you've mastered the basics, here's what comes next.

[**Explore the ChatDKG builder toolkit**](../dkg-toolkit/)

Everything you need to build with the DKG: publish and query knowledge, deploy autonomous AI agents, and launch decentralized knowledge ecosystems with paranets—all from a unified toolkit.

[**Build with your Edge Node**](../dkg-edge-node/)

Take control of your stack: deploy agents, paranets, and private Knowledge Assets on your own infrastructure—fully customizable and privacy-first.



You’re now on the path to building a **semantic, decentralized, and AI-ready knowledge ecosystem!**
