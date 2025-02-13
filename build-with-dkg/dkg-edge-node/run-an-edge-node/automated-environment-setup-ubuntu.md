---
description: This page will guide you trough the DKG Edge Node installation process
---

# Automated environment setup (Ubuntu)

The installation process involves interacting with the installer through the terminal. To proceed, you should have all the required inputs ready, as they will be required by the installer:

* Ubuntu 20.04, 22.04 or 24.04 instance
* Admin and operational keys and their private keys
* Funds on the wallets
* Firewall configured

## 1. How the installer works

This installer automatically sets up and configures all the necessary processes for the Edge Node:

1. [Authentication service](https://github.com/OriginTrail/edge-node-authentication-service)
2. [Edge Node API](https://github.com/OriginTrail/edge-node-api)
3. [Edge Node interface](https://github.com/OriginTrail/edge-node-interface)
4. [Knowledge mining API](https://github.com/OriginTrail/edge-node-knowledge-mining)
5. [dRAG](https://github.com/OriginTrail/edge-node-drag)

{% hint style="info" %}
The provided installer is designed to install the **OriginTrail Edge** node on **Ubuntu 20.04 LTS, 22.04 LTS and 24.04 LTS** distributions.
{% endhint %}

{% hint style="info" %}
It is also possible to install the OriginTrail Edge node on other systems, but it would require modifications to the installer. If you have any such modifications in mind, we highly encourage your contributions. Please visit our [GitHub](https://github.com/OriginTrail/ot-node) for more information.
{% endhint %}

## 2. Download the OriginTrail DKG Edge Node installer

```bash
cd /root/ && curl -L -o edge-node-installer-main.zip https://github.com/OriginTrail/edge-node-installer/archive/refs/heads/main.zip
```

After changing to root directory and downloading the main.zip file, proceed to unziping and removing it, as it's no longer needed:

```bash
unzip edge-node-installer-main.zip && rm edge-node-installer-main.zip && cd edge-node-installer-main
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

```bash
bash edge-node-installer.sh
```

## 5. Usage

You can interact with the user interface on _http://your-nodes-ip-address_.

{% hint style="info" %}
The default login credentials are as following:

**username:** my\_edge\_node

**password:** edge\_node\_pass

It is recommended to change the default credentials, you can do that by directly altering the _Users_ table in the _edge-node-auth-service_.
{% endhint %}

## Need help? <a href="#need-help" id="need-help"></a>

If you encounter any issues during the installation process or have questions regarding any of the above topics, jump into our official [Discord](https://discord.gg/xCaY7hvNwD) and ask for assistance.

Follow our official channels for updates:

* [X](https://x.com/origin_trail)
* [Medium](https://medium.com/origintrail)
* [Telegram](https://t.me/origintrail)
