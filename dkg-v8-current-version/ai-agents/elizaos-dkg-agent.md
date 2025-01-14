# ElizaOS DKG agent

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

With the newest DKG x ElizaOS integration, you can now build AI agents that store their memories on the Decentralized Knowledge Graph (DKG). This setup enables agents to share memories (creating a **collective memory**), manage their knowledge in a transparent and verifiable way, in order to base their decision-making on reliable and tamper-evident data.\
\
Currently, the DKG integration is available in the [Elizagraph starter kit](https://github.com/OriginTrail/elizagraph) that includes the plugin. This repository is expected to evolve into the primary agent-launching platform for the DKG. The community will also have opportunities to contribute via GitHub issues, each representing a potential new feature or bug-fixes. An official integration into the main ElizaOS repository is coming soon, making the integration available to even more developers.

To set up an AI agent using OriginTrail and ElizaOS, follow these steps:

**Prerequisites**

[Python 2.7+](https://www.python.org/downloads/)

[Node.js 23+](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm/)

[pnpm](https://pnpm.io/installation)

**Clone the Elizagraph repository**

```bash
git clone https://github.com/OriginTrail/elizagraph.git
cd elizagraph
```

**Install dependencies and build the project**

```bash
pnpm install
pnpm run build
```

**Set up Environment Variables**

Copy the `.env.example` file and rename it to `.env` and fill in the necessary details

1. _Node information_

If you do not already have a DKG node set up - you can use a public node or set up a [development node](../v8-dkg-sdk/setting-up-your-development-environment.md) or a [testnet node](../v8-dkg-core-node/run-a-v8-core-node-on-testnet/). Then, populate the following variables.

There's one public node available for mainnet ([https://positron.origin-trail.network](https://positron.origin-trail.network/)) and one for testnet ([https://v6-pegasus-node-02.origin-trail.network](https://v6-pegasus-node-02.origin-trail.network)). All blockchains are supported on each of the nodes.

* `ENVIRONMENT`: Define your environment. For example, use `development` if you're running a local setup, `testnet`for a testnet setup or `mainnet`a mainnet setup.
* `OT_NODE_HOSTNAME`: Enter the hostname or IP address of your OriginTrail DKG node. This will be the URL of the node you set up or http://localhost if you're running it locally.
* `OT_NODE_PORT`: The port used by the DKG node, typically `8900`.
* `PUBLIC_KEY`: The public key of the wallet you will use to publish Knowledge Assets.
* `PRIVATE_KEY`: The private key corresponding to the above wallet. Ensure you keep this secure and never share it outside of the .env file.
* `BLOCKCHAIN_NAME`: Specify the blockchain network you’re using. `otp:2043` (NeuroWeb mainnet), `base:8453` (Base mainnet), `gnosis:100` (Gnosis mainnet), `otp:20430` (NeuroWeb testnet), `base:84532` (Base testnet), `gnosis:10200` (Gnosis testnet)

In order to fund your wallet on testnet, feel free to use the [Faucet](../../dkg-v6-previous-version/node-setup-instructions/useful-resources/dkg-testnet-faucet.md) in our Discord. There's a message pinned in the #faucet channel in case some of the faucets are down - in that case feel free to ping us to send you some testnet funds manually.

2. _LLM key_

Eliza supports a wide range of LLM providers, so create an API key for one of them and paste it into the environment file.

3. _Twitter credentials (in case you want to use Twitter)_

Eliza uses a basic Twitter authentication setup, so use your username, password and email so that the application can post on the platform. If you encounter issues, we recommend you to use the TWITTER\_COOKIES variable and copy the cookies from the browser.

**Customize DKG Knowledge Asset & Query Templates**

If you wish to do so, modify the templates in `plugin-dkg/constants.ts` to change the format in which your data is stored or queried.

**Run the character**

Firstly, create a character in the `characters` folder, for example `chatdkg.character.json`

```bash
pnpm start --characters="characters/chatdkg.character.json"
```

#### Notes

* There is no need to manually add `plugin-dkg` to the `plugins` array; it will load automatically.
* Ensure you configure the Twitter client (if you wish to use Twitter) and select your LLM provider in the character settings.
