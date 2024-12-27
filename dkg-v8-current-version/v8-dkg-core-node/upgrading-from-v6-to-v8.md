# Upgrading from V6 to V8

{% hint style="info" %}
This section is only for the node runners which are already running their nodes on V6 and need to upgrade to V8.
{% endhint %}

A few manual steps must be performed to successfully update your V6 node to a V8 Core Node. The following steps should be performed after the official V8 release has been deployed on the DKG mainnet.

#### Preparing your node for V8 update:

Have your node automatically download the latest version, and verify that the auto-updater is enabled on the ot-node service. To enable the auto-updater, follow the instructions on the following [page](https://docs.origintrail.io/dkg-v6-current-version/node-setup-instructions/useful-resources/manually-configuring-your-node).&#x20;

Once the auto-updater is enabled in the .origintrail\_noderc file, restart the node to apply the configuration changes. When the update is released, your node will automatically pull the latest version (V8), install node modules, and restart.

#### Configuring the new V8 blockchainEvents module:

The new V8 ot-node engine introduces a <mark style="color:green;">blockchainEvents</mark> module, which you will need to configure on your node by adjusting the settings in the configuration file. The provided template includes configurations for three blockchains: <mark style="color:green;">otp:2043, gnosis:100</mark>, and <mark style="color:green;">base:8453</mark>. Depending on which blockchains your node is connected to, you should modify the template accordingly.

* **Adjust the&#x20;**<mark style="color:green;">**blockchains**</mark>**&#x20;array**: Only include the blockchain IDs relevant to your node. For example, if your node is not connected to the <mark style="color:green;">gnosis:100</mark> blockchain, remove it from the array.
* **Update the&#x20;**<mark style="color:green;">**rpcEndpoints**</mark>**&#x20;section**: Provide the appropriate RPC endpoints for each blockchain your node is connected to. Remove any endpoints that do not apply to your node’s blockchain configuration.

**Example configuration with blockchainEvents added:**

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
                            "base:84532": ["https://<your_rpc>"],
                            "gnosis:10200": ["https://<your_rpc>"]
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

### Running data migration:

After the node successfully starts with version 8, you **should manually run the data migration script** run-data-migration.sh, located in the "**`/ot-node/current/v8-data-migration/`**" directory, by executing:

```
bash run-data-migration.sh
```

The data migration script migrates all triples from their V6 to V8 triple store repositories. Make sure you have configured RPCs properly for all the blockchains your node is connected to. Depending on how much data your node is hosting, this migration might last several hours to several days.&#x20;

{% hint style="info" %}
This migration will not influence your node reward performance. Your node will remain fully operational, and all pre-V8 Knowledge Assets will remain queryable via the GET protocol method.
{% endhint %}

If the data migration is interrupted for any reason (e.g., server restart), simply re-run the script. It will automatically resume from the point where it was interrupted.

### Tracking data migration progress:

To track the data migration progress, check the migration script log file located at                               **"`/ot-node/current/v8-data-migration/logs/migration.log`**", for example by using the command "**tail -f migration.log**".

{% hint style="warning" %}
We strongly encourage all node runners to update as soon as the release is out to ensure continued compatibility and to take advantage of the latest features and improvements.
{% endhint %}
