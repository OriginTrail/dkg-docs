# ElizaOS DKG agent

ElizaOS is a popular open source AI agent framework which supports a native DKG integration through the DKG plugin. You can now build **AI agents that store their memories** on the Decentralized Knowledge Graph (DKG). This setup enables agents to **share memories** (creating a **collective memory**) and manage their knowledge **transparently and verifiably.**&#x20;

You can watch the following video to learn how to setup a ElizaOS DKG agent, or follow the text instructions below.

ElizaOS is operational on **Mac** and **Ubuntu** devices, Windows is not yet supported

## Video tutorial (\~1h 15mins)

{% embed url="https://youtu.be/w3-_WBH3uSQ?si=5g3WY2G-HEPu0Kt9" %}
Video: How to build an AI agent with ElizaOS DKG Plugin
{% endembed %}

## Classic instructions

You can use the OriginTrail [Elizagraph starter kit](https://github.com/OriginTrail/elizagraph), which includes the plugin, or using the [official ElizaOS repo](https://github.com/elizaOS/eliza), where the plugin has already been integrated.  The following instructions will assume you are using the **Elizagraph Starter kit**.

### **Prerequisites - make sure you have them all set up**

{% hint style="info" %}
[Python 2.7+](https://www.python.org/downloads/)

[Node.js 23+](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm/)

[pnpm](https://pnpm.io/installation)
{% endhint %}

## **Step-by-step**

### **1. Clone the Elizagraph repository**

```bash
git clone https://github.com/OriginTrail/elizagraph.git
cd elizagraph
```

### **2. Install dependencies and build the project**

```bash
pnpm install
pnpm run build
```

### **3. Set up environment variables**

Copy the `.env.example` file (from the Elizagraph folder in cloned repository) and rename it to `.env` and fill in the necessary details. The following instructions will help you populate the .env file.

1. **Node information**

If you do not already have a DKG node set up, you can use a public node that the OriginTrail team set up so that everyone has an easy way to interact with the DKG.

There's one public node available for mainnet ([https://positron.origin-trail.network](https://positron.origin-trail.network/)) and one for testnet ([https://v6-pegasus-node-02.origin-trail.network](https://v6-pegasus-node-02.origin-trail.network)). All blockchains are supported on each of the nodes.

Alternatively, you could also set up and connect to your own Edge Node for further features like a graph & chatbot interface, customizable knowledge mining pipelines, private knowledge assets, and more. Check out Edge Nodes [here](../../graveyard/everything/dkg-edge-node/).

{% hint style="info" %}
**Mainnet** is the live blockchain for real transactions, while **testnet** is a risk-free testing environment.
{% endhint %}

{% hint style="info" %}
Here's an example of how to set up a MetaMask wallet: [here](https://youtu.be/-HTubEJ61zU?si=tUcacxeluIMRFp6q)
{% endhint %}

* `ENVIRONMENT`: Define your environment. For example, use `development` if you're running a local setup, `testnet`for a testnet setup, or `mainnet`a mainnet setup.
* `OT_NODE_HOSTNAME`: Enter the hostname or IP address of your OriginTrail DKG node. This will be the URL of the node you set up or http://localhost if you're running it locally.
* `OT_NODE_PORT`: The port used by the DKG node, typically `8900`.
* `PUBLIC_KEY`: The public key of the wallet you will use to publish Knowledge Assets.
* `PRIVATE_KEY`: The private key corresponding to the above wallet. Ensure you keep this secure and never share it outside of the .env file.
* `BLOCKCHAIN_NAME`: Specify the blockchain network you’re using. `otp:2043` (NeuroWeb mainnet), `base:8453` (Base mainnet), `gnosis:100` (Gnosis mainnet), `otp:20430` (NeuroWeb testnet), `base:84532` (Base testnet), `gnosis:10200` (Gnosis testnet)

In order to fund your wallet on testnet, feel free to use the [Faucet](../../dkg-knowledge-hub/useful-resources/test-token-faucet.md) in the [OriginTrail Discord](https://discord.gg/xCaY7hvNwD). There's a message pinned in the **#faucet-bot** channel in case some of the faucets are down. In that case, feel free to ping the core team to send you some testnet funds manually.

{% hint style="info" %}
If you are building your agent on the NeuroWeb, you need to get NEURO first and then TRAC.
{% endhint %}

2. **LLM key**

Eliza supports a wide range of LLM providers. To use one of them, create an API key and paste it into the environment file.

{% hint style="info" %}
Here’s how to get an [API key from ChatGPT](https://www.youtube.com/watch?v=3BrmNZoPzHA).&#x20;
{% endhint %}

For example, if you want to use an Open AI LLM, populate the OPENAI\_API\_KEY variable in the .env.

```properties
OPENAI_API_KEY= # obtain the key on https://platform.openai.com/
```

3. **X credentials (in case you want to use X)**

Eliza uses a basic X authentication setup. Use your username, password, and email so that the application can post on the platform. If you encounter issues, we recommend you to use the TWITTER\_COOKIES variable and copy the cookies from the browser.

### **4. Customize DKG Knowledge Asset & query templates**

If you wish to do so, modify the templates in `plugin-dkg/constants.ts` to change the format in which your data is stored or queried.

Additionally, you can modify the interactions with the DKG in the Eliza providers, actions, and evaluators by calling different DKG.js functions, or modifying the parameters. For example, you could use a paranet for your agent. Check out the SDK docs [here](../../build-a-dkg-node-ai-agent/advanced-features-and-toolkits/dkg-sdk/).

### **5. Run the character**

Firstly, create a character in the `characters` folder, for example `chatdkg.character.json.`

You can look at existing examples in the `characters` folder for inspiration.

```bash
pnpm start --characters="characters/chatdkg.character.json"
```



{% hint style="warning" %}
#### Notes

* There is no need to manually add `plugin-dkg` to the `plugins` array, it will load automatically because it is included in the `agent/src/index.ts` file.
* Ensure you configure the X client (if you wish to use X) and select your LLM provider in the character settings.
{% endhint %}
