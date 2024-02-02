---
description: Employ your TRAC in the OriginTrail Decentralized Knowledge Graph
---

# 🚀 Delegated staking

The OriginTrail Decentralized Network is a permissionless system that hosts the Decentralized Knowledge Graph (DKG) and is ran by the OriginTrail community. Anyone can run an OriginTrail DKG node ([installation instructions can be found here](../node-setup-instructions/)).&#x20;

For a DKG node to be eligible to host a portion of the DKG and receive publishing fees (to be a hosting node), it has to accumulate a **minimum of 50 000 TRAC** tokens as stake in the network on a particular blockchain. Network stake provides the economic security layer and can be provided by anyone owning TRAC tokens by the notion of "delegated staking".&#x20;

Therefore we distinguish 2 roles supporting DKG infrastructure - **node operators** and **TRAC delegators**.

**Node operators** are usually technically savvy individuals and organizations who choose to sovereignly host and maintain network nodes (specialized DKG software running servers), for the purpose of gaining value from knowledge publishing fees, access to the knowledge in the DKG and its technology. All nodes together form a permissionless market for DKG services, competing for their share of network stake and operational fees.

**Delegators** are providers of TRAC tokens who participate in the market by delegating their TRAC tokens to nodes (ran by node operators) in a non-custodial way, helping the nodes achieve a better market position in the network by signalling through economic stake.&#x20;

Note that node operators and node delegators are not distinct - you can be both at the same time.&#x20;

{% hint style="info" %}
Contrary to inflationary systems, TRAC staking is strictly utility based and rewards are funded through DKG usage via knowledge publishing fees.&#x20;
{% endhint %}

### How does DKG delegated staking work?

Once you delegate TRAC tokens to a node, in return you receive **node** “**share tokens**” (similar to Uniswap LP tokens). Each node deployed on OriginTrail has a respective, node-specific, mintable and burnable 18 decimal ERC20 token created for it on the desired blockchain during node deployment, with the token symbol and name set by the node operator (an example of such a node share token on NeuroWeb blockchain can be found [here](https://neuroweb.subscan.io/erc20\_token/0x98136e72d70b0c52bb253b9bb6902956d213f117?tab=transfers)).&#x20;

When you delegate TRAC tokens to a node, they are locked inside DKG smart contracts, a proportional amount of node share tokens is minted for you and sent to your delegating wallet address.  To withdraw your TRAC, you simply burn the share tokens via the DKG smart contracts, unlocking your TRAC tokens. Withdrawing tokens is subject to a withdrawal delay of 28 days.

{% hint style="success" %}
Delegated staking is a non-custodial system, so the node operator has no access to the locked TRAC tokens at any time.
{% endhint %}

\
Each node can also set an _**operator\_fee**_ - taken as a percentage of the TRAC fee, which is deducted from each knowledge asset publishing fee, and is directed to the node operator prior to sharing with other delegators. The remaining TRAC fee is then split in proportion to the amount of share tokens among all delegators.

{% hint style="info" %}
**Example**: if a node accumulated **1000 TRAC** tokens in the previous period, and the node has two delegators both of 50% share, and the operator\_fee is 10%:

* the node operator will receive 100 TRAC (10%)
* each delegator receives 450 TRAC (50% of the remaining 900 TRAC)
{% endhint %}

### How to delegate your TRAC&#x20;

First navigate to:

* Testnet [DKG Explorer Staking D](https://dkg-testnet.origintrail.io)[ashboard](https://dkg-testnet.origintrail.io/staking)
* Mainnet [DKG Explorer Staking Dashboard ](https://dkg.origintrail.io/staking)(launching imminently)

{% hint style="warning" %}
The DKG Staking dashboard is currently in beta and still in development, and is available on the Testnet DKG explorer. As you might discover bugs and UX issues we'd love to hear you report them in our #staking [Discord](https://discordapp.com/invite/FCgYk2S) channel. We expect the productive Staking Dashboard release together with 6.2.0 mainnet release.
{% endhint %}

* Pick one or more nodes to which you'd like to delegate your TRAC tokens. Consider the node's performance and characteristics (such as the operator fee, accumulated stake, information about the node operator and the amount of stake provided by them, etc.)
* Click the "Delegate stake" button to open the delegation popup

<figure><img src="../../.gitbook/assets/staking-ui.png" alt="" width="563"><figcaption><p>Indicative dashboard</p></figcaption></figure>

* Designate how much TRAC you want to delegate to this node in the input box
* Click the **Delegate button** to initiate the delegation process. This will entail two blockchain transactions - the token **approval** transaction, and the TRAC **token transfer** transaction**.**

<figure><img src="../../.gitbook/assets/delegate.png" alt="" width="563"><figcaption><p>Indicative Delegation popup modal</p></figcaption></figure>

* Once the transactions are executed successfully, you will receive node share tokens in your wallet. (make sure to keep those tokens to be able to withdraw your TRAC rewards later)
* That's it, you have successfully delegated TRAC tokens to a DKG node!

### How can you collect TRAC rewards?

Over time the amount of TRAC tokens earned by the node will grow (as the node accumulates knowledge asset fees, increasing the node's total stake). A portion, proportionate to the amount of share tokens you own to that node, will be available for you to withdraw (after the deduction of the operator fee). You can initiate the withdrawal of the accumulated TRAC at any time by burning a portion of your node share tokens. The withdrawal is performed in two transactions, with a 28 day delay.&#x20;

<figure><img src="../../.gitbook/assets/withdrwa.png" alt="" width="553"><figcaption><p>Indicative Withdrawal popup modal</p></figcaption></figure>



{% hint style="warning" %}
The Delegated Staking feature is initially launched on Gnosis blockchain where the OriginTrail core developers will confirm the staking implementation correctness and perform bug bounty on staking smart contracts. After successful confirmation of the implementation, the delegated staking feature will be rolled out to NeuroWeb and other blockchains.
{% endhint %}

### If you are running a node

If you are running a DKG node you can delegate TRAC tokens to your node in the same way as described above (effectively assuming the role of a delegator). It is recommended you delegate TRAC tokens as well, signalling your commitment to the network via economic stake as well - this provides a trust signal to other delegators.

To understand how to set up your operator fee, follow the [node-setup-instructions](../node-setup-instructions/ "mention") instructions for node setup. Note that changing your operator fee incurs a 28 day delay, balancing the 28 day delay delegators experience when withdrawing stake from your node.&#x20;

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Depiction of delegating and withdrawing of TRAC from DKG smart contracts</p></figcaption></figure>

### Have questions?

Drop by our [Discord](https://discordapp.com/invite/FCgYk2S) or [Telegram group](https://t.me/origintrail) and feel free to post it there. Make sure to follow our official announcements and stay safe!

Happy staking! :rocket:

