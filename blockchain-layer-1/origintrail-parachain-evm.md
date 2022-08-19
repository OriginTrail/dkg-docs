# OriginTrail Parachain EVM

OriginTrail Parachain supports two types of blockchain accounts:

* Substrate accounts (Polkadot native, used with Polkadot wallets such as Polkadot.js), which are used for native OriginTrail Parachain functionality
* Ethereum accounts (Ethereum native, used with Ethereum wallets such as Metamask), which are used within the EVM

This enables the OriginTrail Parachain users to get benefits of "both worlds". To enable the EVM functionality, users need to create a mapping between their Substrate and Ethereum accounts (wallets) to the OriginTrail Parachain through a one time transaction, which can be performed through [this interface](https://parachain.origintrail.io/parachain-account-mapping) (before going to this interface you need to fund your wallets with OTP and TRACE test tokens, instructions are available here).

The interface uses an Ethereum wallet to sign the Substrate address provided and submit it as a transaction to the OriginTrail Parachain, so that the Parachain runtime can verify that the two addresses are indeed owned by the same user.

Once the mapping is completed, you can use the OriginTrail Parachain EVM functionalities.

{% hint style="info" %}
The account mapping interface doesn't have access to your wallet private keys and only uses your wallet signing and transaction functionalities to submit a valid transaction.&#x20;
{% endhint %}

### Why the need for two accounts?

OriginTrail Parachain uses the native Substrate address format (H256), which is different from the Ethereum address format (H160), therefore it needs to enable usage of both in order to perform both Substrate native functionalities and Ethereum compatible activity.&#x20;

The Substrate address (wallet) is used for all native OriginTrail Parachain functionality such as OTP transactions, collator delegation, governance features etc, while the Ethereum address (wallet) is used for operations within the EVM environment, which include OriginTrail DKG v6 transactions, deploying & interacting with Ethereum smart contracts deployed on OriginTrail Parachain and similar.

In the future, the OriginTrail DKG is expected to move beyond the EVM implementation to a Substrate native one, introducing capabilities such as Graph Contracts.

### Which wallets can be used with OriginTrail Parachain then?

For all interactions with the EVM (including OriginTrail DKG v6), you can use any Ethereum compatible wallet, such as e.g. Metamask in conjuction with a hardware wallet.

For Substrate functionality, you need to use Substrate based wallets.&#x20;

### Do I need to perform this mapping for my OriginTrail v6 nodes?

The mapping should be performed for both management and operational wallets, otherwise the node will not be able to start.
