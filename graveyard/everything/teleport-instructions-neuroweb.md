---
description: >-
  The instructions on this page will guide you through the step-by-step process
  of teleporting your TRAC tokens between the NeuroWeb blockchain and Ethereum
  networks and vice versa.
hidden: true
---

# Teleport instructions - NeuroWeb

After the successful integration of the OriginTrail Decentralized Knowledge Graph (DKG) with NeuroWeb, the teleport interface has been launched in order to allow users to transfer TRAC tokens from Ethereum to NeuroWeb and vice versa. The specific details of the teleport can be found in relevant OriginTrail RFCs:

* [OT-RFC-12 on OriginTrail Parachain TRAC bridges](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-12%20OriginTrail%20Parachain%20TRAC%20bridges%20\(v2\).pdf)
* [OT-RFC-16 on Parachain Bridges Implementation RFC](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-16-Parachain-Bridges-Implementation/OT-RFC-16-Parachain-Bridges-Implementation.pdf)

## Prerequisites:

* Wallet with TRAC tokens on the Ethereum or NeuroWeb network that you wish to teleport. Make sure you own the private key of the wallets that hold your TRAC token. Do not use exchange wallets or any other wallet that you do not own the private key to.
* Some amount of ETH or NEURO tokens, depending on the teleport direction, on the same wallet where you hold TRAC tokens to pay for the teleport transactions.
* You will need to connect your Ethereum wallet address with a NeuroWeb wallet address using [the mapping interface](https://neuroweb.ai/evm). This will create a mapping between the two addresses, which is necessary for the successful transfer of TRAC between the two networks.
* The minimum amount of TRAC tokens for teleport is 1 TRAC.
* Metamask browser extension.

{% hint style="info" %}
We recommend that you also go through the [Teleport FAQ](https://teleport.origintrail.io/#faq) page and get additional information on the teleport process.
{% endhint %}

## Step 1:

In order to teleport your TRAC tokens between the two networks, go to [https://teleport.origintrail.io/](https://teleport.origintrail.io/) and navigate to the teleport interface by clicking on the **“Teleport TRAC tokens”** button.

The interface will guide you through the “Get started” process. Please read all the instructions provided carefully to fully familiarize yourself with the teleport process.

## Step 2:

There are four steps required to transfer TRAC tokens from Ethereum to the NeuroWeb network and vice versa.

### Step 2.1 - Choose the teleport direction:

The first step is selecting the proper network in Metamask. This should be set based on the desired teleport direction between the two networks.

If you are teleporting TRAC tokens from Ethereum to NeuroWeb, make sure that your selected network in Metamask is “Ethereum mainnet”.  If you wish to teleport TRAC tokens from NeuroWeb to Ethereum, select the “NeuroWeb” network.

{% hint style="info" %}
**Add the NeuroWeb Network to Metamask:**

* In the "Add a network manually" section, enter the following details:
  * **Network Name**: NeuroWeb Mainnet
  * **New RPC URL**: https://astrosat-parachain-rpc.origin-trail.network/
  * **Chain ID**: 2043
  * **Currency Symbol**: NEURO
  * **Block Explorer URL**: https://neuroweb.subscan.io/
{% endhint %}

When the desired network in Metamask is selected and recognized by the interface, select the teleport direction and proceed to the next step.

{% hint style="warning" %}
Before proceeding to the next step, make sure that you have selected the proper wallet address with the TRAC tokens you wish to teleport.
{% endhint %}

<figure><img src="../../.gitbook/assets/Posnetek zaslona 2025-01-30 145420.png" alt=""><figcaption><p>Choosing teleport direction</p></figcaption></figure>

### Step 2.2 - Connect your wallet:

When you proceed to this step, the interface should automatically recognize the selected wallet address in Metamask and load it into the required field.

Make sure you double-check that the selected wallet is the one you wish to teleport TRAC tokens from. Also, check that the “Current network” recognized by the interface is the correct one (depending on the desired teleport direction).

<figure><img src="../../.gitbook/assets/connect_wallet.png" alt=""><figcaption><p>Connect wallet address</p></figcaption></figure>

After making sure that all values are correct, proceed to the next step.

### Step 2.3 - Initiate the teleport process:&#x20;

During this step you will have to provide the desired TRAC amount that you wish to teleport from one network to another. The interface will check the TRAC balance on the selected wallet and display it. Enter the TRAC amount into the required input field and initiate the teleport process.

After initiating it, Metamask will pop up and ask you to approve the transaction. By clicking “Approve” you authorize our contract to transfer your TRAC tokens. After that, you will proceed to the final initialization step.

<figure><img src="../../.gitbook/assets/initiate-teleport.png" alt=""><figcaption><p>Initiating teleport process</p></figcaption></figure>

{% hint style="info" %}
You are allowed to teleport different amounts of TRAC multiple times from the same wallet address.
{% endhint %}

### Step 2.4 - Complete the teleport process:

During the final step of the process, you will see the TRAC amount you are about to teleport. If the amount is correct, proceed by clicking the “Confirm teleport” button. After confirming, your Metamask will pop up and ask you to confirm the teleport finalization. Upon approval, TRAC tokens will be locked on the smart contract on Ethereum or NeuroWeb, depending on the teleport direction.

{% hint style="warning" %}
Deposits are possible until the 10th of each month, closing at 15:00 UTC.

Distributions of TRAC on the destination network will be performed by the 15th of each month (no more than 5 days after the finalization of deposits).
{% endhint %}

## Need help?

If you encounter any issues or have any additional questions regarding TRAC teleport, contact technical support at [tech@origin-trail.com](mailto:tech@origin-trail.com).
