---
description: This page will guide you through the DKG Edge Node installation process
---

# Automated environment setup

{% hint style="warning" %}
Currently, the automated environment setup works only on **Ubuntu 24.04 LTS** and **Ubuntu 22.04 LTS**.
{% endhint %}

The installation process involves interacting with the installer through the terminal. To proceed, you should have all the required inputs ready, as they will be required by the installer:

* Admin and operational keys for your Edge Node and their private keys
* Funds on the wallets
* Firewall configured

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

```sh
git clone https://github.com/OriginTrail/edge-node-installer.git
cd edge-node-installer
```

## 3. Set the environment variables file (.env)

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

## 5. Usage

You can interact with the user interface at _http://your-nodes-ip-address_.

{% hint style="info" %}
The default login credentials are as follows:

**username:** my\_edge\_node

**password:** edge\_node\_pass

It is recommended to change the default credentials. You can do that by directly altering the _Users_ table in the _edge-node-auth-service_.
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
