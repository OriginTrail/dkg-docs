---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Interact with DKG paranets

{% hint style="danger" %}
**Paranets are not currently supported in the DKG V8. Expect the support to be back latest by the end of February.**
{% endhint %}

The DKG Python SDK provides functionality for interacting with paranets on the OriginTrail Decentralized Knowledge Graph (DKG). This section of the SDK allows developers to create, manage, and utilize paranets effectively.

## Setup and installation

To interact with paranets, you need to connect to a running OriginTrail node (either local or remote) and ensure you have the dkg.py SDK installed and properly configured. Follow the general setup instructions for [installing dkg.py](./) and read more about paranets [in the following section](../../../dkg-v6-previous-version/autonomous-ai-paranets/).

### Creating a paranet

Before creating a paranet, you must first create a Knowledge Asset (KA) on the DKG that will represent the paranet. To create a Knowledge Asset on the DKG, refer to [the following page](./).

Once the Knowledge Asset is created, it will have a unique identifier known as a Universal Asset Locator (UAL). You will use this UAL to create a paranet. The paranet creation process essentially links the paranet to the Knowledge Asset, establishing it on the blockchain. This on-chain representation allows for decentralized management and interaction with the paranet.

Here is an example of how to create a new paranet using the `create` function from the paranet module. This function requires the UAL of the previously created Knowledge Asset, along with other details such as the paranet's name and description:

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
dkg.paranet.create(
    ual=paranet_ual,
    name="TestParanet",
    description="TestParanetDescription",
    paranet_nodes_access_policy=ParanetNodesAccessPolicy.CURATED,
    paranet_miners_access_policy=ParanetMinersAccessPolicy.CURATED
)
```

In this example:

* `ual` is the unique identifier of the Knowledge Asset created on the DKG.
* `name` is the name you want to give to your paranet. It should be descriptive enough to indicate the paranet's purpose or focus.
* `description` provides additional context about the paranet, explaining its purpose and the types of Knowledge Assets or services it will involve.
* `paranet_nodes_access_policy` defines a paranet's policy towards including nodes. If OPEN, any node can be a part of the paranet. If CURATED, only the paranet owner can approve nodes to be a part of the paranet.
* `paranet_miners_access_policy` defines a paranet's policy towards including knowledge miners. If OPEN, anyone can publish to a paranet. If CURATED, only the paranet owner can approve knowledge miners who can publish to the paranet.

After the paranet is successfully created, the paranet UAL can be used to interact with the specific paranet. This includes deploying services within the paranet, managing incentives, and claiming rewards associated with the paranet's operations.

### Adding/removing nodes to/from a paranet

This functionality is only available to the paranet operator if they created a paranet with `ParanetNodesAccessPolicy.CURATED`.&#x20;

By default, a node can participate in any paranet. However, with this change, if a node wants to participate in a paranet with the curated nodes access policy, it has to either be added to a paranet by a paranet operator or it has to request access.&#x20;

The paranet operator can add nodes to a paranet or remove them from a paranet by passing a `paranet_ual` and nodes `identity_ids`.

```python
paranet_ual  = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
node1_identity_id = dkg.node.get_identity_id(NODE1_PUBLIC_KEY)
node2_identity_id = dkg.node.get_identity_id(NODE2_PUBLIC_KEY)
node3_identity_id = dkg.node.get_identity_id(NODE3_PUBLIC_KEY)

identity_ids = [node1_identity_id, node2_identity_id, node3_identity_id]
dkg.paranet.add_curated_nodes(paranet_ual, identity_ids)

identity_ids = [node2_identity_id, node3_identity_id]
dkg.paranet.remove_curated_nodes(paranet_ual, identity_ids)
```

### Request curated node access to a paranet

A node can request access to be added to a paranet. A paranet operator can then either reject or approve access to the node based on its `identity_id`.&#x20;

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
identity_id = dkg.node.get_identity_id(NODE_PUBLIC_KEY)

# Node requests access to a curated paranet - Rejected
requesting_node.paranet.request_curated_node_access(paranet_ual)
dkg.paranet.reject_curated_node(paranet_ual, identity_id)

# Node requests access to a curated paranet - Approved
requestingNode.paranet.request_curated_node_access(paranet_ual)
dkg.paranet.approve_curated_node(paranet_ual, identity_id)
```

