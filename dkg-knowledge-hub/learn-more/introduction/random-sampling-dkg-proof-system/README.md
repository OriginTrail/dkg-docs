# Random Sampling & proofs explained

The **Random Sampling** proof system in OriginTrail DKG V8 is a decentralized, scalable, and lightweight mechanism for ensuring the **availability of knowledge**, **incentivizing network participation**, and **fairly distributing publishing rewards**. This page introduces its purpose, mechanics, and how it connects node runners, token delegators, and publishers in the DKG ecosystem.

### Why does Random Sampling exist

For a stable functioning decentralized system, service and data availability cannot be assumed — it must be proven. In the DKG, **Core Nodes are responsible for hosting and serving Knowledge Assets**. But how can the network be sure they actually do?

Random Sampling is a **Proof-of-Knowledge (PoK)** mechanism that enables the network to continuously and randomly challenge nodes to prove that they store specific data. Nodes are challenged by blockchain smart contracts, which govern the system in a decentralized way. In particular, the system:&#x20;

* Ensures that data remains available over time
* Rewards nodes that are consistently online and engaged
* Provides a fair, automated way to distribute fees paid by publishers

It replaces earlier, less scalable methods used in DKG V6 with a vastly more efficient system, capable of supporting **100 billion+ Knowledge Assets.**

### Where do the node rewards come from?

The DKG tokenomics is based on the TRAC utility token, a non-inflationary, fully circulating ERC-20 token launched in 2018 on the Ethereum blockchain. The node rewards are all utility-based — paid by the knowledge publishers, which cover the DKG service fees to node runners. There are no inflationary rewards.&#x20;

### Network goals and incentives

The DKG network is designed to reward:

* **System uptime** — Nodes must submit frequent, valid proofs of knowledge availability
* **Data correctness** — Proofs are only possible if a node hosts the challenged data in the exact form published by the publishers
* **High publishing factor** — Nodes that contribute new knowledge by opening their API for publishing to the DKG earn higher scores
* **Stake commitment** — The more TRAC tokens staked to a node by delegators, the greater the reward share
* **Service efficiency** — Lower service ask fees improve system competitiveness and incentivise adoption

These incentives align node behavior with the network's goals: fast, reliable, and decentralized knowledge hosting.

### Staking implementation details

The DKG staking system allows any TRAC token holder to participate in the network by **delegating tokens to Core Nodes**. This supports the network’s operation and entitles delegators to a share of the publishing rewards.

{% hint style="info" %}
Visit [this page ](../../../../contribute-to-the-dkg/delegated-staking/)for a step-by-step guide on how to stake TRAC tokens.
{% endhint %}

#### Non-custodial system

The DKG delegated staking system is **fully non-custodial,** meaning TRAC delegators do not provide access to their tokens to the DKG Core Node runners or any third party. The tokens are securely locked in the DKG smart contracts and can only be transferred by the token delegator through the smart contract functions.

#### Staking Dashboard

The Staking Dashboard is an easy-to-use web page that enables DKG staking interactions, as well as monitoring node performance and rewards over time. Staking can be done via any EVM-compatible wallet.&#x20;

#### Reward claiming and restaking

* Rewards are **not automatically claimed —** they must be explicitly claimed using the `claimRewards` function, for each epoch individually.
* When claimed, rewards are **automatically re-staked** into the delegator's active stake. This increases both the delegator’s stake and the total stake of the node, enhancing future reward shares.
* Rewards can only be claimed for **completed and finalized epochs**. The system enforces this to ensure accurate score calculation.

#### Who can trigger reward claiming?

* **Core Nodes** are naturally incentivized to claim rewards for all their delegators, since doing so increases their total stake and therefore reward performance. This is the preferred option to the alternative, which is having delegators each triggering the claiming transaction manually for each epoch.
* To ensure fairness, **delegators can also claim rewards for themselves**, particularly in cases where the node is offline or unresponsive. In this way, delegators are in no way dependent on the node operation and can withdraw their tokens at any time.&#x20;

#### Withdrawal period

* All delegated stakes are subject to a **28-day withdrawal period**.
* A delegator must initiate a withdrawal request and wait for the withdrawal period to elapse before accessing their tokens.

***

### Random sampling proof system — key concepts

