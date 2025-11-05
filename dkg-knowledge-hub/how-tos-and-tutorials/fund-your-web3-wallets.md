---
description: >-
  Before your DKG Node can publish or interact with the network, each wallet
  generated during setup needs to be funded with two types of tokens.
---

# Fund your Web3 wallets

## Fund your wallets

Before your DKG Node can operate, you’ll need to fund the wallets created during setup with two types of tokens:

* **TRAC** – for publishing Knowledge Assets.
* **Native gas token** – for transaction fees (e.g., **NEURO** on NeuroWeb, **ETH** on Base, **xDAI** on Gnosis).

On testnets, these tokens are free. Request them from each network’s faucet (e.g., via our Discord for NeuroWeb) before publishing or interacting with the DKG. To obtain your testnet tokens:

1. Join our [**Discord**](https://discord.com/invite/xCaY7hvNwD)
2. Open **#faucet-bot** channel

You can type `!help` to see more commands.

### **NeuroWeb testnet**

Please enter the following commands in our **Discord `#faucet-bot` channel**, replacing `YOUR_WALLET_ADDRESS` with your actual wallet address. Once submitted, the OriginTrail faucet bot will automatically send your test tokens:

```bash
# Fund NEURO
!fundme_neuroweb YOUR_WALLET_ADDRESS

# Fund TRAC
!fundme_neuroweb_trac YOUR_WALLET_ADDRESS
```

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-03 at 11.59.03 PM.png" alt=""><figcaption></figcaption></figure>

#### **Verify your transactions — NeuroWeb**

After requesting tokens, you can confirm that they arrived in your wallet by checking the **NeuroWeb blockchain explorer**:

* 👉 Visi&#x74;**:** [https://neuroweb.subscan.io/](https://neuroweb.subscan.io/)

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-03 at 11.59.42 PM.png" alt=""><figcaption></figcaption></figure>

* Enter **your wallet address** in the search bar.
* Navigate to the **Balance** or **Transfers** section.
* You’ll see your **TRAC** and **NEURO** testnet transactions listed there.

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-04 at 12.00.38 AM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-04 at 12.00.32 AM.png" alt=""><figcaption></figcaption></figure>

If your transaction appears, your wallet is funded and ready for use on the testnet.&#x20;

***

### **Base Sepolia testnet**

* Fund ETH on Base by following the [official Base documentation](https://docs.base.org/base-chain/tools/network-faucets).

Please enter the following commands in our **Discord `#faucet-bot` channel**, replacing `YOUR_WALLET_ADDRESS` with your actual wallet address. Once submitted, the OriginTrail faucet bot will automatically send your test tokens:

```bash
# Fund TRAC
!fundme_v8_base_sepolia_trac YOUR_WALLET_ADDRESS
```

<figure><img src="../../.gitbook/assets/Fund Base.png" alt=""><figcaption></figcaption></figure>

#### Verify your transactions – Base

If you’re deploying your DKG Node on **Base**, you can verify that your wallet was funded using the Base block explorer:

* 👉 Visit: [Base Sepolia explorer](https://sepolia.basescan.org/)

<figure><img src="../../.gitbook/assets/Base Explorer.png" alt=""><figcaption></figcaption></figure>

Enter your **public wallet address** to check for incoming tokens and completed transactions.

***

### **Gnosis Chiado testnet**

Please enter the following commands in our **Discord `#faucet-bot` channel**, replacing `YOUR_WALLET_ADDRESS` with your actual wallet address. Once submitted, the OriginTrail faucet bot will automatically send your test tokens:

```bash
# Fund xDAI
!fundme_xdai YOUR_WALLET_ADDRESS

# Fund TRAC
!fundme_chiado_trac YOUR_WALLET_ADDRESS
```

<figure><img src="../../.gitbook/assets/Fund Gnosis.png" alt=""><figcaption></figcaption></figure>

#### **Verify your transactions – Gnosis**

For nodes running on **Gnosis**, confirm your wallet balance and transaction status here:

* 👉 Visit: [Gnosis Chiado explorer](https://gnosis-chiado.blockscout.com/)

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-13 at 7.38.41 AM.png" alt=""><figcaption></figcaption></figure>

Search for your **wallet address** to see recent activity, token deposits, and confirmations.&#x20;
