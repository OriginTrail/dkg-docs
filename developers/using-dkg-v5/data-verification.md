# Data verification

### Verification and signature checks

When importing a dataset, the graph representation of the dataset is hashed to generate a unique identifier for that dataset, called the `dataset_id`.

The entire dataset (graph data together with dataset metadata) is used to generate a [Merkle tree](https://en.wikipedia.org/wiki/Merkle_tree) of the dataset, and the root hash of the Merkle tree is considered to be the dataset **root hash**. This process ensures data integrity because changing any part of the dataset would cause the dataset **root hash** to change.

When a dataset is replicated on the network, the integrity of the dataset (including any contained graph object) can be verified by fetching the Merkle tree root hash from the blockchain (published during the replication procedure).

The fingerprint API route returns the Merkle tree root hash from the blockchain of the dataset with the given `dataset_id`. The fingerprint API details are explained on the following link

[https://app.swaggerhub.com/apis-docs/otteam/ot-node-api/v2.0#/info/get_fingerprint\_\_id](https://app.swaggerhub.com/apis-docs/otteam/ot-node-api/v2.0#/info/get_fingerprint\_\_id\_)
