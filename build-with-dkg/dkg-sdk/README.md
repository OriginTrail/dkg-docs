---
description: Decentralized Knowledge Graph V8 client
icon: gear-complex-code
coverY: 0
---

# DKG SDK

{% embed url="https://youtu.be/4oi_0hJmxcY" %}
OriginTrail dev tutorial: SDK walkthrough
{% endembed %}

The OriginTrail SDKs are client libraries for your applications, used to interact and connect with the OriginTrail Decentralized Knowledge Graph.

From an architectural standpoint, the SDK libraries are application interfaces into the DKG. They enable you to create and manage **Knowledge Assets** through your apps and perform network queries (such as search or SPARQL queries), as illustrated below.&#x20;

<figure><img src="../../.gitbook/assets/V8 DKG SDK.png" alt=""><figcaption><p>The interplay between your app, DKG and blockchains</p></figcaption></figure>



The OriginTrail SDK currently comes in two forms:

* Javascript SDK - [**dkg.js**](dkg-v8-js-client/)&#x20;
* Python SDK - [**dkg.py**](dkg-v8-py-client/)**.**&#x20;



### Try out the SDK

You can try out the SDK in two different ways:

#### 1. Using Public DKG Nodes

Try the SDK with public DKG nodes by following the [Quickstart: Test Drive the DKG in 5 Minutes](https://docs.origintrail.io/build-with-dkg/quickstart-test-drive-the-dkg-in-5-mins) guide.

#### 2. Development Environment Setup

Set up a development environment using one of the following options:

* **Deploy your node on the DKG testnet (recommended):**\
  This option allows you to quickly experiment with the SDK on a testnet of your choice.\
  Follow the [Edge Node Deployment Guide](https://docs.origintrail.io/build-with-dkg/dkg-edge-node/setup-your-edge-node-development-environment) for setup instructions.
* **Deploy your node on a local DKG network:**\
  Use this option for a fully localized development environment by following the [Developoment Environment Setup Guide](setting-up-your-development-environment.md).



SDKs for other programming languages would be welcome contributions to the project. The core development team is also considering including them in the roadmap.

{% hint style="info" %}
Interested in building a DKG SDK in a particular programming language? We'd love to support you.&#x20;

Create an [issue](https://github.com/OriginTrail/ot-node/issues) on our GitHub, and let's get the conversation started!
{% endhint %}
