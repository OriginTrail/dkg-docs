---
description: >-
  This section of the tutorial will cover the details regarding the RPC
  endpoints for the blockchains supported by the OriginTrail DKG node.
---

# Acquire archive RPC endpoints

In order for your OriginTrail node to be able to connect and communicate with any of the supported blockchains, it will require an archive RPC endpoint. There are different RPC providers offering endpoints for different blockchains and it's up the node runner to choose the provider.

## 1. NeuroWeb archival RPC endpoint:

When it comes to deploying your node on OriginTrail's NeuroWeb (testnet or mainnet), your node will automatically be provided with the RPC endpoint. This means that no action is required from the node runner **at the current stage**.

## 2. Gnosis and Chiado archival RPC endpoints:

Refer to the [official Gnosis documentation](https://docs.gnosischain.com/tools/rpc/)[ ](https://docs.gnosischain.com/)and choose an RPC provider in order to acquire the archival RPC Endpoint.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.&#x20;
{% endhint %}

During the installation process, installer will ask you to input the Chiado (Testnet) or Gnosis (Mainnet) archival RPC endpoint which will autimatically configure your node to use it. The endpoint you provide, will be inserted into the **.origintrail\_noderc** (custom configuration file) automatically.

{% hint style="info" %}
You will be able to change your RPC endpoint manually later by editing the **.origintrail\_noderc** custom configuration file which will be located inside the "ot-node" directory.
{% endhint %}



## 3. Base and Base Sepolia archival RPC endpoints:

Refer to the[ official Base documentation](https://docs.base.org/docs/) and choose an RPC provider in order to acquire the archival RPC Endpoint.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.&#x20;
{% endhint %}

During the installation process, installer will ask you to input the Base Sepolia (Testnet) or Base (Mainnet) archival RPC endpoint which will autimatically configure your node to use it. The endpoint you provide, will be inserted into the **.origintrail\_noderc** (custom configuration file) automatically.

{% hint style="info" %}
You will be able to change your RPC endpoint manually later by editing the **.origintrail\_noderc** custom configuration file which will be located inside the "ot-node" directory.
{% endhint %}
