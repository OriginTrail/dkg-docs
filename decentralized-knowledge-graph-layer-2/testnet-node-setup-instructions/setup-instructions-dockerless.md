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

### Installation

#### Step 1 - Fund your wallets

Fund your Substrate and Ethereum wallets with OTP and TRAC test tokens. Instructions are available at [fund-your-v6-testnet-node.md](fund-your-v6-testnet-node.md "mention") page.

{% hint style="info" %}
Make sure to fund both your operational and management wallets.
{% endhint %}

#### Step 2 - Create a mapping for both operational and management wallets

Create a mapping between your Substrate and Ethereum wallets (that are pre-funded in the previous step), this can be performed through [this interface](https://parachain.origintrail.io/parachain-account-mapping).&#x20;

{% hint style="info" %}
The mapping needs to be performed for both for the node operational and management wallets.
{% endhint %}

#### Step 3 - Login to your node server

Login to the server as root. You **cannot** use sudo and run this script. The command "**npm ci**" might fail.

#### Step 4 - Run the installer

**Download the installer script:**

```
cd /root/ && curl https://raw.githubusercontent.com/OriginTrail/ot-node/v6/release/testnet/installer/installer.sh --output installer.sh
```

**Update permissions for the installer script:**

```
chmod +x installer.sh
```

**Run the installer script:**

```
./installer.sh
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

Note: to verify your node is running, run `otnode-logs` command

**Stop node:** otnode-stop&#x20;

**Restart node:** otnode-restart&#x20;

**Show node logs:** otnode-logs&#x20;

**Open node configuration:** otnode-config

We would love to meet you in our Discord chat - join us [here](https://discord.gg/6BGSCJfk4Y).
