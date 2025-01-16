---
cover: ../../../.gitbook/assets/dkg-js-banner.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
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

# Interact with DKG Paranets

{% hint style="danger" %}
**Paranets are not currently supported in V8. Expect the paranet support to be back latest by the end of February.**
{% endhint %}

The DKG JavaScript SDK provides functionality for interacting with Paranets on the OriginTrail Decentralized Knowledge Graph. This section of the SDK allows developers to create, manage, and utilize paranets effectively.

#### Setup and Installation

To interact with Paranets, you need to connect to a running OriginTrail node (either local or remote) and ensure you have the dkg.js SDK installed and properly configured. Follow the general setup instructions for [installing dkg.js](./) and read more about Paranets [in the following section](../../../dkg-v6-previous-version/autonomous-ai-paranets/).

#### Creating a Paranet

Before creating a Paranet, you must first create a Knowledge Asset (KA) on the Decentralized Knowledge Graph (DKG) that will represent the Paranet. To create a Knowledge Asset on the DKG refer to [the following page](./).

Once the Knowledge Asset is created, it will have a unique identifier known as a Universal Asset Locator (UAL). To create a Paranet, you will use this UAL. The Paranet creation process essentially links the Paranet to the Knowledge Asset, establishing it on the blockchain. This on-chain representation allows for decentralized management and interaction with the Paranet.

Here is an example of how to create a new Paranet using the `create` function from the Paranet module. This function requires the UAL of the previously created Knowledge Asset, along with other details such as the Paranet's name and description:

```javascript
const UAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
await dkg.paranet.create(UAL, {
        paranetName: 'AiParanet',
        paranetDescription: 'AI agents paranet for demonstration purposes.',
        paranetNodesAccessPolicy: PARANET_NODES_ACCESS_POLICY.CURATED,
        paranetMinersAccessPolicy: PARANET_MINERS_ACCESS_POLICY.CURATED,
});
```

In this example:

* `UAL` is the unique identifier of the Knowledge Asset created on the DKG.
* `paranetName` is the name you want to give to your Paranet. It should be descriptive enough to indicate the Paranet's purpose or focus.
* `paranetDescription` provides additional context about the Paranet, explaining its purpose and the types of knowledge assets or services it will involve.
* `paranetNodesAccessPolicy` defines a paranet's policy towards including nodes. If OPEN, any node can be a part of the paranet. If CURATED, only the paranet owner can approve nodes to be a part of the paranet.
* `paranetMinersAccessPolicy` defines a paranet's policy towards including knowledge miners. If OPEN, anyone can publish to a paranet. If CURATED, only the paranet owner can approve knowledge miners who can publish to the paranet.

After the Paranet is successfully created, the Paranet UAL can be used to interact with the specific Paranet. This includes deploying services within the Paranet, managing incentives, and claiming rewards associated with the Paranet's operations.

#### Adding/removing nodes to/from a Curated Paranet

This functionality is only available to the paranet operator if they created a paranet with `paranetNodesAccessPolicy.CURATED`. By default a node can participate in any paranet. However, with this change, if a node wants to participate in a paranet with the curated nodes access policy it has to either be added to a paranet by a paranet operator or it has to request access. The paranet operator can add nodes to a paranet or remove them from a paranet by passing a `paranetUAL` and nodes`identityIds`.

<pre class="language-javascript"><code class="lang-javascript">const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
const node1IdentityId = await dkg.node.getIdentityId(NODE1_PUBLIC_KEY);
const node2IdentityId = await dkg.node.getIdentityId(NODE2_PUBLIC_KEY);
const node3IdentityId = await dkg.node.getIdentityId(NODE3_PUBLIC_KEY);
<strong>
</strong><strong>// Adding nodes to a curated paranet
</strong><strong>const identityIdsToAdd = [node1IdentityId, node2IdentityId, node3IdentityId];
</strong>await dkg.paranet.addCuratedNodes(paranetUAL, identityIdsToAdd);

// Removing nodes from a curated paranet
const identityIdsToRemove = [node2IdentityId, node3IdentityId];
await dkg.paranet.removeCuratedNodes(paranetUAL, identityIdsToRemove);
</code></pre>

#### Request curated node access to a Curated Paranet

A node can request access to be added to a paranet. A paranet operator can then either reject or approve access to the node based on its `identityId`.&#x20;

<pre class="language-javascript"><code class="lang-javascript">const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
const identityId = await dkg.node.getIdentityId(REQUESTING_NODE_PUBLIC_KEY);

// Node requests access to a curated paranet - Access rejected
await requestingNode.paranet.requestCuratedNodeAccess(paranetUAL);
<strong>await dkg.paranet.rejectCuratedNode(paranetUAL, identityId);
</strong>
// Node requests access to a curated paranet - Access approved
await requestingNode.paranet.requestCuratedNodeAccess(paranetUAL); 
await dkg.paranet.approveCuratedNode(paranetUAL, identityId);
</code></pre>

