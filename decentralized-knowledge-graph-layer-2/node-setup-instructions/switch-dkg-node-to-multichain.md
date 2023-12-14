# Switch DKG node to multichain

Welcome to the guide on expanding the capabilities of your existing OriginTrail DKG node! By following these instructions, you'll seamlessly transition from a single-chain setup to a powerful multichain configuration, connecting your node not only to the OriginTrail Parachain but also to the Gnosis blockchain.

Before diving into the integration process, ensure you have your OriginTrail Parachain DKG node fully operational and connected.

## Mainnet DKG node

Coming soon!

## Testnet DKG node

Since the 6.1.0 release, your OriginTrail DKG Testnet node now supports Gnosis Chiado. To enable your DKG Testnet node's connection to Gnosis Chiado, follow the next set of instructions.

### 1. Obtain Gnosis Chiado Archival RPC Endpoint

Refer to the [official Gnosis documentation](https://docs.gnosischain.com/tools/rpc/) and select an RPC provider to acquire the Archival RPC Endpoint.&#x20;

Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.

{% hint style="warning" %}
Selecting an archival endpoint is a crucial requirement for the optimal functionality of your DKG node.
{% endhint %}

### 2. Acquire test tokens

Go to [fund-your-dkg-testnet-node.md](fund-your-dkg-testnet-node.md "mention") to get test TRAC and xDAI tokens.

### 3. Update DKG node configuration

Open .origintrail\_noderc file of your DKG testnet node. Within the config, locate the 'blockchain' object, and add the following object to the 'implementation' array, specifying your RPC endpoint and wallets.

```json
"gnosis:100": {
  "enabled": true,
  "config": {,
    "rpcEndpoints": [
      "https://archive-rpc.chiado.gnosischain.com/"
    ],
    "gasPriceOracleLink": "https://blockscout.chiadochain.net/api/v1/gas-price-oracle",
    "evmOperationalWalletPublicKey": "0x0bf...",
    "evmOperationalWalletPrivateKey": "0x1e3...",
    "evmManagementWalletPublicKey": "0xd09..."
   }
 }
```

### 4. Restart your node

You can proceed and restart your node to confirm that it will start communicating with Gnosis Chiado.

```
otnode-restart && otnode-logs
```

If you added everything successfully, your node will show the “**blockchain module initialized with implementation: gnosis:10200**” log.

### 5. Set up stake and ask via npm scripts

Use npm scripts to setup both node stake and service ask directly from the server where your node was installed, **however this process requires you to provide your node admin wallet key on the script.**&#x20;

{% hint style="warning" %}
Please make sure that you replace the public and private key values accordingly as well as the stake value before execution. This scripts should be run from the ot-node directory.
{% endhint %}

**Set TRAC stake for your node:**

Example command:&#x20;

```
npm run set-stake -- --rpcEndpoint=https://rpc.chiado.gnosischain.comm/ --stake=50000 --operationalWalletPrivateKey=0x92962c43dd7cb66d9d37c174388558eb57a722d33f65f91398a5a2714c36fdc4 --managementWalletPrivateKey=0x6f9a4cd2714f8a56950ad96742d2e6efcd0319a259a47cf56775c6d63e731e67 --hubContractAddress=0xC06210312C9217A0EdF67453618F5eB96668679A 
```

**Set your ask for your node:**&#x20;

Example command:&#x20;

```
npm run set-stake -- --rpcEndpoint=https://rpc.chiado.gnosischain.com/ --stake=50000 --operationalWalletPrivateKey=0x92962c43dd7cb66d9d37c174388558eb57a722d33f65f91398a5a2714c36fdc4 --managementWalletPrivateKey=0x6f9a4cd2714f8a56950ad96742d2e6efcd0319a259a47cf56775c6d63e731e67 --hubContractAddress=0xC06210312C9217A0EdF67453618F5eB96668679A 
```

If you have come this far and your node logs are not showing any errors, you're node is successfully set up!&#x20;



