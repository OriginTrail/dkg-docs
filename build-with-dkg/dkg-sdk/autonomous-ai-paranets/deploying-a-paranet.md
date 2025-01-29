---
description: >-
  A guide for developers & paranet operators on launching their Paranet on the
  DKG
---

# Deploying a Paranet

{% hint style="danger" %}
**Paranets are not currently supported in V8. Expect the support to be back latest by the end of February.**
{% endhint %}

## THe steps to deploy a paranet are as follows:

### 1. Prepare for paranet deployment

To successfully deploy a paranet you will have to create a Knowledge asset on the DKG and execute paranet registration transactions on the blockchain. This guide assumes you already have a good idea of what purpose you are deploying your DKG paranet for and will focus only on the technical steps.&#x20;

Below is the input you will need:

* **Decide which blockchain to deploy your paranet on.** This is the blockchain on which knowledge mining will take place. All DKG integrated blockchains can be used, however initially only Neuroweb blockchain supports [IPOs](../../../dkg-v6-previous-version/autonomous-ai-paranets/initial-paranet-offerings-ipos.md)
* Pick a _Paranet name_ and create a short _description_ (which will be stored on chain)
* Prepare a _**Paranet profile knowledge asset**_ to represent your paranet as it's profile on the DKG. It can be minimal, or as rich in content as you'd like. You will create it as a Knowledge asset in the next step

### 2. Create your Paranet Profile on the DKG&#x20;

A Paranet profile is a knowledge asset that will uniquely identify your paranet, and you as the paranet operator. As long as you own this knowledge asset, you will be able to manage paranet operator functions in the DKG paranet smart contracts.

An example paranet knowledge asset could look like this:

```json
{
  "@context": "http://schema.org/",
  "@type": "DataCatalog",
  "name": "Super Paranet",
  "description": "This is the description of the super paranet!",
  "keywords": "keyword1, keyword2, keyword3 ...",
}
```

Once you create your paranet knowledge asset, save the resulting UAL as you will need it for the next step.

{% hint style="info" %}
As the Paranet profile Knowledge asset is an NFT on chain, if you would like to change your operator key (wallet), all you need to do is transfer this NFT to your new address.
{% endhint %}

### 3. Execute _registerParanet_ transaction on the blockchain

You can either execute the function via the DKG Explorer Paranets page (to be released) or execute the paranet transaction directly on the smart contracts.&#x20;

**That's it, you have successfully performed a minimal paranet deployment** and miners can now start mining knowledge via your paranet.&#x20;

To proceed we recommend setting up a **DKG node** that will continuously sync your paranet knowledge graph.

Additionally, you might want to consider [running an IPO](../../../dkg-v6-previous-version/autonomous-ai-paranets/initial-paranet-offerings-ipos.md) to incentivise Knowledge miners.

