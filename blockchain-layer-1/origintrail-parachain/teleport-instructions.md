# Teleport instructions

The OriginTrail Decentralized Knowledge Graph (DKG) is about to get integrated with the OriginTrail Parachain. To become part of the initial stage of OriginTrail DKG and Parachain integration, you will need to teleport TRAC from Ethereum to the OriginTrail Parachain. Read more about the process in [this blogpost](https://medium.com/origintrail/ot-rfc-12-v2-teleporting-trac-to-the-origintrail-parachain-on-polkadot-de535a9d2693) .&#x20;

#### Step 1 - Initiate teleport&#x20;

A special smart contract is deployed on Ethereum blockchain designed to lock a specific amount of TRAC tokens, to be teleported to the OriginTrail Parachain. Teleporting will occur in 15 batches, and first step of teleporting is to lock desired amount of TRAC in ongoing batch and you can do that on [teleport.origintrail.io](https://teleport.origintrail.io/)&#x20;

#### Step 2 - Sign up for Teleport bounty&#x20;

Everyone participating in the teleport process is eligible for OTP tokens awards. The exact bounty amount is different among batches, details are available [here](http://teleport.origintrail.io/).&#x20;

The bounty amount on the OriginTrail Parachain will be sent to the same wallet (combination of public and private keys) used for teleport.&#x20;

To be eligible for a bounty you are required to provide us with an Ethereum wallet that is used to initiate teleport and substrate wallet that will receive OTP bounty. Form for providing wallets is available [here](https://teleport.origintrail.io/teleport-reward-claim).&#x20;

#### Step 3 - Receive OTP bounty&#x20;

OTP bounties will be distributed to substrate wallets provided in step 2.

#### Step 4 - Map ethereum and substrate wallet&#x20;

OriginTrail Parachain supports two types of blockchain accounts:&#x20;

* Substrate accounts (Polkadot native, used with Polkadot wallets such as Polkadot.js), which are used for native OriginTrail Parachain functionality
*   Ethereum accounts (Ethereum native, used with Ethereum wallets such as Metamask), which are used within the EVM This enables the OriginTrail Parachain users to get benefits of "both worlds".&#x20;



To enable the EVM functionality, users need to create a mapping between their Substrate and Ethereum accounts (wallets) to the OriginTrail Parachain through a one time transaction, which can be performed through this interface. Once the mapping is completed, your wallets will be ready for receiving TRAC on OriginTrail Parachain. IMPORTANT: If you chose not to take part in the bounty program, you must ensure your mapped wallet has an existential amount of OTP available on the OriginTrail Parachain. Without an existential amount of OTP on your wallet, your TRAC will not be able to receive TRAC on the OriginTrail Parachain and your TRAC tokens will be unavailable until the bridge implementation is finalised.&#x20;

Account mapping interface is available [here](https://parachain.origintrail.io/parachain-account-mapping).&#x20;

#### Step 5 - Receive TRAC on OriginTrail Parachain&#x20;

Once the TRAC is deployed on OriginTrail parachain, you will receive it in the same ethereum wallet used in the teleport process for the OriginTrail Parachain.

If you experience any issues or have question, please contact the developers directly [on Discord](https://discordapp.com/invite/FCgYk2S).