### Adding/removing knowledge miners to/from a paranet

This functionality is only available to the paranet operator if they created a paranet with `ParanetMinersAccessPolicy.CURATED`.&#x20;

By default a knowledge miner can publish to any paranet. However, with this change, if a knowledge miner wants to publish to a paranet with the curated miner access policy it has to either be added to a paranet by a paranet operator or it has to request access.&#x20;

The paranet operator can add knowledge miners to a paranet or remove them from a paranet by passing a `paranet_ual` and `miner_addresses`.

<pre class="language-python"><code class="lang-python">paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
<strong>miner_address1 = '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266'
</strong>miner_address2 = '0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC'
miner_address3 = '0x90F79bf6EB2c4f870365E785982E1f101E93b906'
<strong>
</strong><strong>miner_addresses = [miner_address1, miner_address2, miner_address3]
</strong>dkg.paranet.add_curated_miners(paranetUAL, miner_addresses)

miner_addresses = [miner_address2, miner_address3]
dkg.paranet.remove_curated_miners(paranetUAL, miner_addresses)
</code></pre>

#### Request curated knowledge miner access to a paranet

A knowledge miner can request access to be added to a paranet. A paranet operator can then either reject or approve access to the knowledge miner based on its `miner_address`.&#x20;

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
miner_address = '0xe5beaB7853A22f054Ef287EA62aCe7A32528b3eE'

requesting_kminer.paranet.request_curated_miner_access(paranet_ual)
dkg.paranet.reject_curated_miner(paranet_ual, miner_address)

requesting_kminer.paranet.request_curated_miner_access(paranet_ual)
dkg.paranet.approve_curated_miner(paranet_ual, miner_address)
```

### Adding services to a paranet

Enhance the capabilities of your paranet by integrating new services. The `add_services` function allows you to add both on-chain and off-chain services to your paranet. These services can range from AI agents and data oracles to decentralized knowledge interfaces and more.

Before adding services, you first need to create them using the `create_service` function. Services added to a paranet can either have on-chain addresses, representing smart contracts or other on-chain entities, or they can be off-chain services, which do not have associated blockchain addresses.

Each service can be identified by all paranet users via its registry Knowledge Asset and can include multiple on-chain accounts under its control. This enables services to participate in economic activities within the DKG.

```python
paranet_service_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/2'
dkg.paranet.create_service(
    ual=paranet_service_ual,
    name="TestParanetService",
    description="TestParanetServiceDescription",
    addresses=["0x03C094044301E082468876634F0b209E11d98452"]
)

dkg.paranet.add_services(ual=paranet_ual, services_uals=[paranet_service_ual])
```

In this example:

* `ual` specifies the UAL of the Paranet Service Knowledge Asset
* `name` specifies the name of the service.
* `description` provides a brief description of what the service does.
* `addresses` lists blockchain addresses associated with the service. For off-chain services, this field can be left empty.
* `services_uals` is an array of Universal Asset Locators for the services you want to add to your paranet.

By integrating and managing services, paranet operators can expand the capabilities of their paranet, providing a robust infrastructure for decentralized applications and AI-driven services.

## Knowledge mining for open paranets

Paranets allow users to leverage collective intelligence by contributing their Knowledge Assets, enhancing the overall utility and value of the network. There are two primary ways to add a Knowledge Asset to a paranet:

1. **Directly mining Knowledge Assets to a paranet**
2. **Submitting existing Knowledge Assets to a paranet**

To directly mine Knowledge Assets and add them to a paranet, use the `dkg.asset.create` function and specify the `paranet_ual` as a parameter. Here’s an example:

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
ka_data = {
    "public": {
        "@context": ["http://schema.org"],
        "@id": "uuid:3",
    }
}

create_submit_ka_result = dkg.asset.create(
    ka_data,
    1,
    100000000000000000000,
    paranet_ual=paranet_ual,
)
```

In this example, the Knowledge Asset is created and directly added to the specified paranet.

