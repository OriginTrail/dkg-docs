---
description: Instructions for Staking Your TRAC on the Base blockchain
---

# Staking TRAC on Base

These instructions will guide you through the process of staking your TRAC tokens on the Base network via the staking interface.

## Requirements:

1. TRAC on Base network
2. Base ETH to pay for fees

{% hint style="success" %}
The process of bridging TRAC tokens to Base is described [here](https://docs.origintrail.io/integrated-blockchains/base-blockchain).
{% endhint %}

{% hint style="warning" %}
For the purpose of creating these instructions, we used the Base Sepolia (testnet). The process is exactly the same for the Base mainnet.
{% endhint %}



**The following smart wallets are supported by the interface for staking in Base:**

1. MetaMask
2. CoinBase
3. OKX Wallet

### Process steps:

{% hint style="info" %}
For the purpose of this tutorial we have been using Metamask wallet extension.
{% endhint %}

Once you have confirmed that you have both Base ETH and TRAC tokens available on the Base blockchain and that your Metamask is connected to the Base blockchain, you can proceed to the staking interface at [https://dkg.origintrail.io/staking](https://dkg.origintrail.io/staking) and follow the steps below:

1. Click on the '**Connect Wallet**' button in the top right corner of the navigation bar and follow the prompts to connect your wallet to the interface.
2. Use the '**Filter by Blockchain**' dropdown to select the Base blockchain, which will filter and display all available nodes on this network along with their staking information.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-21 at 12.44.41.png" alt=""><figcaption><p>Filter out Base nodes</p></figcaption></figure>

3. Once you've decided which node you want to stake your TRAC to, click on the 'Manage Stake' button next to the desired node on the right side of the table. Read the disclaimer and press 'I understand'.

{% hint style="warning" %}
You can stake your TRAC only to nodes which have less than 2,000,000 TRAC stake delegated to them.&#x20;
{% endhint %}

3. When the staking pop-up opens, you'll have the option to delegate or withdraw TRAC tokens from the node. Proceed by selecting 'Delegate TRAC'.
4. After clicking on 'Delegate TRAC,' a field to enter the amount of TRAC you wish to stake will appear on the right side of the pop-up. Enter the amount of TRAC you want to delegate as your stake and click on 'Delegate':

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-21 at 12.56.45.png" alt=""><figcaption><p>Delegation process</p></figcaption></figure>

5. The delegation process will require two transactions: one to increase the allowance and another to confirm the contract interaction.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-21 at 12.59.35.png" alt=""><figcaption><p>Sign transactions</p></figcaption></figure>

6. Once both transactions are signed and confirmed, you should see a 'Stake delegated successfully' message appear:

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-21 at 12.59.52.png" alt=""><figcaption><p>Stake delegated successfully</p></figcaption></figure>

7. To confirm that the process was successful, check your TRAC delegation by going to the 'My Delegation' tab above the table with the nodes and verifying that your delegation is listed there. Additionally, ensure that the stake amount on the node has increased following the successful delegation.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-21 at 13.05.55.png" alt=""><figcaption><p>My delegations</p></figcaption></figure>

{% hint style="info" %}
If you encounter any issues during the staking process or require assistance, please contact our technical support team by sending an email to **tech@origin-trail.com**.
{% endhint %}