#### Adding/removing knowledge miners to/from a Curated Paranet

This functionality is only available to the paranet operator if they created a paranet with `paranetMinersAccessPolicy.CURATED`. By default a knowledge miner can publish to any paranet. However, with this change, if a knowledge miner wants to publish to a paranet with the curated miner access policy it has to either be added to a paranet by a paranet operator or it has to request access. The paranet operator can add knowledge miners to a paranet or remove them from a paranet by passing a `paranetUAL` and `minerAddresses`.

<pre class="language-javascript"><code class="lang-javascript">const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
<strong>const minerAddress1 = '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266';
</strong>const minerAddress2 = '0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC';
const minerAddress3 = '0x90F79bf6EB2c4f870365E785982E1f101E93b906';
<strong>
</strong><strong>const minerAddressesToAdd = [minerAddress1, minerAddress2, minerAddress3];
</strong>await dkg.paranet.addCuratedMiners(paranetUAL, minerAddressesToAdd);

const minerAddressesToRemove = [minerAddress2, minerAddress3];
await dkg.paranet.removeCuratedMiners(paranetUAL, minerAddressesToRemove);
</code></pre>

#### Request Knowledge Miner access to a Curated Paranet

A knowledge miner can request access to be added to a paranet. A paranet operator can then either reject or approve access to the knowledge miner based on its `minerAddress`.&#x20;

<pre class="language-javascript"><code class="lang-javascript">const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
const requestingMinerAddress = '0x90F79bf6EB2c4f870365E785982E1f101E93b906';

// Knowlegde miner requests access - Access rejected
<strong>await requestingMiner.paranet.requestCuratedMinerAccess(paranetUAL);
</strong>await dkg.paranet.rejectCuratedMiner(paranetUAL, requestingMinerAddress);

// Knowlegde miner requests access - Access approved
await requestingMiner.paranet.requestCuratedMinerAccess(paranetUAL);
await dkg.paranet.approveCuratedMiner(paranetUAL, requestingMinerAddress);
</code></pre>

#### Adding Services to a Paranet

Enhance the capabilities of your Paranet by integrating new services. The `addServices` function allows you to add both on-chain and off-chain services to your Paranet. These services can range from AI agents and data oracles to decentralized knowledge interfaces and more.

Before adding services, you first need to create them using the `createService` function. Services added to a Paranet can either have on-chain addresses, representing smart contracts or other on-chain entities, or they can be off-chain services, which do not have associated blockchain addresses.

Each service can be identified by all Paranet users via its registry knowledge asset, and can include multiple on-chain accounts under its control. This enables services to participate in economic activities within the Decentralized Knowledge Graph (DKG).

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
const serviceUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/2';
await dkg.paranet.createService(paranetUAL, {
    paranetServiceName: 'MyAiService',
    paranetServiceDescription: 'Autonomous AI service for AI paranet',
    paranetServiceAddresses: ['0xb3155543738b997b7a1a5bc849005bc2afd35578', '0x2375e543738b997b7a125bc849005b62afd35571'],
});

const serviceUALs = [serviceUAL]; 
await dkg.paranet.addServices(paranetUAL, serviceUALs);
```

In this example:

* `paranetServiceName` specifies the name of the service.
* `paranetServiceDescription` provides a brief description of what the service does.
* `paranetServiceAddresses` lists blockchain addresses associated with the service. For off-chain services, this field can be left empty.
* `serviceUALs` is an array of Universal Asset Locators for the services you want to add to your Paranet.

By integrating and managing services, Paranet operators can expand the capabilities of their Paranet, providing a robust infrastructure for decentralized applications and AI-driven services.

#### Knowledge mining for Open Paranets

Paranets allow users to leverage collective intelligence by contributing their knowledge assets, enhancing the overall utility and value of the network. There are two primary ways to add a Knowledge Asset to a Paranet:

1. **Directly Mining Knowledge Assets to a Paranet**
2. **Submitting Existing Knowledge Assets to a Paranet**

To directly mine Knowledge Assets and add them to a Paranet, use the `dkg.asset.create` function and specify the `paranetUAL` as a parameter. Here’s an example:

```javascript
const content = {
    public: {
        '@context': ['https://schema.org'],
        '@id': 'uuid:22',
        company: 'KA-Company',
        user: {
            '@id': 'uuid:user:22',
        },
        city: {
            '@id': 'uuid:budapest',
        },
    }
};
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';

