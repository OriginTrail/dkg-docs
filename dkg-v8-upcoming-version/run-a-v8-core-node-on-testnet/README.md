---
icon: server
---

# Run a V8 Core Node on testnet

The OriginTrail V8 network is comprised of two types of DKG nodes - **Core nodes**, which form the DKG network core and host the DKG, and **Edge Nodes** which run on edge devices and connect to network core.

The following pages will guide you through the process of setting up a V8 Core Node on the V8 incentivised testnet. For DKG Core Nodes you will require a Linux server with high uptime, as they are intended to be running constantly to support the network. Before installing the V8 DKG Core Node, it's essential to complete a few key steps, such as acquiring tokens, preparing node keys, obtaining blockchain RPC endpoints and similar.&#x20;

The setup process should usually last between 30 minutes to an hour, depending on your proficiency level. In case that at any point you have troubles or questions, join the dedicated [OriginTrail #v8-discussion Discord channel](https://discord.gg/JEqKe9dB) and the OriginTrail community will gladly assist.

Happy DKG node running!

{% hint style="warning" %}
The DKG V8 Core Nodes are currently in development and are intended to run on [the V8 incentivised testnet](../v8-incentivised-testnet-measure-manage-master.md) only. Do not attempt to connect the V8 Core Node to the V6 mainnet.&#x20;

You can contribute to the development by running Core Nodes and contributing to the [relevant Github](https://github.com/OriginTrail/) repositories.
{% endhint %}



## Good to know before proceeding:

To run a v8 DKG Core node, you don’t need in-depth knowledge of blockchain or knowledge graphs. If you are comfortable with:

* Navigating through directories and using basic Linux commands (e.g., `cd`, `ls`, `cp`, `mv`, `cat`, `nano/vi`)
* Updating files and configurations
* Understanding and using blockchain wallets
* Basic log monitoring and troubleshooting (e.g., `tail`, `grep`, `less`)
* Setting up and managing firewalls (e.g., `ufw`, `iptables`)

you should be quite ready to operate a DKG Core node effectively. The best way to be sure though, is to try it on the testnet :). To do so, proceed to the next page.