If you have existing Knowledge Assets, you can submit them to a paranet using the `dkg.asset.submit_to_paranet` function. Here’s an example:

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
ka_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/55'

submit_ka_result = dkg.asset.submit_to_paranet(ual=ka_ual, paranet_ual=paranet_ual)
```

Adding Knowledge Assets to paranets can be done directly during the creation process or by submitting existing assets. This flexibility allows for robust management and contribution of knowledge, enhancing the collective intelligence and functionality of the paranet.

## Knowledge mining for curated paranets

In curated paranets, there is a single method for adding Knowledge Assets, which is through the `dkg.asset.local_store` function.

Unlike open paranets, where assets can be mined or submitted, curated paranets offer more controlled management of data, ensuring consistency and integrity across the network. This approach enables users to store both public and private data on their nodes, providing enhanced security and control.&#x20;

Additionally, other nodes in the curated paranet can synchronize data from your node, ensuring that all participating nodes have access to the most up-to-date information. This model prioritizes privacy, control, and efficient data sharing within a trusted network.

Here's an example of how to create a Knowledge Asset for a curated paranet:

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
ka_data = {
    "public": {
        "@context": ["http://schema.org"],
        "@id": "uuid:3",
    },
    "private": {
        "@context": ["http://schema.org"],
        "@graph": [
            {"@id": "uuid:user:1", "name": "Adam", "lastname": "Smith"},
            {"@id": "uuid:belgrade", "title": "Belgrade", "postCode": "11000"},
        ],
    },
}

local_store_result = dkg.asset.local_store(
    ka_data,
    1,
    100000000000000000000,
    paranet_ual=paranet_ual,
)
```

## Checking and claiming rewards

Participants in a paranet can earn rewards for their various roles and contributions, such as knowledge mining, voting on proposals, or operating the paranet. The dkg.py library provides functions to check if an address has a specific role within the paranet and to claim rewards associated with that role.

**Roles in a paranet:**

* **Knowledge miners:** Contribute to the paranet by mining Knowledge Assets.
* **Paranet operators:** Manage the paranet, including overseeing services and facilitating operations.
* **Proposal voters:** Participate in decision-making by voting on the Initial Paranet Offering (IPO).

Participants can verify their roles and claim rewards through the following steps and examples:

<pre class="language-python"><code class="lang-python">paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'

# Check if an address is a knowledge miner
is_knowledge_miner = dkg.paranet.is_knowledge_miner(ual=paranet_ual)

# Check if an address is a paranet operator
is_operator = dkg.paranet.is_operator(ual=paranet_ual)
<strong>
</strong><strong># Check if an address is a voter
</strong>is_voter = dkg.paranet.is_voter(ual=paranet_ual)

# Check claimable rewards
knowledge_miner_reward = dkg.paranet.calculate_claimable_miner_reward_amount(ual=paranet_ual)
operator_reward = dkg.paranet.calculate_claimable_operator_reward_amount(ual=paranet_ual)

print(f"Claimable Knowledge Miner Reward for the Current Wallet: {knowledge_miner_reward}")
print(f"Claimable Paranet Operator Reward for the Current Wallet: {operator_reward}")
if (is_voter):
    voter_rewards = dkg.paranet.calculate_claimable_voter_reward_amount(ual=paranet_ual)
    print(f"Claimable Proposal Voter Reward for the Current Wallet: {voter_rewards}")

# Claim miner rewards
dkg.paranet.claim_miner_reward(ual=paranet_ual)

# Claim operator rewards
dkg.paranet.claim_operator_reward(ual=paranet_ual)

# Claim operator rewards
dkg.paranet.claim_voter_reward(ual=paranet_ual)
</code></pre>

By following these steps, you can effectively check your role and claim the rewards you have earned for contributing to the paranet. This system ensures that all participants are fairly compensated for their efforts, promoting a robust and active community within the p.

## Updating claimable rewards

In some cases, you may have already mined a Knowledge Asset to a specific paranet but decided to update the Knowledge Asset. By doing so, you become eligible for additional NEURO rewards (in the case when additional TRAC is spent for the update).&#x20;

To ensure that your claimable rewards reflect your new contributions, you need to call the `update_claimable_rewards` function for the paranet after the update finalization. This function updates your claimable reward amounts based on your latest contributions.

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'