const knowledgeAsset = await DkgClient.asset.create(content, { epochsNum: 2, paranetUAL: paranetUAL });
console.log('Knowledge asset created with UAL: ', knowledgeAsset.UAL);
```

In this example, the Knowledge Asset is created and directly added to the specified Paranet.

If you have existing Knowledge Assets, you can submit them to a Paranet using the `dkg.asset.submitToParanet` function. Here’s an example:

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
const kaUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/55';

await DkgClient.asset.submitToParanet(kaUAL, paranetUAL);
```

Adding Knowledge Assets to Paranets can be done directly during the creation process or by submitting existing assets. This flexibility allows for robust management and contribution of knowledge, enhancing the collective intelligence and functionality of the Paranet.

#### Knowledge mining for Curated Paranets

In curated Paranets, there is a single method for adding Knowledge Assets, which is through the `dkg.asset.localStore` function.

Unlike open Paranets, where assets can be mined or submitted, curated Paranets offer more controlled management of data, ensuring consistency and integrity across the network. This approach enables users to store both public and private data on their node, providing enhanced security and control.&#x20;

Additionally, other nodes in the curated Paranet can synchronize data from your node, ensuring that all participating nodes have access to the most up-to-date information. This model prioritizes privacy, control, and efficient data sharing within a trusted network.

Here's an example of how to create a KA for Curated Paranet:

```javascript
const content = {
    public: {
        '@context': ['https://schema.org'],
        '@id': 'uuid:22',
        company: 'KA-Company',
        user: {
            '@id': 'uuid:user:22',
        },
        city: {
            '@id': 'uuid:budapest',
        },
    },
    private: {
        '@context': ['https://schema.org'],
        '@graph': [
            {
                '@id': 'uuid:user:1',
                name: 'Adam',
                lastname: 'Smith',
            },
            {
                @id': 'uuid:belgrade',
                title: 'Belgrade',
                postCode: '11000',
            },
        ],
    },
};
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';

const knowledgeAsset = await DkgClient.asset.localStore(content, { epochsNum: 2, paranetUAL: paranetUAL });
console.log('Knowledge asset created with UAL: ', knowledgeAsset.UAL);
```

#### Checking and Claiming Rewards

Participants in a Paranet can earn rewards for their various roles and contributions, such as knowledge mining, voting on proposals, or operating the Paranet. The dkg.js library provides functions to check if an address has a specific role within the Paranet and to claim rewards associated with that role.

**Roles in a Paranet:**

* **Knowledge Miners:** Contribute to the Paranet by mining knowledge assets.
* **Paranet Operators:** Manage the Paranet, including overseeing services and facilitating operations.
* **Proposal Voters:** Participate in decision-making by voting on the Initial Paranet Offering.

Participants can verify their roles and claim rewards through the following steps and examples:

<pre class="language-javascript"><code class="lang-javascript">const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';

// Check if an address is a knowledge miner
const isMiner = await dkg.paranet.isKnowledgeMiner(paranetUAL, { roleAddress: '0xMinerAddress' });
console.log('Is Knowledge Miner:', isMiner);

// Check if an address is a paranet operator
const isOperator = await dkg.paranet.isParanetOperator(paranetUAL, { roleAddress: '0xOperatorAddress' });
console.log('Is Paranet Operator:', isOperator);
<strong>
</strong><strong>// Check if an address is a voter
</strong>const isVoter = await dkg.paranet.isProposalVoter(paranetUAL, { roleAddress: '0xVoterAddress' });
console.log('Is Proposal Voter:', isVoter);

// Check claimable Knowledge miner rewards
const claimableMinerRewards = await dkg.paranet.getClaimableMinerReward(paranetUAL);
console.log('Claimable Miner Reward:', claimableMinerRewards);

// Claim miner rewards
await dkg.paranet.claimMinerReward(paranetUAL);
console.log('Miner rewards claimed successfully!');

// Check claimable operator rewards
const claimableVoterRewards = await dkg.paranet.getClaimableVoterReward(paranetUAL);
console.log('Claimable Voter Reward:', claimableVoterRewards);

// Claim voter rewards
await dkg.paranet.claimVoterReward(paranetUAL);
console.log('Voter rewards claimed successfully!');

// Check claimable operator rewards
const claimableOperatorRewards = await dkg.paranet.getClaimableOperatorReward(paranetUAL);
console.log('Claimable Operator Reward:', claimableOperatorRewards);

// Claim operator rewards
await dkg.paranet.claimOperatorReward(paranetUAL);
console.log('Operator rewards claimed successfully!');
</code></pre>

By following these steps, you can effectively check your role and claim the rewards you have earned for contributing to the Paranet. This system ensures that all participants are fairly compensated for their efforts, promoting a robust and active community within the Paranet.

#### Updating Claimable Rewards

In some cases, you may have already mined a knowledge asset to a specific Paranet but decided to update the knowledge asset. By doing so, you become eligible for additional NEURO rewards. To ensure that your claimable rewards reflect your new contributions, you need to call the `updateClaimableRewards` function for the Paranet. This function updates your claimable reward amounts based on your latest contributions.

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';

