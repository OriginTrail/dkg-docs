---
icon: circle-nodes
description: >-
  The platform for building collective neuro-symbolic AI. Start building with
  the V8 DKG edge node beta version
cover: ../../.gitbook/assets/Edge_Node_cover (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# V8 DKG Edge Node

Looking to build your Decentralized AI project, launch a DKG paranet, build a DRAG system or just take the DKG for a spin?&#x20;

The OriginTrail DKG V8 Edge node is an open source platform designed to empower builders of neuro-symbolic AI projects, providing a collection of fully customizable components to build Decentralized AI applications based on OriginTrail Decentralized Knowledge Graph.&#x20;

Edge nodes enable running Decentralized AI services on the "network edge", providing a unified platform for:&#x20;

* **producing & publishing Knowledge assets,** offering a multitude of Knowledge asset creation agents, based on Knowledge Graph creation pipelines, vector embedding generation and others combined with a Paranet publishing system&#x20;
* **maintaining data privately stored on device hosting the Edge node,** enabling full configurability of technology used, such as choice of graph databases, vector stores etc
* **building Decentralized Retrieval Augmented Generation (DRAG) pipelines,** using the DRAG API and combining knowledge graph queries, vector search or other retrieval methods
* **configurability and choice of AI models,** running either on device or externally
* **customizable and extendable UI elements for your projects, such as Paranet UIs,** on the basis of the Edge node codebase



{% hint style="info" %}
Though currently in Beta, the individual DKG Edge node components have been successfully deployed in various productive environments by builders on DKG V6 mainnet. We expect to reach a productive release by end of 2024. \
As an early builder, you can additionally benefit from the [DKG Edge node inception program](dkg-edge-node-inception-program.md) with up to 100k TRAC tokens for your publishing costs on DKG mainnet.&#x20;
{% endhint %}

{% hint style="warning" %}
The V8 DKG node and its documentation are a work in progress and expected to undergo many improvements - we welcome all your contributions. Feel free to contribute to these docs directly via [Github](https://github.com/OriginTrail/dkg-docs) (you should see an "Edit in Github" button in the top right corner of the screen).&#x20;
{% endhint %}

### How can I get started building with the Edge node?

<table data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><a href="dkg-edge-node-architecture.md">Step 1: Learn about the V8 Edge node internals (architecture)</a></td><td></td><td></td></tr><tr><td><a href="setup-a-boilerplate-v8-edge-node.md">Step 2: Setup a boilerplate V8 Edge node project</a></td><td></td><td></td></tr><tr><td><a href="customize-the-edge-node-and-build-your-project.md">Step 3: Customize the V8 Node to Build your project</a></td><td></td><td></td></tr><tr><td><a href="deploy-your-edge-node-based-project.md">Step 4: Deploy to your environment</a></td><td></td><td></td></tr></tbody></table>

### What's the difference between a Core node and an Edge node?

The OriginTrail DKG V8 network is comprised of two types of DKG nodes - **Core nodes**, which form the DKG network core and host the DKG, and **Edge Nodes** which run on edge devices and connect to network core. The current beta version is designed to operate on edge devices running Linux and MacOS, with future support for a wide range of edge devices such as mobile phones, wearables, IoT devices, and generally enterprise environments. This enables large volumes of sensitive data to safely enter the AI age while maintaining privacy.

The DKG Edge Node ensures that data remains protected on the device, giving owners full control over how their data is shared. This data becomes part of the global DKG, with precise access management permissions controlled by the data owner. Through decentralized Retrieval Augmented Generation (dRAG), AI applications can access both private and public DKG data, with the owner’s permission, to power privacy-preserving AI solutions.

With the ability to run AI applications directly on edge devices, DKG Edge Nodes enable secure and decentralized data usage on the growing number of network edge devices. The DKG Edge Node also plays a key role in expanding the DKG into a large-scale decentralized physical infrastructure network (DePIN).
