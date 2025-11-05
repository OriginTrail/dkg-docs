---
cover: ../../../../.gitbook/assets/OT x BASE doc visual.jpg
coverY: 0
---

# Connect to Base

Since 6.5.0 release, OriginTrail DKG nodes support Base blockchain (Mainnet). Learn more about how to use your node with Base below.

## Mainnet node setup instructions (Base)

Since the 6.5.0 release, your OriginTrail DKG node can operate on Base network. In order to connect your node to Base, please refer to the instructions below.

### 1. Obtain Base Archival RPC Endpoint

Refer to the [official Base documentation](https://docs.base.org/docs/) or search for the RPC providers that offer Base RPC's.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.
{% endhint %}

### 2. Acquire TRAC and ETH tokens

List of available exchanges is available on our [website](https://origintrail.io/technology/trac-token).

Instructions on how to bridge TRAC and ETH tokens to Base blockchains can be found [here](https://docs.origintrail.io/integrated-blockchains/ethereum-ecosystem/base-blockchain#bridging-trac-to-base).

### 3. Update DKG node configuration

Open the **.origintrail\_noderc** configuration file of your DKG node located inside the **ot-node** directory. Within the config, locate the **"blockchain"** object, and add the following object to the **"implementation"** array, specifying your RPC endpoint and wallets.&#x20;

As `operationalWallets` is an array, you can define multiple operational wallets.

```json
"base:8453": {
  "enabled": true,
  "config": {
    "sharesTokenSymbol": "shares_token_symbol",
    "sharesTokenName": "shares_token_name",
    "operatorFee": <value_between_0_and_100>,
    "rpcEndpoints": [
      "<Your Base RPC endpoint>/"
    ],
    "operationalWallets": [
      {
        "evmAddress": "0x0bf...",
        "privateKey": "0x1e3..."
      }
    ],
    "evmManagementWalletPublicKey": "0xd09..."
   }
 }
```

After adding **"base:8453"**, your **"blockchain"** object in the configuration file should look like the one below:

```json
...
    "blockchain": {
      "defaultImplementation": "otp:2043",
      "implementation": {
        "otp:20430": {
          "enabled": true,
          "config": {
            "sharesTokenSymbol": "shares_token_symbol",
            "sharesTokenName": "shares_token_name",
            "operatorFee": <value_between_0_and_100>,
            "operationalWallets": [
              {
                "evmAddress": "0x0bf...",
                "privateKey": "0x1e3..."
              }
            ],
            "evmManagementWalletPublicKey": "0xd09..."
          }
        },
        "gnosis:100": {
          "enabled": true,
          "config": {
            "sharesTokenSymbol": "shares_token_symbol",
            "sharesTokenName": "shares_token_name",
            "operatorFee": <value_between_0_and_100>,
            "rpcEndpoints": [
              "https://archive-rpc.chiado.gnosischain.com/"
            ],
            "operationalWallets": [
              {
                "evmAddress": "0x0bf...",
                "privateKey": "0x1e3..."
              }
            ],
            "evmManagementWalletPublicKey": "0xd09..."
           }
         },
         "base:8453": {
           "enabled": true,
           "config": {
           "sharesTokenSymbol": "shares_token_symbol",
           "sharesTokenName": "shares_token_name",
           "operatorFee": <value_between_0_and_100>,
           "rpcEndpoints": [
              "<Your Base RPC endpoint>"
           ],
           "operationalWallets": [
            {
              "evmAddress": "0x0bf...",
              "privateKey": "0x1e3..."
            }
          ],
          "evmManagementWalletPublicKey": "0xd09..."
         }
       }
      }
    },
...
```

## 4. Restart your node

You can proceed and restart your node to confirm that it will start communicating with Base.

{% hint style="warning" %}
Once again, make sure that your operational wallet has some Base ETH in order for your OriginTrail DKG node to be able to create the profile on the new network.
{% endhint %}

```
otnode-restart && otnode-logs
```

If you added everything successfully, your node will show the log that says “**blockchain module initialized with implementation: base:8453**”.

If you have come this far and your node logs are not showing any errors, you're node is successfully set up!&#x20;



## Testnet node setup instructions (Base Sepolia)

Since the 6.5.0 release, your OriginTrail DKG node can operate on Base Sepolia network. In order to connect your node to Base Sepolia, please refer to the instructions below.

### 1. Obtain Base Sepolia Archival RPC Endpoint

Refer to the [official Base documentation](https://docs.base.org/docs/) or search for the RPC providers that offer Base RPC's.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.
{% endhint %}

### 2. Acquire TRAC and Sepolia ETH test tokens

Please refer to [Base official documentation](https://docs.base.org/docs/tools/network-faucets) to see the list of available faucet providers.\
In order to obtain TRAC tokens on Base Sepolia, please contact **tech@origin-trail.com.**&#x20;

{% hint style="info" %}
TRAC faucet will be enabled soon via Discord bot, same as for the other networks and the usage instructions will be provided here.
{% endhint %}

### 3. Update DKG node configuration

Open the **.origintrail\_noderc** configuration file of your DKG node located inside the **ot-node** directory. Within the config, locate the **"blockchain"** object, and add the following object to the **"implementation"** array, specifying your RPC endpoint and wallets.&#x20;

As `operationalWallets` is an array, you can define multiple operational wallets.

```json
"base:84532": {
  "enabled": true,
  "config": {
    "sharesTokenSymbol": "shares_token_symbol",
    "sharesTokenName": "shares_token_name",
    "operatorFee": <value between 0 and 100>,
    "rpcEndpoints": [
      "<Your Base Sepolia RPC endpoint>/"
    ],
    "operationalWallets": [
      {
        "evmAddress": "0x0bf...",
        "privateKey": "0x1e3..."
      }
    ],
    "evmManagementWalletPublicKey": "0xd09..."
   }
 }
```

After adding **"base:**&#x38;453&#x32;**"**, your **"blockchain"** object in the configuration file should look like the one below:

```json
...
    "blockchain": {
      "defaultImplementation": "otp:20430",
      "implementation": {
        "otp:20430": {
          "enabled": true,
          "config": {
            "sharesTokenSymbol": "shares_token_symbol",
            "sharesTokenName": "shares_token_name",
            "operatorFee": 5,
            "operationalWallets": [
              {
                "evmAddress": "0x0bf...",
                "privateKey": "0x1e3..."
              }
            ],
            "evmManagementWalletPublicKey": "0xd09..."
          }
        },
        "gnosis:10200": {
          "enabled": true,
          "config": {
            "sharesTokenSymbol": "shares_token_symbol",
            "sharesTokenName": "shares_token_name",
            "operatorFee": 5,
            "rpcEndpoints": [
              "https://archive-rpc.chiado.gnosischain.com/"
            ],
            "operationalWallets": [
              {
                "evmAddress": "0x0bf...",
                "privateKey": "0x1e3..."
              }
            ],
            "evmManagementWalletPublicKey": "0xd09..."
           }
         },
         "base:84532": {
           "enabled": true,
           "config": {
           "sharesTokenSymbol": "shares_token_symbol",
           "sharesTokenName": "shares_token_name",
           "operatorFee": <value_between_0_and_100>,
           "rpcEndpoints": [
              "<Your Base Sepolia RPC endpoint>"
           ],
           "operationalWallets": [
            {
              "evmAddress": "0x0bf...",
              "privateKey": "0x1e3..."
            }
          ],
          "evmManagementWalletPublicKey": "0xd09..."
         }
       }
      }
    },
...
```

## 4. Restart your node

You can proceed and restart your node to confirm that it will start communicating with Base Sepolia.

{% hint style="warning" %}
Once again, make sure that your operational wallet has some Base Sepolia ETH in order for your OriginTrail DKG node to be able to create the profile on the new network.
{% endhint %}

```
otnode-restart && otnode-logs
```

If you added everything successfully, your node will show the log that says “**blockchain module initialized with implementation: base:84532**”.

If you have come this far and your node logs are not showing any errors, you're node is successfully set up!&#x20;

## Node Stake and ask setup:

{% hint style="info" %}
If you are running a [Gateway](https://docs.origintrail.io/decentralized-knowledge-graph/node-setup-instructions/running-a-gateway-node) node, setting up **stake** and **ask** is not required.
{% endhint %}

Please refer to "[Running a full node](https://docs.origintrail.io/decentralized-knowledge-graph/node-setup-instructions/running-a-full-node)" part of our documentation for more details regarding setting up stake and ask parameters.
