---
icon: diagram-project
---

# Delegated Staking (V8)

Being a decentralized system, the OriginTrail DKG enables all ecosystem stakeholders owning TRAC to contribute their economic stake into the functioning of the network for utility. Delegated staking involves locking up TRAC for contributing to the DKG security on selected DKG nodes. DKG node rewards are shared between the TRAC stake delegators.

<figure><img src="../../.gitbook/assets/Staking updates.png" alt=""><figcaption></figcaption></figure>

## TRAC delegated staking mechanics

For a DKG node to be eligible to host a portion of the DKG and receive TRAC network rewards, its TRAC stake plays a crucial role. Set at the minimum of 50 000 TRAC on a particular blockchain, stake has an important role in ensuring security of the DKG. The DKG node operators can contribute to the node stake on their own or by attracting more TRAC to their stake through delegated staking.&#x20;

There are 2 roles involved in delegated staking -  **node operators** and **TRAC delegators.**

**Node operators** are network participants who choose to host and maintain network nodes (specialized DKG software running servers). Nodes store, validate and make knowledge available to AI systems. They receive $TRAC rewards for this service. All nodes together form a permissionless market of DKG services, competing for their share of network TRAC rewards.

**Delegators** lock up their TRAC for contributing to the DKG security on selected DKG nodes and increasing their chance of capturing TRAC network rewards. The rewards that end up being captured by the DKG node are then shared between the TRAC stake delegators. The delegated tokens are locked in a smart contract and are never accessible to the node operators.

Note that node operators and node delegators are not distinct - you can be both at the same time.

{% hint style="info" %}
Contrary to inflationary systems, TRAC staking is strictly utility-based and rewards are generated through DKG usage via knowledge publishing fees.
{% endhint %}

#### How do delegators earn TRAC fees?

As knowledge publishers create Knowledge Assets on the DKG, they lock an appropriate amount of TRAC tokens in the DKG smart contracts. The TRAC amount offered has to be high enough to ensure enough DKG nodes will store it for a specific amount of time. The nodes then commit to storing the knowledge assets for a specific amount of time, measured in **30 day periods called epochs**.\


At the end of each epoch, DKG nodes "prove" that they are providing DKG services to the DKG smart contracts, which in return unlocks  TRAC rewards locked initially by the knowledge publisher.&#x20;

\
Many nodes can compete for the same TRAC reward on the basis of their total stake, node ask and publishing factor. Node rewards are a function of 4 parameters, in order of importance:

1. **Node uptime & availability,** in positive correlation, as nodes need to prove their commitment of hosting the DKG by submitting proofs to the blockchain (through the new V8 random sampling proof system)
2. **TRAC Stake security factor,** in positive correlation - the more stake a node attracts, the higher the security guarantees and therefore the higher chance of rewards (same as in V6)
3. **Publishing factor,** in positive correlation - the more new knowledge has been published via a specific core node (measured in TRAC tokens), the higher the chance of rewards,&#x20;
4. **Node ask,** in negative correlation - the nodes with asks lower than the current network fee are positively impacting the system scalability, and therefore have a higher chance of rewards.

More details are presented in[ OT-RFC-21](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-21_Collective_Neuro-Symbolic_AI/OT-RFC-21%20Collective%20Neuro-Symbolic%20AI.pdf)

After claiming the rewards, they are **automatically restaked, increasing the nodes overall stake by the amount of collected rewards.**

In order to introduce a level of predictability of network operations, withdrawing tokens is subject to an unbonding period of 28 days.



{% hint style="warning" %}
If you want to withdraw tokens in order to delegate to another node on the same network (blockchain) - you **do not** have to wait 28 days! See Broken link
{% endhint %}



{% hint style="success" %}
Delegated staking is a non-custodial system, so the node operator has no access to the locked TRAC tokens at any time.
{% endhint %}

Each node operator can also set an “**operator fee**” which is taken as a percentage of the TRAC rewards deducted each time when a node claims rewards from a knowledge asset. The remaining TRAC fee is then split proportionally to the share of staked tokens across all delegators.

{% hint style="info" %}
**Example**: if a node accumulated **1000 TRAC** tokens in the previous period, and the node has two delegators both of 50% share, and the operator\_fee is 10%:

Comment

* the node operator will receive 100 TRAC (10%)\
  Comment
* each delegator receives 450 TRAC (50% of the remaining 900 TRAC)
{% endhint %}

#### If you are running a Core node

If you are running a DKG Core node you can delegate TRAC tokens to your node in the same way as others. It is recommended you delegate TRAC tokens as well, signalling your commitment to the network via economic stake - this provides a trust signal to other delegators.

To understand how to set up your operator fee, follow the OOOOOOVO nstructions for node setup. Note that changing your operator fee incurs a 28 day delay, balancing the 28 day delay delegators experience when withdrawing stake from your node.



(image)Depiction of delegating and withdrawing of TRAC from DKG smart contracts

\
**Have questions?**

Drop by our [Discord](https://discordapp.com/invite/FCgYk2S) or [Telegram group](https://t.me/origintrail) and feel free to post it there. Make sure to follow our official announcements and stay safe!

Happy staking! 🚀

\
\
