# Setup instructions (Dockerless)

{% hint style="info" %}
These setup instructions for DKGv6 are "Work in progress" and are subject to change. The development team expects to introduce improvements as well as a more automated process of setting up the DKGv6 node in the future.
{% endhint %}

{% hint style="success" %}
Need any assistance with node setup? Join the DKGv6 Discord chat and find help within the OriginTrail tech community!
{% endhint %}

{% hint style="warning" %}
**IMPORTANT: These instructions are not intended for migrating your current v5 node to v6. Attempting this will most likely break your v5 node at this point. You should only use these instructions in order to setup a fresh OriginTrail v6 testnet node.**
{% endhint %}

### Prerequisites <a href="#docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b" id="docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b"></a>

* A dedicated **4GB RAM/2CPUs/50GB HDD** **Ubuntu** server (minimum hardware requirements)

# Installation

## Step 1 - Create your wallets

First, you will need a total of **4 wallets**. 

### **2 EVM (Ethereum) wallets**
- **1 Operational wallet**
    - Private keys will be stored in the node
    - An ideal example is a Metamask wallet
    - *For V6 Stage 1 testers, you must use the same operational wallet address for telemetry contributions*
- **1 Management wallet** 
    - Private keys are not stored on the node
    - An ideal example is a Ledger wallet

{% hint style="info" %}
To view your EVM wallet balance, make sure to add the [OriginTrail Parachain Network RPC](https://docs.origintrail.io/blockchain-layer-1/origintrail-parachain/origintrail-parachain-network-rpc) to your Metamask
{% endhint %}

### **2 Substrate wallets**
- **1 Operational wallet**
    - An ideal example is a wallet generated on [Polkadot{.js} extension](https://polkadot.js.org/extension/) or [Talisman](https://talisman.xyz/)
- **1 Management wallet**
    - You can also use a Polkadot{.js} or Talisman extension.

{% hint style="info" %}
To view your substrate wallet balance, you can either visit
[**OriginTrail Parachain Devnet**](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Flofar.origin-trail.network#/accounts) **(testnet)** or [**OriginTrail Parachain**](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fparachain-rpc.origin-trail.network#/accounts) **(mainnet)**
{% endhint %}

## Step 2 - Fund your wallets

Fund your Substrate and EVM wallets with test OTP and TRAC tokens. Instructions are available on [fund-your-v6-testnet-node.md](fund-your-v6-testnet-node.md "mention") page.

You can also ask for test OTP and TRAC tokens on [OriginTrail Node Community](https://t.me/otnodegroup). 

{% hint style="info" %}
You need test OTP in both substrate wallets, and test Trac in your EVM operational wallet.
{% endhint %}

{% hint style="info" %}
The [Discord channel](https://discord.com/channels/460837319025623050/748179338699997235) will only fund 1 substrate wallet (starting with 'g') and 1 EVM wallet. After receiving test OTP on your first substrate wallet, visit [OriginTrail Parachain Devnet](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Flofar.origin-trail.network#/accounts) and send test OTP to your second substrate wallet. 
{% endhint %}

To view your test TRAC balance on Metamask, first switch your network to 'OriginTrail Parachain Network RPC' using the instructions above, then add the TEST custom token address using the import function
```
0x137e321166522A60CBF649Beb7a65989b9e1518e
```

## Step 3 - Create a mapping for both operational and management wallets

Create a mapping between your Substrate and EVM wallet, this can be performed through [this interface](https://parachain.origintrail.io/parachain-account-mapping).&#x20;

Connect the mapping interface with your EVM operational wallet and paste your substrate operational wallet (can start with 5 or g). 

{% hint style="info" %}
The mapping needs to be performed twice. Once for operational wallets (substrate and EVM) and once for management wallets (substrate and EVM).
{% endhint %}

{% hint style="info" %}
If you see MOTP in Metamask on the 'OriginTrail Parachain Network RPC', it means the mapping succeeded. Once mapped, the OriginTrail Parachain Devnet (substrate) and OriginTrail Parachain Network RPC (EVM) should show the same balance/tokens. 
{% endhint %}

## Step 4 - Login to your node server

Login to the server as root. You **cannot** use sudo and run this script. The command "**npm ci**" might fail.

## Step 5 - Run the installer

{% hint style="info" %}
This installer is intended for use on a fresh server. It will only work on a current v6 Stage 1 testnet server if you wipe it by doing the following step: 
```
systemctl stop otnode blazegraph fuseki && rm -rf ot-node blazegraph* fuseki* installer.sh
```
{% endhint %}

**Download and run the installer script:**

```
cd /root/ && curl https://raw.githubusercontent.com/OriginTrail/ot-node/v6/release/testnet/installer/installer.sh --output installer.sh && chmod +x installer.sh && ./installer.sh
```

The installer script will guide you through the installation.

{% hint style="success" %}
**Congratulations. Welcome to v6 beta**
{% endhint %}

**Checking node logs:**

```
journalctl -u otnode --output cat -fn 100
```

![Successfully started](<../../.gitbook/assets/Screenshot 2021-12-27 at 15.49.28.png>)

**OriginTrail node commands:**

**Start node:** otnode-start&#x20;

**Stop node:** otnode-stop&#x20;

**Restart node:** otnode-restart&#x20;

**Show node logs:** otnode-logs&#x20;

**Open node configuration:** otnode-config

We would love to meet you in our Discord chat - join us [here](https://discord.gg/6BGSCJfk4Y).