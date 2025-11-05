---
cover: ../../../../.gitbook/assets/MicrosoftTeams-image (1).png
coverY: 0
---

# Connect to Gnosis

Since 6.2.0 release, OriginTrail DKG nodes support Gnosis blockchain. Learn more about how to use your node with Gnosis below.

## Mainnet node instructions (Gnosis chain)

Since the 6.2.0 release, your OriginTrail DKG node supports the Gnosis blockchain. In order to connect your node to Gnosis, please refer to the instructions below.

### 1. Obtain Gnosis archival RPC Endpoint

Refer to the [official Gnosis documentation](https://docs.gnosischain.com/tools/rpc/) and select an RPC provider to acquire the Archival RPC Endpoint.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.
{% endhint %}

### 2. Acquire tokens

In order for your node to be able to create the profile on the Gnosis blockchain, it will require some xDai tokens on the operational wallet (at least one of the wallets in **operationalWallets**). Make sure that you acquire them before proceeding to update the configuration file; otherwise, your node will fail to connect to the Gnosis network.

If you are planning on running an OriginTrail [Full node](../../../../graveyard/everything/node-setup-instructions/running-a-full-node.md), make sure that you also acquire TRAC tokens on Gnosis network and have them ready on the management wallet (**evmManagementWalletPublicKey**). TRAC is required for the process of setting up stake on your node once it's successfully connected to Gnosis and created its profile.

{% hint style="info" %}
As described in the "[**Acquiring tokens**](https://docs.origintrail.io/decentralized-knowledge-graph/node-setup-instructions/installation-prerequisites/acquiring-tokens)" instructions page, bridging TRAC tokens from Ethereum to Gnosis network is done via [**OmniBridge**](https://omnibridge.gnosischain.com/bridge) or any other bridging platform.&#x20;
{% endhint %}

{% hint style="warning" %}
DKG [Gateway](https://docs.origintrail.io/decentralized-knowledge-graph/node-setup-instructions/running-a-gateway-node) nodes do not require TRAC stake.
{% endhint %}

### 3. Update DKG node configuration

Open **.origintrail\_noderc** file of your DKG node located inside the **ot-node** directory. Inside the configuration file, locate the **"blockchain"** object, and add the following object to the **"implementation"** array, specifying your RPC endpoint and wallets. As `operationalWallets` is an array, you can define multiple operational wallets, which is recommended.

```json
"gnosis:100": {
  "enabled": true,
  "config": {,
    "operatorFee": 5,
    "rpcEndpoints": [
      "https://<desired_rpc_endpoint>"
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

After adding **"gnosis:100"**, make sure to add the initial `operatorFee` (range from 0% to 100%).

{% hint style="warning" %}
Initial operator fee (**operatorFee**) can only be set on the profile creation, so make sure not to forget about it. In order to change it later through Houston, you will need to wait for a delay of 28 days!
{% endhint %}

After these additions, your **"blockchain"** object in the configuration file should look similar to the example below:

```json
...
    "blockchain": {
      "defaultImplementation": "otp:2043",
      "implementation": {
        "otp:2043": {
          "enabled": true,
          "config": {
            "sharesTokenSymbol": "shares_token_symbol",
            "sharesTokenName": "shares_token_name",
            "operatorFee": 5,
            "operationalWallets": [
               {
                "evmAddress": "0x...",
                "privateKey": "0x..."
               }
            ],
            "evmManagementWalletPublicKey": "0x..."
          }
        },
        "gnosis:100": {
          "enabled": true,
          "config": {
            "sharesTokenSymbol": "shares_token_symbol",
            "sharesTokenName": "shares_token_name",
            "operatorFee": 5,
            "rpcEndpoints": [
              "https://<desired_rpc.endpoint>"
            ],
            "operationalWallets": [
               {
                "evmAddress": "0x...",
                "privateKey": "0x..."
               }
            ],
            "evmManagementWalletPublicKey": "0x..."
          }
        }
      }
    },
...
```

### 4. Restart your node

You can proceed and restart your node to confirm that it will start communicating with Gnosis Chiado.

```
otnode-restart && otnode-logs
```

If you added everything successfully, your node will show the “**blockchain module initialized with implementation: gnosis:10200**” log.

## Testnet node instructions (Gnosis Chiado)

Since the 6.1.0 release, your OriginTrail DKG node can operate on Gnosis Chiado network. In order to connect your node to Gnosis, please refer to the instructions below.

### 1. Obtain Gnosis Chiado Archival RPC Endpoint

Refer to the [official Gnosis documentation](https://docs.gnosischain.com/tools/rpc/) and select an RPC provider to acquire the Archival RPC Endpoint.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.
{% endhint %}

### 2. Acquire TRAC and Chiado test tokens

Go to [test-token-faucet.md](../../../useful-resources/test-token-faucet.md "mention") to get test TRAC and xDAI tokens.

### 3. Update DKG node configuration

Open the **.origintrail\_noderc** configuration file of your DKG node located inside the **ot-node** directory. Within the config, locate the **"blockchain"** object, and add the following object to the **"implementation"** array, specifying your RPC endpoint and wallets. As `operationalWallets` is an array, you can define multiple operational wallets, which is recommended.

```json
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
 }
```

After adding **"gnosis:10200"**, your **"blockchain"** object in the configuration file should look like the one below:

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
         }
      }
    },
...
```

## 4. Restart your node

You can proceed and restart your node to confirm that it will start communicating with Gnosis Chiado.

{% hint style="warning" %}
Once again, make sure that your operational wallet has some Chiado in order for your OriginTrail DKG node to be able to create the profile on the new network.
{% endhint %}

```
otnode-restart && otnode-logs
```

If you added everything successfully, your node will show the log that says “**blockchain module initialized with implementation: gnosis:10200**”.



If you have come this far and your node logs are not showing any errors, you're node is successfully set up!&#x20;

## Node Stake and ask setup:

{% hint style="info" %}
If you are running a [Gateway](https://docs.origintrail.io/decentralized-knowledge-graph/node-setup-instructions/running-a-gateway-node) node, setting up **stake** and **ask** is not required.
{% endhint %}

Please refer to "[Running a full node](https://docs.origintrail.io/decentralized-knowledge-graph/node-setup-instructions/running-a-full-node)" part of our documentation for more details regarding setting up stake and ask parameters.

