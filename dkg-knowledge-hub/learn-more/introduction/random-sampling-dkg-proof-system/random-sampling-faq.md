# Random Sampling FAQ



**How do I choose which Core Node to delegate my TRAC to?**

The system is designed in such a way as to incentivize positive network behavior (see more in [.](./ "mention")). That means your delegated TRAC will help increase a Core Node's chances of receiving rewards, while the nodes with the best characteristics receive a higher share of the rewards. To pick a node, consider the following metrics (available in the [Staking Dashboard](https://staking.origintrail.io))

* **Node Power** — Shows how competitive the node is in earning rewards. Higher Node Power means a higher chance of rewards.&#x20;
* **Node Health** — Reflects reliability and uptime. Higher Node health means a higher chance of rewards.
* **Operator fee** — The percentage cut the node takes from rewards to cover the cost of its operations (e.g., blockchain transaction fees).&#x20;

You’re generally looking for a node with high power, high health, and a reasonable fee.



**Can a node operator take my stake?**

No. Delegated TRAC tokens are locked in smart contracts. Node operators cannot access or withdraw your stake. You can withdraw your tokens yourself after initiating a withdrawal and completing the 28-day unstaking period.



**What happens if my Core Node goes offline during an upgrade?**

DKG is designed to be resilient. If your node goes offline (e.g., for maintenance), it won’t be slashed, but it may miss proof submissions during that downtime. This means:

* Your node’s **Node Health** score may decrease.
* You may receive lower rewards for that epoch.

As a node operator, maintaining your node uptime is one of the highest priorities, and it is, therefore, incentivized. You can use the **DKG Sync** feature to catch up on missed data and rejoin the network without penalty.



**Will my node be penalized if it misses a proof?**

No, there is no slashing or loss of stake for missing a proof. However, missing proofs results in a **zero score** for that proof period, which reduces your total rewards for the epoch. Node Health will also decrease temporarily.



**What’s the timeline for the V8.1 reward system rollout?**

The rollout is structured as follows:

1. **V8.1.0** – Random Sampling live (current proofs and rewards)
2. **V8.1.1** – V6 rewards compatibility module
3. **V8.1.2** – Tuning Period rewards module

These are released in quick succession as development and testing complete, rolling out in June 2025.



**How can I improve my node’s performance and earn more rewards?**

Node rewards are based on three main factors:

1. **Uptime and proof submissions** — Stay online and responsive to increase your Node Health.
2. **Publishing activity** — Publish Knowledge Assets or [open your publishing API](../../../../graveyard/everything/dkg-core-node/how-to-open-up-your-node-for-publishing.md) for others to use to increase your Node Power.
3. **Ask price** — Set a fair, competitive service fee, increasing your Node Power.
4. **Set a low operator fee** — Making your node more interesting for delegators.
5. **Promote your node** — Get TRAC holders excited to delegate their stake to your node to increase your Node Power.

**How are rewards collected for V6 and the Tuning Period?**

Both the V6 rewards and the Tuning Period (between V8.0.0 and V8.1.0) are processed using the new **Random Sampling** reward system:

* **V6 rewards** use a retroactive application of Random Sampling based on available historical data.
* **Tuning Period rewards** assume all eligible nodes had **full uptime** and participation. Rewards for this period will be claimable once V8.1.2 is released.

**Who is eligible for V6 era rewards?**

Nodes that were active during the DKG V6 period (before the V8 upgrade) are eligible to earn accumulated rewards from that era.  V6 rewards will be distributed via a compatibility module introduced in version V8.1.1, and are consolidated for the period of all 12 epochs in 2025 (1 year). Specifically, eligible nodes will submit proofs for upcoming epochs based on the same principles as those for V8 era rewards.&#x20;

Reward claiming for already elapsed epochs **will assume 100% uptime for that period (all nodes will have equal Node Health),** so nodes will compete on **Node Power**. Further technical details will be released with the V6 compatibility module release on the DKG testnet.

