---
icon: circle-chevron-right
cover: ../../.gitbook/assets/DKG V8.1 (1).png
coverY: 0
---

# DKG V8.1.X update guidebook

The DKG V8.1.X release series marks a major step forward for the OriginTrail ecosystem, **unlocking TRAC staking rewards and laying the groundwork for the next phase of the OriginTrail roadmap: the Metcalfe Convergence**. With the introduction of the [Random Sampling proof system](../learn-more/introduction/random-sampling-dkg-proof-system/), TRAC delegators will begin sharing network rewards based on this new, highly scalable  “Proof of Knowledge” system, while DKG Core Node runners benefit from new automation and network resilience features.

Alongside reward activation, V8.1.X releases introduce user-facing improvements such as **Node Health** and **Node Power,** two new metrics that make it easier to understand how DKG nodes are performing and earning rewards. Together, these upgrades strengthen the DKG’s role as the trusted knowledge layer for AI and set the stage for further growth of the DKG in the Metcalfe Convergence phase of the roadmap.

V8.1.X Launch mechanics & timeline\



* **JUNE 23, 2025 V8.1.0 MAINNET LAUNCH SEQUENCE INITIATED**\
  Staking features suspended from 12:00 CET for up to 72 hours. During this period, new V8.1.0 contracts are deployed and tested.&#x20;
* **JUNE 24, 2025: DKG CORE NODE V8.1.0 RELEASE**\
  Core Node runners start updating nodes
* **ETA JUNE 26, 2025: V8.1.0 MAINNET RELEASE COMPLETE**\
  Staking Dashboard back online
* **ETA JULY '25: V8.1.1 RELEASE**\
  Nodes start collecting V6 rewards
* **ETA JULY '25: V8.1.2 RELEASE:**\
  Rewards for the V8 Tuning period become collectible
* **AUGUST '25: TRANSITION TO METCALFE CONVERGENCE PHASE**

## Instructions for DKG Core Node runners

{% hint style="success" %}
In a nutshell:

* Auto-update features should take care of your Core Node update (if you have it turned on). However, it is highly recommended that you review your node activity and confirm that it has successfully updated to V8.1.0
* Core Nodes get new features; familiarize yourself with them below
{% endhint %}

### How to update to v8.1.0

If your node **auto-updater is enabled**, the **node will automatically update to version v8.1.0** without requiring any manual effort on your part.&#x20;

{% hint style="info" %}
Keeping the autoupdater enabled ensures your node always runs the latest stable release, including important security patches, bug fixes, and performance improvements. Staying up to date helps maintain optimal network participation.
{% endhint %}

While the update process itself is seamless, once your node is running v8.1.0, there are a few important features and settings you should review and get familiar with.&#x20;

### DKG Random Sampling proof system

With the release of V8.1.0, DKG Core Nodes will automatically begin participating in the [Random Sampling Proof-of-Knowledge (PoK) system](../learn-more/introduction/random-sampling-dkg-proof-system/). **No manual setup is required.**

