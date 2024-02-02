---
description: >-
  This section of the tutorial will cover the details regarding the RPC
  endpoints for the blockchains supported by the OriginTrail DKG node.
---

# Acquire archive RPC endpoints

In order for your OriginTrail node to be able to connect and communicate with any of the supported blockchains, it will require an archive RPC endpoint. There are different RPC providers offering endpoints for different blockchains and its up the node runner to choose the provider.

## 1. NeuroWeb archival RPC endpoint:

When it comes to deploying your node on OriginTrail's NeuroWeb (testnet or mainnet), your node will automatically be provided with the RPC endpoint so no action is required from the node runner **at the current stage**.&#x20;

## 2. Gnosis and Chiado archival RPC endpoints:

Refer to the [official Gnosis documentation](https://docs.gnosischain.com/tools/rpc/) and choose an RPC provider in order to acquire the archival RPC Endpoint.&#x20;

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.&#x20;
{% endhint %}

During the installation process, installer will ask you to input the Chiado (Testnet) or Gnosis (Mainnet) archival RPC endpoint and autimatically configure your node to use it. The endpoint you provide, will be inserted into the **.origintrail\_noderc** (configuration file) automatically.

{% hint style="info" %}
You will be able to change your RPC endpoint manually later if you wish by editing the .origintrail\_noderc custom configuration file which will be located inside the "ot-node" directory.
{% endhint %}
