# Sync a DKG Paranet

To interact with specific DKG paranets Knowledge Graphs using your OriginTrail node, you need to configure your node to synchronize paranet's knowledge assets. This setup can be achieved by modifying your node's configuration file to include paranet UAL.&#x20;

If you have not yet set up your node or need guidance on configuring a full or gateway node, please refer to the following links:

* [Setting up a full DKG node](running-a-full-node.md)
* [Setting up a gateway DKG node](running-a-gateway-node.md)

To enable your node to sync with a paranet, you will need to add `assetSync` object  to your node’s `.origintrail_noderc` file. Below is an example of how to configure this (make sure to replace the UAL in the example below):

```json
"assetSync": {
    "syncParanets": ["did:dkg:hardhat2:31337/0x8aafc28174bb6c3bdc7be92f18c2f134e876c05e/1"]
}
```

After you have updated the `.origintrail_noderc` file, save your changes and restart your OriginTrail node. This ensures that the new settings take effect and your node starts syncing data from the specified paranet.

Your node will start syncing when you see following log:

```
Paranet sync: Starting paranet sync for paranet: did:dkg:hardhat2:31337/0x8aafc28174bb6c3bdc7be92f18c2f134e876c05e/1
```

The paranet is fully synced when you see following log:

```
Paranet sync: KA count from contract and in DB is the same, nothing new to sync, for paranet: did:dkg:hardhat2:31337/0x8aafc28174bb6c3bdc7be92f18c2f134e876c05e/1 
```

Interacting with the paranet Knowledge graph through your node is explained on [building-with-dkg-paranets.md](../autonomous-ai-paranets/building-with-dkg-paranets.md "mention") page.

