---
description: >-
  There are two types of keys used by OriginTrail Nodes to securely operate on
  the network - the operational wallet and admin wallet (previously known as
  management key).
---

# Node keys explained

## Operational key

The operational wallet (or operational key) is used to perform actions on the network. Its **private key is stored on the OriginTrail node** itself and is needed to perform a multitude of operations on the DKG such as sending transactions to blockchains, signing, submitting proofs, etc. It requires blockchain native tokens in order to be able to publish transactions. (OTP for OriginTrail Parachain, MATIC for Polygon, xDAI for Gnosis, ETH for Ethereum etc). In the configuration, this key is known as “**evmOperationalWallet**”.

In case of OriginTrail Parachain, your operational wallets need to be mapped - the Substrate operational wallet should be mapped to your **evmOperationalWallet**.

## Admin key

The admin wallet, also known as the management wallet (**evmManagementWallet**) is designated for all administrative activities for your node, such as managing stake, collecting rewards, changing your nodes on-chain parameters and managing keys (such as adding or removing admin wallets). **The admin, private key is NOT stored on the node for additional safety.**

Your Substrate “Admin” wallet should be mapped to your **evmManagementWallet**.

## A note on wallets

As a node operator, you are responsible for keeping track and securely storing and managing your admin and operational keys. Do not share your keys with anyone! For the admin key specifically we recommend using additional security, such as hardware wallets (e.g. Ledger).
