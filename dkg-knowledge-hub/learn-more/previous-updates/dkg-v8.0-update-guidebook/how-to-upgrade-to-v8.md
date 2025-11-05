---
description: >-
  Below you will find the guidelines for builders, TRAC delegators, and node
  runners for the V8.0 release and activities expected in the Upgrade Period.
---

# How to upgrade to V8?

<figure><img src="../../../../.gitbook/assets/DKG V8 update guide book - gitbook cover1 (1).png" alt=""><figcaption></figcaption></figure>

## For builders

**Edge Nodes: If you’re running edge-node services**, you should make sure the DKG Node Engine (ot-node service) is properly updated, as V6 Edge Nodes will not be compatible with the new features. You should also ensure that you update to the newly released V8.0 DKG clients (dkg.js and dkg.py) in your projects - a sufficient level of backward compatibility is enabled for the V6 clients, however, keep in mind that the new features of V8 are somewhat different ([check the previous sections on updated Knowledge Assets](protocol-updates.md)).

For the ot-node service update, please follow the instructions in the [#for-core-node-runners](how-to-upgrade-to-v8.md#for-core-node-runners "mention") section below.

Having that said, individual pre-V8 Knowledge Assets will remain queryable via the GET protocol method.&#x20;

**Paranets**: If you are running a paranet on the DKG mainnet, you should be aware that it will be resynced if you have enabled paranet sync in the node config. The node will perform a re-sync by itself, and all the data will be available when sync is completed.

**Smart contracts**: If you are **querying DKG contracts** on any of the deployed chains, you can expect the productive version of V8 smart contracts to be [available on the official repo](https://github.com/OriginTrail/dkg-evm-module/) after the release.

For any questions, please reach out to the developer community in Discord.

## For TRAC delegators

If you have previously delegated your TRAC on any of the DKG-supported blockchains to Core Nodes, your stake will remain active and will continue to contribute to the network. In order to manage your stake (delegating, withdrawing, and redelegating), **you will have to perform a migration to the new system**. This migration will be facilitated by the new Staking Dashboard, which will enable executing migration transactions directly from your staking wallet. These transactions will burn your current share tokens, and account for your stake in the new V8 smart contracts directly.

There is no rush to migrate - your rewards will continue to accrue even if you don’t migrate. The only thing unavailable before migration is managing your stake.&#x20;

Learn more about the new Delegated staking [here](../../../../contribute-to-the-dkg/delegated-staking/).

## For Core Node runners

### Upgrading from V6 to V8

{% hint style="info" %}
This section is only for the node runners who are already running their nodes on V6 and need to upgrade to V8.
{% endhint %}

A few manual steps must be performed to successfully update your V6 node to a V8 Core Node. The following steps should be performed after the official V8 release has been deployed on the DKG mainnet.

### Preparing your node for V8 update

Have your node automatically download the latest version, and verify that the auto-updater is enabled on the ot-node service. To enable the auto-updater, follow the instructions on the following [page](https://docs.origintrail.io/dkg-v6-current-version/node-setup-instructions/useful-resources/manually-configuring-your-node).&#x20;

Once the auto-updater is enabled in the .origintrail\_noderc file, restart the node to apply the configuration changes. When the update is released, your node will automatically pull the latest version (V8), install node modules, and restart.

### Configuring the new V8 blockchainEvents module

The new V8 ot-node engine introduces a <mark style="color:green;">blockchainEvents</mark> module, which you will need to configure on your node by adjusting the settings in the configuration file. The provided template includes configurations for three blockchains: <mark style="color:green;">otp:2043, gnosis:100</mark>, and <mark style="color:green;">base:8453</mark>. Depending on which blockchains your node is connected to, you should modify the template accordingly.

* **Adjust the&#x20;**<mark style="color:green;">**blockchains**</mark>**&#x20;array**: Only include the blockchain IDs relevant to your node. For example, if your node is not connected to the <mark style="color:green;">gnosis:100</mark> blockchain, remove it from the array.
* **Update the&#x20;**<mark style="color:green;">**rpcEndpoints**</mark>**&#x20;section**: Provide the appropriate RPC endpoints for each blockchain your node is connected to. Remove any endpoints that do not apply to your node’s blockchain configuration.

**Example configuration with blockchainEvents added**

```
{
    "modules": {
        "autoUpdater": {
            <auto_updater_module_configuration>
        },
        "blockchainEvents": {
            "enabled": true,
            "implementation": {
                "ot-ethers": {
                    "enabled": true,
                    "package": "./blockchain-events/implementation/ot-ethers/ot-ethers.js",
                    "config": {
                        "blockchains": [
                            "otp:2043",
                            "gnosis:100",
                            "base:8453"
                        ],
                        "rpcEndpoints": {
                            "base:8453": ["https://<your_rpc>"],
                            "gnosis:100": ["https://<your_rpc>"]
                        }
                    }
                }
            }
        },
        "blockchain": {
            <blockchain_module_configuration>
        },
        ...
```

### Running data migration

After the node successfully starts with version 8, you **should manually run the data migration script** run-data-migration.sh. Before that, make sure you update the **MAIN\_DIR** variables in these two files if your main directory is **NOT** "root":

1. run-data-migration.sh
2. constants.js

Both files are located in the "**`/ot-node/current/v8-data-migration/`**" directory.\
\
After that, execute the data migration script in the same directory by running:

```bash
bash run-data-migration.sh
```

The data migration script migrates all triples from their V6 to V8 triple store repositories. Make sure you have configured RPCs properly for all the blockchains your node is connected to. Depending on how much data your node is hosting, this migration might last several hours to several days.&#x20;

{% hint style="info" %}
This migration will not influence your node reward performance. Your node will remain fully operational, and all pre-V8 Knowledge Assets will remain queryable via the GET protocol method.
{% endhint %}

If the data migration is interrupted for any reason (e.g., server restart), simply re-run the script (make sure the script is not already running, check the [#restarting-terminating-the-data-migration](how-to-upgrade-to-v8.md#restarting-terminating-the-data-migration "mention") section for more information). It will automatically resume from the point where it was interrupted.

### Tracking data migration progress

To track the data migration progress, check the nohup.out file located at "**`/ot-node/data/nohup.out`**", for example, by using the command:

```bash
tail -f nohup.out
```

If you want to analyze the logs, we suggest taking a look at the migration log file located at "/**`ot-node/data/data-migration/logs/migration.log`**".

### Restarting/terminating the data migration

If you want to restart the script, make sure you terminate the old process first. You can find out whether the old process is still running by entering this into the terminal:

```bash
ps aux | grep v8-data-migration
```

If the old data migration process is still running, you should see an output like this:

```bash
root     1046979 30.9  3.8 22159880 152996 pts/0 Sl   11:12   0:15 node v8-data-migration.js
root     1047113  0.0  0.0   8164   712 pts/0    S+   11:13   0:00 grep --color=auto v8-data-migration
```

Run "**`kill <PID>`**" command on the node process and repeat the steps under the[#running-data-migration](how-to-upgrade-to-v8.md#running-data-migration "mention") section.

{% hint style="warning" %}
We strongly encourage all node runners to update as soon as the release is out to ensure continued compatibility and to take advantage of the latest features and improvements.
{% endhint %}
