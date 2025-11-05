# How DKG synchronization works

The **DKG Sync** feature enhances the **anti-fragility** of the OriginTrail Decentralized Knowledge Graph (DKG) by allowing Core Nodes to continuously and efficiently backfill any missing Knowledge Assets (KAs). This is especially useful for **gracefully handling temporary node downtime**, such as during server upgrades or brief periods of unavailability.

Rather than relying on constant uptime, DKG Sync enables nodes to recover and remain synchronized with the state of the public DKG shard(s) they participate in, ensuring robust participation in discovery, querying, and Random Sampling.

### Why was DKG sync introduced

As the DKG grows and evolves, Core Nodes may experience periods of downtime, restarts, or join the network for the first time. Rather than penalizing such situations, the sync system is designed to allow:

* Reliable and autonomous catch-up for missing data
* Smooth reintegration of previously unavailable nodes
* Full historical sync for newly joined nodes to get up to speed
* Consistently high levels of data replication across the network

This improves the system's overall anti-fragility, making it more adaptive and resilient as it scales, restarts, or undergoes late onboarding. Rather than penalizing such situations, the sync system is designed to allow:

* Reliable and autonomous catch-up for missing data
* Smooth reintegration of previously unavailable nodes
* Consistently high levels of data replication across the network

This makes the network more robust over time, allowing it to adapt and improve in response to dynamic changes in node availability.

### How it works

The sync feature operates as a **background service** and performs two key tasks:

#### 1. Sync new Knowledge Collections

* Compares the latest on-chain KC ID to the node’s own synced state
* Constructs and sends Batch GET requests for any new, missing KCs
* Stores verified KCs locally and tracks update progress
* Queues any missing results for retry

#### 2. Retry missed Knowledge Collections

* Periodically retries fetching failed KCs using intelligent retry logic
* Dynamically schedules based on retry count and last attempt timestamp
* Removes successfully synced KCs from retry queue



The DKG Sync feature introduces **Batch GET**, a new network operation optimized for retrieving multiple KCs efficiently. Rather than issuing redundant GET requests to multiple nodes, Batch GET enables smart coordination strategies that reduce bandwidth, balance load, and maximize responsiveness.

These mechanisms ensure that even a freshly joined or recently restarted node can synchronize efficiently without overwhelming the network.

### Sync Logic and resource considerations

| Requirement              | Behavior                                                        |
| ------------------------ | --------------------------------------------------------------- |
| **Fresh nodes**          | Can perform full historical sync on joining                     |
| **Operational priority** | Sync yields to publish/query tasks                              |
| **Peer interaction**     | Sync tracks peer GET volumes to avoid overload                  |
| **Resilience**           | Sync recovers cleanly from failures and continues automatically |

***

#### How to turn on DKG Sync

For DKG Sync to run, it needs to be enabled in the node configuration.&#x20;

In `.origintrail_noderc` file at top level add `assetSync` object to enable  and configure sync:

```
{
   "modules": {
       ...
   },
   "auth": {
       ...
   },
   "assetSync": {
       "syncDKG": {
           "enabled": true,
           // Number of KCs suggested to be 50 in beginning
           "syncBatchSize": <NUMBER-OF-KCs-IN-BATCH>
       },
       // You already have this if your node is syncing a paranet
       "syncParanets": []
   }
}
```

