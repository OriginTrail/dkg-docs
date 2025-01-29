---
description: If you are new to TRAC delegated staking, this guide is for you!
---

# Step-by-step staking

Welcome to the step-by-step TRAC delegated staking guide! First, lets start with some prerequisites

Prerequisites:

1. You need to have some TRAC tokens to delegate. See ['How to get on TRAC(k)?' section >](https://origintrail.io/get-started/trac-token)&#x20;
2. You need to decide which blockchain you want to stake on (the [DKG supports multiple blockchains](broken-reference)).
3. Bridge your TRAC to the chosen blockchain. See instructions for bridging:
   * [Base Blockchain](../../integrated-blockchains/base-blockchain.md)
   * [NeuroWeb](../../integrated-blockchains/neuroweb.md)
   * [Gnosis ](../../integrated-blockchains/gnosis-chain.md)[Chain](../../integrated-blockchains/gnosis-chain.md)
4. Have some gas fee tokens available on the chosen network:
   * Base Mainnet: ETH on Base
   * NeuroWeb: NEURO
   * Gnosis Chain: xDAI

{% hint style="warning" %}
_If you are staking on NeuroWeb, please make sure that you update both **"Max base fee"** and "**Priority fee**" to **0.00000001** before signing transactions._
{% endhint %}

### **TRAC staking using the Staking Dashboard:**

{% hint style="info" %}
For the purpose of this tutorial we have been using Metamask wallet extension.
{% endhint %}

Once you have confirmed that you have both gas tokens and TRAC tokens available, you can proceed to the Staking Dashboard at [https://staking.origintrail.io/](https://staking.origintrail.io/) and follow the steps below:\


**Step 1:** Click on the **'Connect wallet'** button in the top right corner of the navigation bar and follow the prompts to connect your wallet to the interface.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-27 at 15.24.48.png" alt="" width="375"><figcaption></figcaption></figure>



**Step 2:** Make sure you have selected the right blockchain in your wallet.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-27 at 15.25.21.png" alt="" width="327"><figcaption></figcaption></figure>



**Step 3:** The Staking Dashboard shows a list of all the Core Nodes hosting the DKG. This table shows different information, such as:

* The node name,&#x20;
* Which blockchain it's connected to,&#x20;
* How much stake does a node have,&#x20;
* The node's ask,&#x20;
* The node's operator fee,&#x20;
* Reward statistics, and other.&#x20;

**To delegate your TRAC tokens, you need to pick one or more nodes you believe are going to perform best for the network (on the basis of criteria explained on the** [**Delegated staking page**](./)**) and which has enough "room" to take TRAC (meaning less than 2M TRAC already staked, 2M being the maximum amount of TRAC per one node)**

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-27 at 15.26.46.png" alt="" width="563"><figcaption></figcaption></figure>



**Step 4:** Once you click on a Core Node, a staking pop-up opens with the option to delegate or withdraw TRAC tokens from the node. Proceed by pressing the **'Delegate'** button

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-27 at 15.28.41.png" alt=""><figcaption><p>Delegating popup</p></figcaption></figure>



**Step 5:** Enter the amount of TRAC you would like to delegate and press the **'Delegate TRAC'** button. The delegation process will require two transactions: one to increase the allowance and another to confirm the contract interaction.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-27 at 15.29.46.png" alt=""><figcaption></figcaption></figure>



**Step 6:** To confirm that the process was successful, check your TRAC delegation by going to the **'My delegations'** tab above the table with the nodes and verify that your delegation is listed there. Additionally, ensure that the stake amount on the node has increased following the successful delegation.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-27 at 15.30.30.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you encounter any issues during the staking process or require assistance, please contact our technical support team by sending an email to **tech@origin-trail.com**.
{% endhint %}
