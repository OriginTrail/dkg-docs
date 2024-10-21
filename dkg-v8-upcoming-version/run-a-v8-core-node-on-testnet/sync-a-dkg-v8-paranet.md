# Sync a DKG V8 Paranet

To interact with specific DKG paranets Knowledge Graphs using your OriginTrail node, you need to configure your node to synchronize paranet's knowledge assets. This setup can be achieved by modifying your node's configuration file to include paranet UAL.&#x20;

To enable your node to sync with a paranet, you will need to add `assetSync` object  to your node’s `.origintrail_noderc` file. Below is an example of how to configure this (make sure to replace the UAL in the example below):

```json
"assetSync": {
    "syncParanets": ["did:dkg:base:84532/0x8aafc28174bb6c3bdc7be92f18c2f134e876c05e/1"]
}
```



Once `.origintrail_noderc` is updated, it should look something like this:

<pre class="language-java"><code class="lang-java">...
    "auth": {
        "ipWhitelist": [
            "::1",
            "127.0.0.1"
        ]
    },
<strong>    "assetSync": {
</strong>        "syncParanets": ["did:dkg:base:84532/0x8aafc28.../1"]
    }    
}
</code></pre>

After you have updated the `.origintrail_noderc` file, save your changes and restart your OriginTrail node. This ensures that the new settings take effect and your node starts syncing data from the specified paranet.

Your node will start syncing when you see following log:

```
Paranet sync: Starting paranet sync for paranet: did:dkg:hardhat2:31337/0x8aafc28174bb6c3bdc7be92f18c2f134e876c05e/1
```

The paranet is fully synced when you see following log:

```
Paranet sync: No new assets to sync for paranet: did:dkg:hardhat2:31337/0x8aafc28174bb6c3bdc7be92f18c2f134e876c05e/1 
```

