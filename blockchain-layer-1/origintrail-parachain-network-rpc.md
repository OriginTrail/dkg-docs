# OriginTrail Parachain Network RPC

There are public instances of OriginTrail Parachain:&#x20;

1. OriginTrail Parachain Mainnet
   * This is the official OriginTrail Parachain that is connected to the Polkadot Relay Chain, on these parachain tokens: TRAC and OTP have value. TRAC will be teleported to this chain from Ethereum, more information [here](https://teleport.origintrail.io/).
2. OriginTrail Parachain Testnet
   * This is a parachain test network that is connected to the Rococo Relay Chain that is hosted by Parity. At the moment, this network has no utility for the OriginTrail community.
3. OriginTrail Parachain Devnet
   * This is a parachain test network that is connected to a relay chain that is hosted by TraceLabs. OriginTrail V6 beta testnet and Magnify beta version are connected to this parachain. Users on this network have test tokens without value (Test OTP and Test TRAC).

### OriginTrail Parachain Mainnet

Polkadot.js endpoint is available [here](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fparachain-rpc.origin-trail.network#/explorer).

Metamask connection parameters:

| Parameter          | Value                                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| chainID            | 2043                                                                                                         |
| Network Name       | OriginTrail Parachain Mainnet                                                                                |
| RPC Endpoint       | [https://astrosat-parachain-rpc.origin-trail.network/](https://astrosat-parachain-rpc.origin-trail.network/) |
| Token symbol       | MOTP                                                                                                         |
| Block Explorer URL | (not available at the moment)                                                                                |

Note: because of difference in token decimals between ETH (18) and OTP (12), one token in metamask will be equal to 1 milion OTPs. This issue will be resolved in the following releases.

### OriginTrail Parachain Devnet

Polkadot.js endpoint is available [here](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Flofar.origin-trail.network#/).

Metamask connection parameters:

| Parameter          | Value                                                                                  |
| ------------------ | -------------------------------------------------------------------------------------- |
| chainID            | 2160                                                                                   |
| Network Name       | OriginTrail Parachain Devnet                                                           |
| RPC Endpoint       | [https://lofar-tm-rpc.origin-trail.network](https://lofar-tm-rpc.origin-trail.network) |
| Token symbol       | MOTP                                                                                   |
| Block Explorer URL | (not available at the moment)                                                          |

Note: because of difference in token decimals between ETH (18) and OTP (12), one token in metamask will be equal to 1 milion OTPs. This issue will be resolved in the following releases.
