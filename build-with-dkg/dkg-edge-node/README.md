---
icon: diagram-project
description: >-
  The platform for building collective neuro-symbolic AI. Start building with
  the DKG Edge Node beta version
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

# DKG Edge Node

Looking to build your decentralized AI project, launch a Decentralized Knowledge Graph (DKG) paranet, build a dRAG system, or just take the DKG for a spin?&#x20;

The OriginTrail DKG Edge Node is an open-source platform designed to empower builders of neuro-symbolic AI projects. It provides a collection of fully customizable components for building decentralized AI applications based on the OriginTrail DKG.&#x20;

Edge Nodes enable running decentralized AI services on the "network edge", providing a unified platform for:&#x20;

* **Producing & publishing Knowledge Assets,** offering a multitude of Knowledge-Asset-creation agents based on knowledge graph creation pipelines, vector embedding generation, and others combined with a paranet publishing system.
* **Maintaining data privately stored on a device hosting the Edge Node,** enabling full configurability of technology used, such as choice of graph databases, vector stores, etc.
* **Building Decentralized Retrieval Augmented Generation (dRAG) pipelines** using the dRAG API and combining knowledge graph queries, vector search, or other retrieval methods.
* **Configurability and choice of AI models,** running either on the device or externally.
* **Customizable and extendable user interface (UI) elements for your projects, such as paranet UIs,** on the basis of the Edge Node codebase.

{% hint style="info" %}
As an early builder, you can benefit from the [DKG Edge Node inception program](dkg-edge-node-inception-program.md) with up to 100k TRAC tokens for your publishing costs on the DKG mainnet.&#x20;
{% endhint %}

{% hint style="warning" %}
The DKG Edge Node and its documentation are a work in progress. They are expected to undergo many improvements and we welcome all your contributions to this.&#x20;

Feel free to contribute to these docs directly through [GitHub](https://github.com/OriginTrail/dkg-docs) (click the "Edit on GitHub" button in the top right corner of the screen).&#x20;
{% endhint %}

### How can I start building with the Edge Node?

<table data-view="cards" data-full-width="false"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><a href="dkg-edge-node-architecture.md">Step 1: Learn about the Edge Node internals (architecture)</a></td><td></td></tr><tr><td><a href="./">Step 2: Set up an Edge Node project</a></td><td></td></tr><tr><td><a href="customize-the-edge-node-and-build-your-project.md">Step 3: Customize the Edge Node to build your project</a></td><td></td></tr><tr><td><a href="deploy-your-edge-node-based-project.md">Step 4: Deploy to your environment</a></td><td></td></tr></tbody></table>

### What's the difference between a Core Node and an Edge Node?

The OriginTrail DKG V8 network is comprised of two types of DKG nodes — **Core Nodes**, which form the DKG network core and host the DKG, and **Edge Nodes,** which run on edge devices and connect to the network core. The current beta version is designed to operate on edge devices running Linux and MacOS, with future support planned for a wide range of edge devices such as mobile phones, wearables, IoT devices, and generally enterprise environments. This enables large volumes of sensitive data to safely enter the AI age while maintaining privacy.

The DKG Edge Node ensures that data remains protected on the device, giving owners full control over how their data is shared. This data becomes part of the global DKG, with precise access management permissions controlled by the data owner. Through dRAG, AI applications can access both private and public DKG data, with the owner’s permission, to power privacy-preserving AI solutions.

With the ability to run AI applications directly on edge devices, DKG Edge Nodes enable secure and decentralized data usage on the growing number of network edge devices. The DKG Edge Node also plays a key role in expanding the DKG into a large-scale decentralized physical infrastructure network (DePIN).