// Update claimable rewards for the specified Paranet
await dkg.paranet.updateClaimableRewards(paranetUAL);
console.log('Claimable rewards updated successfully!');
```

This function only updates the claimable rewards based on your latest contributions. To actually claim the rewards, use the respective claiming functions such as `claimMinerReward`, `claimVoterReward`, or `claimOperatorReward`.

#### Performing SPARQL Queries on a Specific Paranet

The Decentralized Knowledge Graph (DKG) enables users to perform SPARQL queries on specific Paranets. By specifying a Paranet, users can target their queries to retrieve data related to that Paranet. This can be particularly useful when working with domain-specific data or services within a Paranet.

To query a specific Paranet, ensure that the node you are querying has already enabled Paranet syncing for the Paranet you wish to query. Without this setup, the node may not have the relevant data required to process your queries.[ Read here](../../../dkg-v6-previous-version/node-setup-instructions/sync-a-dkg-paranet.md) how to setup node to sync a Paranet.

To query a specific Paranet, you can either specify the Paranet UAL using the `paranetUAL` parameter or set the `graphLocation` to the desired Paranet UAL. This approach allows you to direct your queries to the Paranet that holds the relevant data.

Here’s how you can perform a query on a specific Paranet using the `paranetUAL` parameter:

```javascript
 const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
 const queryWhereMadrid = `PREFIX schema: <http://schema.org/>
        SELECT DISTINCT ?graphName
        WHERE {
          GRAPH ?graphName {
            ?s schema:city <uuid:Madrid> .
        }
}`;

let queryResult = await dkg.graph.query(
        queryWhereMadrid,
        'SELECT',
        { paranetUAL: paranetUAL },
);

console.log(queryResult.data);

// Same query using graph location to pass Paranet UAL
queryResult = await dkg.graph.query(
        queryWhereMadrid,
        'SELECT',
        { graphLocation: paranetUAL },
);

console.log(queryResult.data);
```

By querying specific Paranets, you can leverage the powerful capabilities of the DKG to interact with domain-specific knowledge assets and services, ensuring that your queries are targeted and efficient. This makes it easier to work with complex data structures and gain insights from your Paranet's knowledge assets.

#### Federated SPARQL Queries

Federated SPARQL queries allow users to execute queries across multiple knowledge graphs or Paranets simultaneously. In the context of the Decentralized Knowledge Graph (DKG), a node might sync with multiple Paranets. Federated queries allow you to query multiple Paranets within a single SPARQL query, accessing data from each specified Paranet and merging the results.

Imagine you have a DKG node that synchronizes with three different Paranets. You want to perform a query that targets two of these Paranets to retrieve data about users and cities. Federated SPARQL queries provide a convenient way to specify which Paranets to include in your query.

If you need to query data across multiple specified Paranets, you should use federated SPARQL queries. However, if you want to query all available Paranets, you do not need to provide any specific arguments, as all Paranets will be queried by default using the default triple store repository.

To execute a federated SPARQL query, you can use the `SERVICE` keyword to specify the Paranet UALs you want to query. This keyword allows you to include data from different sources in your query.

Here’s an example of a federated query targeting two out of three Paranets:

```javascript
const federatedQuery = `
    PREFIX schema: <http://schema.org/>
        SELECT DISTINCT ?s ?city1 ?user1 ?s2 ?city2 ?user2 ?company1
        WHERE {
          ?s schema:city ?city1 .
          ?s schema:company ?company1 .
          ?s schema:user ?user1;
        
          SERVICE <${paranetUAL3}> {
            ?s2 schema:city <uuid:Belgrade> .
            ?s2 schema:city ?city2 .
            ?s2 schema:user ?user2;
          }
        
          filter(contains(str(?city2), "Belgrade"))
        }
    `;

    queryResult = await dkg.graph.query(
        federatedQuery,
        'SELECT',
        { graphLocation: paranetUAL1 },
    );
  
    console.log(queryResult.data);
```

**Explanation:**

* **`SERVICE` Keyword:** The `SERVICE` keyword is used to include data from Paranet 3 (`paranetUAL3`) in the query, while the primary Paranet is set to Paranet 1 (`paranetUAL1`).
* **Query Structure:** The query retrieves distinct subjects (`?s`), cities, users, and companies from Paranet 1, and performs a sub-query within Paranet 3 to get data where the city is `Belgrade`.
* **Filter Clause:** The `filter` clause is used to ensure that the city data from Paranet 3 contains the string "Belgrade".

Federated SPARQL queries provide a powerful way to aggregate and analyze data across multiple Paranets, this enables more complex data retrieval and cross-Paranet data integration, making it easier to gather comprehensive insights from diverse data sources.