| Concept                       | Description                                                               |
| ----------------------------- | ------------------------------------------------------------------------- |
| **Knowledge Sector**          | A virtual shard of the DKG, hosted by a subset of Core Nodes              |
| **Knowledge Collection (KC)** | A group of Knowledge Assets minted together (stored as an NFT collection) |
| **Chunk**                     | A 32-byte unit of a Knowledge Collection used for Merkle hashing          |
| **Epoch**                     | A fixed-length interval (e.g., 30 days) over which rewards are calculated |
| **Proof Period**              | A short cycle (e.g., 30 minutes) in which nodes are challenged            |

***

### How Random Sampling works

1. **Random challenge generation**
   * At the start of each _proof period_, the DKG smart contract randomly selects a chunk from a Knowledge Collection for each Core Node.
   * Example: Node1 receives challenge `(KCID = 1012, chunk = 23)`.
2. **Node responds with Merkle proof**
   * The node computes a Merkle proof for the chunk and submits it on-chain.
   * The contract verifies the proof by recomputing the Merkle root.
3. **Score assignment**
   * If the proof is valid, a _proofScore_ is computed based on:
     * Node stake
     * Publishing factor
     * Uptime
     * Ask price
4. **Epoch score aggregation**
   * All valid scores in the epoch are summed: `totalNodeScore = ∑ proofScore`
5. **Reward distribution**
   * At the end of each epoch, accumulated publisher fees are distributed to:
     * **Core Node operators**, based on totalNodeScore and their operator fee
     * **Delegators**, proportionally to their stake and staking duration



A high-level sequence diagram below illustrates the entire lifecycle from publishing, staking, service provisioning, reward claiming, and token withdrawals.&#x20;

<figure><img src="../../../../.gitbook/assets/V8 diagrams - Radnom sampling.png" alt=""><figcaption></figcaption></figure>

***

### Delegators, node Runners, publishers: Roles explained

| Role                    | Description                                                                                                                                                                                                                                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Node operator**       | <p>Operates a DKG Core Node, which hosts the DKG, submits proofs, and earns node rewards. Node operators are the "system administrators" of the DKG, and the better their nodes run, the better their TRAC reward performance will be.<br>For their services, they set an Operator fee (funded by publishing as well).</p> |
| **TRAC delegator**      | Stakes TRAC to a Core Node to earn a share of its rewards. Delegators curate nodes based on their performance in the network — uptime, stake, publishing factor, and service ask. One delegator can stake TRAC to multiple Core Nodes simultaneously.                                                                      |
| **Knowledge publisher** | Uses the public DKG for knowledge creation and querying. Pays fees to mint Knowledge Assets and fund node incentives                                                                                                                                                                                                       |



***

### Time dimension: Epochs and proof periods

To coordinate time-based operations across the DKG, it uses a system of **epochs** and **proof periods**, implemented by the `Chronos` and `RandomSampling` contracts.

#### Epochs

An **epoch** is a long-form unit of time (typically 30 days) used to:

* Define the lifespan of Knowledge Assets
* Track and reset reward cycles
* Anchor delegator scoring and reward eligibility

Epochs are calculated from a global start time using:

```
(currentTimestamp - START_TIME) / EPOCH_LENGTH + 1
```

This ensures that all participants are synchronized to the same epoch regardless of timezone or local clock.

{% hint style="info" %}
Synchronized epochs have been introduced in V8, as an evolution of decoupled epochs in the previous version of the DKG (V6), which enabled major DKG scalability improvements on the blockchain layer.
{% endhint %}

#### Proof periods

A **proof period** is a much shorter window of time (e.g., 30 minutes) in which Core Nodes must submit a proof in response to a randomized challenge. Within each epoch, there are many proof periods.

Each proof period:

* Begins at a calculated block interval based on average block time and on-chain parameters
* Triggers a new challenge to each eligible Core Node
* Allows nodes to submit a Merkle proof for a randomly selected chunk from a Knowledge Collection

#### Coordination between epochs and proof periods

* The `Chronos` contract tracks the current epoch, calculates timestamps for any epoch, and determines when new epochs begin.
* The `RandomSampling` contract coordinates proof periods within the current epoch by:
  * Calculating the active proofing block window
  * Generating unique challenges per node
  * Tracking proof submissions for reward calculation

This two-layered time model enables the DKG to scale efficiently by decoupling frequent proof submissions from the slower epoch-based reward distribution.

### Scalability and performance

* Challenges are randomized and verifiably stored on-chain
* Nodes only prove small slices of data per period → no full graph needed
* Gas cost per node per day is <100M gas
* Efficient sector-based storage allows horizontal scaling
* Proofs are computed off-chain and verified cheaply on-chain

The system is robust even with **billions of knowledge chunks** across **hundreds of nodes**, ensuring future-proof operation.

