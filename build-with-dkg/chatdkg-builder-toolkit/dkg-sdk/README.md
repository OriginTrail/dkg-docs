---
description: Decentralized Knowledge Graph V8 client
icon: gear-complex-code
---

# DKG SDK

{% embed url="https://youtu.be/4oi_0hJmxcY" %}
OriginTrail dev tutorial: SDK walkthrough
{% endembed %}

The OriginTrail SDKs are client libraries for your applications, used to interact and connect with the OriginTrail Decentralized Knowledge Graph.

From an architectural standpoint, the SDK libraries are application interfaces into the DKG. They enable you to create and manage **Knowledge Assets** through your apps and perform network queries (such as search or SPARQL queries), as illustrated below.&#x20;

<figure><img src="../../../.gitbook/assets/V8 DKG SDK.png" alt=""><figcaption><p>The interplay between your app, DKG and blockchains</p></figcaption></figure>



The OriginTrail SDK currently comes in two forms:

* Javascript SDK - [**dkg.js**](dkg-v8-js-client/)&#x20;
* Python SDK - [**dkg.py**](dkg-v8-py-client/)**.**&#x20;

{% hint style="info" %}
You can check the **public nodes on the mainnet or testnet** and choose one to use [here](../../../useful-resources/public-nodes.md).
{% endhint %}

SDKs for other programming languages would be welcome contributions to the project. The core development team is also considering including them in the roadmap.

{% hint style="info" %}
Interested in building a DKG SDK in a particular programming language? We'd love to support you.&#x20;

Create an [issue](https://github.com/OriginTrail/ot-node/issues) on our GitHub, and let's get the conversation started!
{% endhint %}
