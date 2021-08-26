# DKG persistance mechanisms

### How do DH nodes store the DKG?

All DH nodes participating in the ODN store the DKG data in two ways:

* by taking responsibility for storing a published data graph through the process of replication, after the process of negotiation and selection by the smart contract randomness beacon called the "offer task". For the service of storing and providing datasets, DH nodes are compensated in TRAC tokens locked at publishing 
* by opportunistically storing datasets for which there is a relatively high likelihood of becoming compensated in the future \(by replacing a designated DH node\). As DH nodes act in the interest of maximizing their service utilization, as long as there is enough free space on their disk, DH nodes will opportunistically store non-designated datasets in their graph databases

### Data pruning

Having the above two modes of storing in mind, all DH nodes can perform data pruning \(dataset removal\) once every 24h in the following situations:

* when a dataset expires, according to the data holding dataset longevity parameter \(meaning there is no longer any designated compensation available\)
* when the disk space reaches a set threshold, after which the node will prune "low estimated value" datasets. Low estimated value datasets are data graphs for which a node is not a designated DH node and are closest to expiry date \(so potential compensation achievable by designation is lowest\)

These features have been introduced in v5 and are editable in the node configuration file. Below is an example of config parameters which enable pruning, including pruning of "Low estimated value datasets", which will activate at 50% of hard disk usage. 

```javascript
"dataset_pruning": {
  "enabled": true,
  "imported_pruning_delay_in_minutes": 1440,
  "replicated_pruning_delay_in_minutes": 1440,
  "low_estimated_value_datasets": {
    "enabled": true,
    "minimum_free_space_percentage": 50
  }
}
```

You will know that pruning command has been started when you see this log:

`trace - Dataset pruning command started. This command will work in background and will try to remove expired and low estimated value datasets.`

{% hint style="info" %}
This feature has been tested on ot-node inside docker container using default Graph database implementation. If you are running the "dockerless" node or you changed default Graph database location inside docker container, make sure that correct path to database engine folder containing all data is set in configuration under database -&gt; engine\_folder\_path.
{% endhint %}

{% hint style="info" %}
Important: For low estimated value dataset pruning to kick in, make sure that your default backup folder doesn't contain any node data backups. This check is performed in order to provide the most precise free hard drive space estimation.

Additionally, the pruning process will not start if the graph database size hasn't reached a threshold of 20% of disk utilisation in order not to perform unnecessary operations and burden the node.
{% endhint %}

{% hint style="info" %}
Turning on both pruning and low estimated value dataset pruning will always try to keep your node hard drive usage at the set minimum free space percentage. However if a node cannot prune any more data \(such as for datasets your DH node is designated to hold\), pruning will not be effective - in these situations an increase in available hard drive space is required.
{% endhint %}

### Have ideas on improving this page? 

Create an issue or pull request [at this repo](https://github.com/OriginTrail/dkg-docs).