dkg.paranet.update_claimable_rewards(ual=paranet_ual)
```

This function only updates the claimable rewards based on your latest contributions. To actually claim the rewards, use the respective claiming functions, such as `claim_miner_reward`, `claim_voter_reward`, or `claim_operator_reward`.

## Performing SPARQL queries on a specific paranet

The DKG enables users to perform SPARQL queries on specific paranets. By specifying a paranet, users can target their queries to retrieve data related to that paranet. This can be particularly useful when working with domain-specific data or services within a paranet.

To query a specific paranet, ensure that the node you are querying has already enabled paranet syncing for the paranet you wish to query. Without this setup, the node may not have the relevant data required to process your queries.[ ](../../../dkg-v6-previous-version/node-setup-instructions/sync-a-dkg-paranet.md)

[Read here](../../../dkg-v6-previous-version/node-setup-instructions/sync-a-dkg-paranet.md) how to set up a node to sync a paranet.

To query a specific paranet, you should set the `graph_location` to the desired paranet UAL. This approach allows you to direct your queries to the paranet that holds the relevant data.

Here’s how you can perform a query on a specific paranet:

```python
paranet_ual = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1'
query_where_madrid = """
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?graphName
WHERE {{
        GRAPH ?graphName {{
                ?s schema:city <uuid:Madrid> .
        }}
}}
"""

query_result = dkg.graph.query(query=query_where_madrid, graph_location=paranet_ual)

print(query_result)
```

By querying specific paranets, you can leverage the powerful capabilities of the DKG to interact with domain-specific Knowledge Assets and services, ensuring that your queries are targeted and efficient. This makes it easier to work with complex data structures and gain insights from your paranet's Knowledge Assets.

### Federated SPARQL queries

Federated SPARQL queries allow users to execute queries across multiple knowledge graphs or paranets simultaneously. In the context of the DKG, a node might sync with multiple paranets. Federated queries allow you to query multiple paranets within a single SPARQL query, accessing data from each specified paranet and merging the results.

Imagine you have a DKG node that synchronizes with three different paranets. You want to perform a query that targets two of these paranets to retrieve data about users and cities. Federated SPARQL queries provide a convenient way to specify which paranets to include in your query.

If you need to query data across multiple specified paranets, you should use federated SPARQL queries. However, if you want to query all available paranets, you do not need to provide any specific arguments, as all paranets will be queried by default using the default triple store repository.

To execute a federated SPARQL query, you can use the `SERVICE` keyword to specify the paranet UALs you want to query. This keyword allows you to include data from different sources in your query.

Here’s an example of a federated query targeting two out of three paranets:

```python
federated_query = """
PREFIX schema: <http://schema.org/>
SELECT DISTINCT ?s ?city1 ?user1 ?s2 ?city2 ?user2 ?company1
WHERE {{
  ?s schema:city ?city1 .
  ?s schema:company ?company1 .
  ?s schema:user ?user1;

  SERVICE <{ual}> {{
    ?s2 schema:city <uuid:Belgrade> .
    ?s2 schema:city ?city2 .
    ?s2 schema:user ?user2;
  }}

  filter(contains(str(?city2), "Belgrade"))
}}
"""

query_result = dkg.graph.query(
    query=federated_query.format(ual=paranet_ual3),
    graph_location=paranet_ual1,
)

print(query_result)
```

**Explanation:**

* **`SERVICE` keyword:** The `SERVICE` keyword is used to include data from Paranet 3 (`paranet_ual3`) in the query, while the primary paranet is set to Paranet 1 (`paranet_ual1`).
* **Query structure:** The query retrieves distinct subjects (`?s`), cities, users, and companies from Paranet 1, and performs a sub-query within Paranet 3 to get data where the city is `Belgrade`.
* **Filter clause:** The `filter` clause is used to ensure that the city data from Paranet 3 contains the string "Belgrade".

Federated SPARQL queries provide a powerful way to aggregate and analyze data across multiple paranets, this enables more complex data retrieval and cross-paranet data integration, making it easier to gather comprehensive insights from diverse data sources.
