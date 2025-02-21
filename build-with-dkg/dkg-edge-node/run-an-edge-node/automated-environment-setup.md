---
description: This page will guide you through the DKG Edge Node installation process
---

# Automated environment setup

{% hint style="info" %}
Currently, the automated environment setup works only on **Ubuntu 24.04 LTS** and **Ubuntu 22.04 LTS**.
{% endhint %}

The installation process involves interacting with the installer through the terminal. To proceed, you should have all the required inputs ready, as they will be required by the installer:

* Admin and operational keys for your Edge Node and their private keys
* Funds on the wallets
* Firewall configured

### Funds on the wallets

You should have funds on your operational wallet, both TRAC and the native blockchain token.

{% hint style="info" %}
If using NeuroWeb, the default blockchain network for the Edge Node, your operational wallet must have NEURO and TRAC tokens.

Learn how to obtain test funds, via our faucet, [here](../../../useful-resources/test-token-faucet.md).
{% endhint %}

{% hint style="info" %}
For just getting started, your management wallet does not need to have funds.
{% endhint %}

### Firewall configuration

Firewall configuration implies opening these ports, for the following services:

* 80 - UI HTTP
* 443 - UI HTTPS
* 3001 - Authentication service
* 3002 - API
* 5002 - DRAG
* 5005 - Knowledge mining
* 8900 - OT Node
* 8008 - Airflow webserver - optional

{% hint style="info" %}
On Ubuntu this is most commonly done by running the command:

```bash
ufw allow <PORT>
```
{% endhint %}

### System Requirements

* **Operating System:** Linux (Ubuntu 24.04, Ubuntu 22.04)
* **RAM:** At least 8 GB
* **CPU:** 4
* **Storage:** At least 20 GB of available space
* **Network:** Stable internet connection

## Software dependencies

Ensure the following services are installed:

* Git

## 1. How the installer works

{% hint style="info" %}
The provided installer is designed to install the **OriginTrail Edge Node** on **Ubuntu 22.04 LTS, and 24.04 LTS** distributions.
{% endhint %}

When the installation process is finalized, you will be provided with the following Edge Node services deployed to your Linux server:

* [V8 DKG Runtime Node](https://github.com/OriginTrail/ot-node/tree/v8/release/testnet)
* [Edge Node Interface](https://github.com/OriginTrail/edge-node-interface)
* [Edge Node API](https://github.com/OriginTrail/edge-node-api)
* [Knowledge Mining API](https://github.com/OriginTrail/edge-node-knowledge-mining)
* [dRAG](https://github.com/OriginTrail/edge-node-drag)
* [Authentication Service](https://github.com/OriginTrail/edge-node-authentication-service)

Each Edge Node service will have its required runtime environment and dependencies properly configured. This includes the installation and setup of **Node.js (with npm), Python, MySQL, Redis**, and **Apache Airflow**.&#x20;

All services will be configured to run as **`systemd`** processes, which will be enabled and started automatically upon installation.

{% hint style="info" %}
It is also possible to install the OriginTrail Edge Node on other systems, but it would require modifications to the installer. If you have any such modifications in mind, we highly encourage your contributions. Please visit our [GitHub](https://github.com/OriginTrail/edge-node-installer) for more information.
{% endhint %}

## 2. Download the OriginTrail DKG Edge Node installer

In order to clone the Edge Node installer repository, simply run the commands below on your Linux server:

<pre class="language-sh"><code class="lang-sh">git clone https://github.com/OriginTrail/edge-node-installer.git
<strong>cd edge-node-installer
</strong></code></pre>

## 3. See environment variables file (.env)

Fill in the required parameters.

```bash
nano .env.example
```

When finished, rename the file to `.env` with the following command.

```bash
mv .env.example .env
```

## 4. Execute the installer by running: <a href="#id-3.-execute-the-installer-by-running" id="id-3.-execute-the-installer-by-running"></a>

Simply run the installer with the command provided below:

```bash
bash edge-node-installer.sh
```

## 5. Changing the environment variables after deploying the Edge Node

### Publishing wallet setup

By default, the development wallet will be already set, which cannot be used for actual Edge node deployment, and needs to be updated with real wallet credentials.

{% hint style="info" %}
For testing/development, you can use your “**Operational wallet**” since it has funds
{% endhint %}

Obtain access to the MySQL database.

```bash
mysql -u root -p
```

{% hint style="info" %}
The default password for the MySQL database is **otnodedb.** It's set it in the `.env` file under "SQL\_PASSWORD".
{% endhint %}

Then, execute the following:

```sql
USE edge-node-auth-service;
```

And update the details:

```sql
UPDATE user_wallets
SET
    wallet = 'YOUR_WALLET',
    private_key = 'PRIVATE_KEY',
    blockchain = 'SELECTED_CHAIN_ID'
WHERE id = 1
LIMIT 1;
```

### Blockchain network setup

The Edge Node currently supports Neuroweb (default), Base, and Gnosis blockchain networks. In order to change the default one, the below steps should be followed.

#### Pre-requisites:

* Selected blockchain is supported
* Selected blockchain variables are populated in the `.env` file

If all requirements are met, the process of changing the Edge Nodes blockchain is as simple as just setting up a new [publishing wallet setup](automated-environment-setup.md#publishing-wallet-setup).

{% hint style="info" %}
The available SELECTED\_CHAIN\_ID are:

* **NeuroWeb mainnet** - otp:2043
* **NeuroWeb testnet** - otp:20430
* **Base mainnet** - base:8453
* **Base testnet** - base:84532
* **Gnosis mainnet** - gnosis:100
* **Gnosis testnet** - gnosis:10200
{% endhint %}

### Configure the rest of the DKG Edge Node services

The instructions for configuring DKG Edge Node services are available in the README file of each service's GitHub repository, where you can follow the steps provided.&#x20;

* **Edge Node Authentication Service** ([README](https://github.com/OriginTrail/edge-node-authentication-service) instructions)
* **Edge Node API** ([README](https://github.com/OriginTrail/edge-node-api) instructions)
* **Edge Node UI** ([README](https://github.com/OriginTrail/edge-node-ui) instructions)
* **Edge Node Knowledge Mining** ([README](https://github.com/OriginTrail/edge-node-knowledge-mining) instructions)
* **Edge Node dRAG** ([README](https://github.com/OriginTrail/edge-node-drag) instructions)

## Need help? <a href="#need-help" id="need-help"></a>

If you encounter any issues during the installation process or have questions about any of the topics above, jump into our official [Discord](https://discord.gg/xCaY7hvNwD) and ask for assistance.

Follow our official channels for updates:

* [X](https://x.com/origin_trail)
* [Medium](https://medium.com/origintrail)
* [Telegram](https://t.me/origintrail)
