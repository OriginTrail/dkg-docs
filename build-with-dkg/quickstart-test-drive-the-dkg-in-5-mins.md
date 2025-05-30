---
icon: flag-checkered
---

# Quickstart (test drive the DKG in 5 mins)

Welcome to your first hands-on experience with the **OriginTrail Decentralized Knowledge Graph (DKG)**! In just a few minutes, you'll **publish and retrieve your first** [**Knowledge Asset**](broken-reference) **(KA)** using [public DKG nodes](../useful-resources/public-nodes.md)—no complex setup required.

***

### What you’ll do

### ✨ What you'll accomplish

You'll use the [**DKG SDK** ](dkg-toolkit/dkg-sdk/)(JavaScript or Python) to:

* Connect to a [public DKG node](../useful-resources/public-nodes.md)
* Publish a simple **Knowledge Asset (KA)**
* Retrieve that KA by querying the DKG

{% hint style="info" %}
**No need to run your own node** — we'll use public infrastructure so you can dive in instantly!
{% endhint %}

***

### What you’ll need

* **Node.js** (for JavaScript SDK) or **Python** (3.8+)
* A Web3 wallet (e.g., MetaMask) with:
  * **Test TRAC tokens**
  * **Test Neuro tokens**
* A **public DKG node endpoint,** which you can find [**here**](../useful-resources/public-nodes.md)

### Step 2: Publish your first Knowledge Asset

### Step 3: Query & retrieve the Knowledge Asset

Or you can use the Python SDK:

```python
query_operation_result = dkg.graph.query(
    """
    PREFIX schema: <http://schema.org/>
    SELECT ?s ?name ?description
    WHERE {
        ?s schema:name ?name ;
           schema:description ?description .
    }
    """
)
print_json(query_operation_result)
```

To learn more about querying the DKG go [here](querying-the-dkg.md).

### What's next?

### 📋 What you'll need&#x20;

Before you start, make sure you have:

1. **Development environment**:
   * **For JavaScript**: [Node.js](https://nodejs.org/) (v16 or higher) installed
   * **For Python**: [Python](https://www.python.org/downloads/) (3.8+) installed
2. **Code editor**:
   * [Visual Studio Code](https://code.visualstudio.com/) or
   * [Cursor](https://cursor.sh/) or any editor you prefer
3. **Web3 wallet** with test tokens for the [NeuroWeb](../integrated-blockchains/neuroweb.md) blockchain:
   * [MetaMask](https://metamask.io/) or similar wallet
   * Test TRAC tokens for publishing the Knowledge Asset
   * Test NEURO tokens for gas fees

🪙 Getting Test Tokens

1. Join our [Discord server](https://discord.com/invite/xCaY7hvNwD)
2. Navigate to the `#faucet-bot` channel
3. Type `!help` to see available commands
4. Use the bot to get free Test TRAC and NEURO tokens

{% hint style="warning" %}
To receive TRAC on Neuroweb, first acquire NEURO via the faucet to initiate your wallet.
{% endhint %}

### 💻 Choose your development path

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="quickstart-test-drive-the-dkg-in-5-mins/quickstart-with-node.js.md">Quickstart with Node.js</a></td><td>Publish your first Knowledge Asset on the DKG with Node.js</td><td><a href="quickstart-test-drive-the-dkg-in-5-mins/quickstart-with-node.js.md">quickstart-with-node.js.md</a></td></tr><tr><td><a href="quickstart-test-drive-the-dkg-in-5-mins/quickstart-with-python.md">Quickstart with Python</a></td><td>Publish your first Knowledge Asset on the DKG with Python</td><td><a href="quickstart-test-drive-the-dkg-in-5-mins/quickstart-with-python.md">quickstart-with-python.md</a></td></tr></tbody></table>