Random Sampling is a decentralized mechanism that continuously verifies whether nodes store specific Knowledge Assets. Smart contracts issue randomized challenges to nodes, requiring them to cryptographically prove they hold certain data. This system is transparent, fair, and entirely trustless. Learn more about the [Random Sampling system](https://docs.origintrail.io/random-sampling-dkg-proof-system) here.

Random Sampling has three key objectives:

* Ensure long-term data availability across the network
* Reward active and reliable nodes that consistently store and serve Knowledge Assets
* Automate the distribution of publisher fees based on verifiable data storage

{% hint style="info" %}
No configuration is necessary, and your node will automatically begin submitting proofs in response to Random sampling challenges.
{% endhint %}

{% hint style="info" %}
Random sampling requires nodes to submit a (limited) amount of additional transactions to the blockchain (up to \~100 per day). Make sure your node's operational keys are funded with enough gas tokens for nodes to be able to do so.
{% endhint %}

### DKG Sync feature

As of DKG V8.1.0, DKG Core Nodes have the ability to “Sync” with the DKG state via the new [DKG Sync feature](../learn-more/introduction/dkg-sync.md), capturing any missing knowledge by downloading it from the network. **To start using the DKG Sync feature, you have to manually enable it.**&#x20;

**Enabling the Sync feature is highly recommended as it can help maintain high node health**, ultimately leading to your node attracting more rewards. Familiarize yourself with the Sync feature [here](../learn-more/introduction/dkg-sync.md) and how it relates to the [Random Sampling system](../learn-more/introduction/random-sampling-dkg-proof-system/) to gain a comprehensive understanding, and be prepared to enable it when your node updates to DKG V8.1.0.\


DKG Sync strengthens the reliability of the DKG by allowing Core Nodes to automatically retrieve and backfill any missing Knowledge Assets (KAs) from the network. This is especially important when your node restarts, experiences downtime, or joins the network for the first time.

**How to enable Sync:**

Instructions for enabling Sync and a more detailed explanation of how it works are available in our documentation, [here](../learn-more/introduction/dkg-sync.md).

### Configurable Blazegraph timeouts

As part of the V8.1 update, configurable timeout values for Blazegraph operations have been introduced to improve system performance and prevent heavy operations from overloading your node triple store. If you are experiencing issues with the Blazegraph process (which may occur for heavy-load users), consider lowering the timeouts.

Generalized default values have already been applied automatically with the update — no action is required. However, if you wish to customize these settings yourself, you can do so by adding the following block to your `.origintrail_noderc` file.

Default timeout configuration (all timeout values are defined in milliseconds):

```
// all values in milliseconds
"tripleStore": {
  "enabled": true,
  "timeout": {
    "query": 90000, 
    "get": 10000,
    "batchGet": 60000,
    "insert": 300000
  }
}
...
```

{% hint style="info" %}
In V8.1.0, these timeouts are Blazegraph-specific, however, the core developers intend to expand the timeout configuration for all supported triple stores.\

{% endhint %}

Parameters overview:

* `query`: Maximum duration for SPARQL queries
* `get`: Maximum duration for GET operations queries
* `batchGet`: Maximum duration for bulk GET operation queries
* `insert`: Maximum duration allowed for insert operation queries (e.g., storing Knowledge Assets)

You can override the timeouts in the .`origintrail_noderc` file by adjusting the values accordingly.

{% hint style="info" %}
**On timeouts:** Query timeouts are useful when your node is under heavy load (due to many concurrent queries), especially if you open up your query endpoint to the user who might run arbitrarily complex queries, so that they limit the load on the triple store. The values above are set to support general implementations
{% endhint %}

## Instructions for TRAC delegators

{% hint style="success" %}
In a nutshell:

* **No action is required from TRAC delegators** for the DKG V8.1.0 update process.
* During the release, staking features will be disabled for approximately 72 hours.
* It’s highly recommended to get familiar with the new Node Power and Node Health KPIs to understand how to best utilize your TRAC in the network.
{% endhint %}

### V8.1.0 launch will start with a temporary suspension of staking features

To complete the V8.1.0 update safely, **staking features will be temporarily suspended for up to 72 hours**, starting on **Monday, June 23, 2025, at 12:00 CET**. During this time, no changes to stakes or reward claims will be possible.

Once staking is locked, the smart contracts will be updated to V8.1.0, **maintaining the state (snapshot)** of staking values present at that time in V8.0.X contracts via an on-chain migration. Target time for the beginning of the on-chain migration (and latest snapshot time) is at&#x20;

* Timestamp **1750683600** ( June 23rd 15:00 CET)&#x20;
* NeuroWeb: Snapshot Block - 9777120
* Base : Snapshot Block - 31948000
* Gnosis: Snapshot Block - 40731720

### No more V6 token migration required

Unlike the V8.0.0 release, where delegators needed to migrate their stake from V6 to V8.0 (possible through the Staking Dashboard), **with the V8.1.0 release, the need for this migration goes away** because of the Random Sampling updates. This means that with DKG V8.1.0, “Node Share tokens” used previously in DKG V6 are **fully deprecated** and no longer serve any function in the DKG (not even for migration). The entire staking system now runs natively on V8 infrastructure, simplifying participation for all delegators.

If you haven’t migrated your stake from V6 yet, no action is needed — the V8.1.0 release will take care of this automatically.&#x20;

### New Staking UI and metrics

The Staking Dashboard user interface has been upgraded with new, easier-to-understand metrics:

* **Node Power:** Reflects how competitive a node is in earning rewards
* **Node Health:** Indicates how reliably a node has submitted proofs.&#x20;

You can find detailed explanations of both metrics in the Staking section [here](../../contribute-to-the-dkg/delegated-staking/).

### Upcoming reward visibility

In addition to the live reward distribution introduced with V8.1.0, two upcoming releases will make previously accrued rewards visible in the Staking Dashboard:

* V8.1.1 will display and enable claims for V6-era rewards
* V8.1.2 will unlock Tuning Period rewards for nodes active between V8.0.0 and V8.1.0

Stay tuned to the official OriginTrail community channels for updates on these follow-up releases and their expected July rollout.

## Instructions for DKG builders

{% hint style="success" %}
In a nutshell:

* V8.1.0 is **not a breaking change**, so no action is needed.
* It is **recommended to update to the latest client** versions to get all the benefits of the improvements in the V8.1.0 release.\

{% endhint %}

The DKG V8.1.0 release is not a breaking change for builders. Existing integrations, publishing flows, and query mechanisms will continue to function as expected.

That said, we strongly recommend updating to the latest versions of the DKG client libraries and tools to benefit from performance improvements, updated defaults (e.g., Blazegraph timeouts), and compatibility with upcoming features such as advanced staking visibility and network telemetry.

### To get the most out of V8.1.0:

* Update your dkg-client packages to the latest stable versions
* Review documentation on how to interact with nodes running V8.1+ (e.g., sync-aware publishing and querying)
* If you are building agent-based systems, check out the updated DKG x MCP integration to take advantage of decentralized knowledge workflows

No code migration is needed, but keeping your client stack up to date ensures you remain aligned with the evolving network.

Let us know in the [#builders-hub on Discord](https://discord.gg/hUcNmaEnSg) if you run into any issues or need assistance with upgrading.

\
