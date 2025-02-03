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

# Interact with DKG paranets

{% hint style="danger" %}
**Paranets are not currently supported in V8. Expect the paranet support to be back latest by the end of February.**
{% endhint %}

The DKG JavaScript SDK provides functionality for interacting with paranets on the OriginTrail Decentralized Knowledge Graph (DKG). This section of the SDK allows developers to create, manage, and utilize paranets effectively.

## Setup and installation

To interact with paranets, you need to connect to a running OriginTrail node (either local or remote) and ensure you have the dkg.js SDK installed and properly configured.&#x20;

Follow the general setup instructions for [installing dkg.js](./) and read more about paranets [in the following section](../../../dkg-v6-previous-version/autonomous-ai-paranets/).

### Creating a paranet

Before creating a paranet, you must first create a Knowledge Asset (KA) on the DKG that will represent the paranet. To create a Knowledge Asset on the DKG, refer to [the following page](./).

Once the Knowledge Asset is created, it will have a unique identifier known as a Universal Asset Locator (UAL). You will use this UAL to create a paranet. The paranet creation process essentially links the paranet to the Knowledge Asset, establishing it on the blockchain. This on-chain representation allows for decentralized management and interaction with the paranet.

Here is an example of how to create a new paranet using the `create` function from the paranet module. This function requires the UAL of the previously created Knowledge Asset, along with other details such as the paranet's name and description:

```javascript
const UAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1/1';
await dkg.paranet.create(UAL, {
        paranetName: 'AiParanet',
        paranetDescription: 'AI agents paranet for demonstration purposes.',
        paranetNodesAccessPolicy: PARANET_NODES_ACCESS_POLICY.OPEN,
        paranetMinersAccessPolicy: PARANET_MINERS_ACCESS_POLICY.OPEN,
});
```

In this example:

* `UAL` is the unique identifier of the Knowledge Asset created on the DKG.
* `paranetName` is the name you want to give to your paranet. It should be descriptive enough to indicate the paranet's purpose or focus.
* `paranetDescription` provides additional context about the paranet, explaining its purpose and the types of Knowledge Assets or services it will involve.
* `paranetNodesAccessPolicy` defines a paranet's policy towards including nodes. If OPEN, any node can be a part of the paranet.
* `paranetMinersAccessPolicy` defines a paranet's policy towards including knowledge miners. If OPEN, anyone can publish to a paranet.&#x20;

After the paranet is successfully created, the paranet UAL can be used to interact with it. This includes deploying services within the paranet, managing incentives, and claiming rewards associated with the paranet's operations.

### Adding services to a paranet

Enhance the capabilities of your paranet by integrating new services. The `addServices` function allows you to add both on-chain and off-chain services to your paranet. These services can range from AI agents and data oracles to decentralized knowledge interfaces and more.

Before adding services, you first need to create them using the `createService` function. Services added to a paranet can either have on-chain addresses, representing smart contracts or other on-chain entities, or they can be off-chain services, which do not have associated blockchain addresses.

Each service can be identified by all paranet users via its registry Knowledge Asset and can include multiple on-chain accounts under its control. This enables services to participate in economic activities within the DKG.

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1/1';
const serviceUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/2/1';
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

By integrating and managing services, paranet operators can expand the capabilities of their paranet, providing a robust infrastructure for decentralized applications and AI-driven services.

## Knowledge mining for open paranets

Paranets allow users to leverage collective intelligence by contributing their Knowledge Assets, enhancing the overall utility and value of the network. There are two primary ways to add a Knowledge Asset to a paranet:

1. **Submitting existing Knowledge Assets to a paranet**

If you have existing Knowledge Assets, you can submit them to a paranet using the `dkg.asset.submitToParanet` function.&#x20;

Here’s an example:

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1/1';
const kaUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/55';

await DkgClient.asset.submitToParanet(kaUAL, paranetUAL);
```

Adding Knowledge Assets to paranets can be done directly during the creation process or by submitting existing assets. This flexibility allows for robust management and contribution of knowledge, enhancing the collective intelligence and functionality of the paranet.

## Checking and claiming rewards

Participants in a paranet can earn rewards for their various roles and contributions, such as knowledge mining, voting on proposals, or operating the paranet. The dkg.js library provides functions to check if an address has a specific role within the paranet and to claim rewards associated with that role.

**Roles in a paranet:**

* **Knowledge miners:** Contribute to the paranet by mining Knowledge Assets.
* **Paranet operators:** Manage the paranet, including overseeing services and facilitating operations.
* **Proposal voters:** Participate in decision-making by voting on the Initial Paranet Offering (IPO).

Participants can verify their roles and claim rewards through the following steps and examples:

<pre class="language-javascript"><code class="lang-javascript">const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1/1';

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

By following these steps, you can effectively check your role and claim the rewards you have earned for contributing to the paranet.&#x20;

This system ensures that all participants are fairly compensated for their efforts, promoting a robust and active community within the paranet.

## Updating claimable rewards

In some cases, you may have already mined a Knowledge Asset to a specific paranet but decided to update the Knowledge Asset. By doing so, you become eligible for additional NEURO rewards.&#x20;

To ensure that your claimable rewards reflect your new contributions, you need to call the `updateClaimableRewards` function for the paranet. This function updates your claimable reward amounts based on your latest contributions.

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1/1';

// Update claimable rewards for the specified Paranet
await dkg.paranet.updateClaimableRewards(paranetUAL);
console.log('Claimable rewards updated successfully!');
```

This function only updates the claimable rewards based on your latest contributions. To actually claim the rewards, use the respective claiming functions, such as `claimMinerReward`, `claimVoterReward`, or `claimOperatorReward`.

## Performing SPARQL queries on a specific paranet

The DKG enables users to perform SPARQL queries on specific paranets. By specifying a paranet, users can target their queries to retrieve data related to that paranet. This can be particularly useful when working with domain-specific data or services within a paranet.

To query a specific paranet, ensure that the node you are querying has already enabled paranet syncing for the paranet you wish to query. Without this setup, the node may not have the relevant data required to process your queries.[ ](../../../dkg-v6-previous-version/node-setup-instructions/sync-a-dkg-paranet.md)

[Read here](../../../dkg-v6-previous-version/node-setup-instructions/sync-a-dkg-paranet.md) how to set up a node to sync a paranet.

To query a specific paranet, you can either specify the paranet UAL using the `paranetUAL` parameter or set the `graphLocation` to the desired paranet UAL. This approach allows you to direct your queries to the paranet that holds the relevant data.

Here’s how you can perform a query on a specific paranet using the `paranetUAL` parameter:

```javascript
 const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1/1';
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

By querying specific paranets, you can leverage the powerful capabilities of the DKG to interact with domain-specific Knowledge Assets and services, ensuring that your queries are targeted and efficient. This makes it easier to work with complex data structures and gain insights from your paranet's Knowledge Assets.

### Federated SPARQL queries

Federated SPARQL queries allow users to execute queries across multiple knowledge graphs or paranets simultaneously. In the context of the DKG, a node might sync with multiple paranets. Federated queries allow you to query multiple paranets within a single SPARQL query, accessing data from each specified paranet and merging the results.

Imagine you have a DKG node that synchronizes with three different paranets. You want to perform a query that targets two of these paranets to retrieve data about users and cities. Federated SPARQL queries provide a convenient way to specify which paranets to include in your query.

If you need to query data across multiple specified paranets, you should use federated SPARQL queries. However, if you want to query all available paranets, you do not need to provide any specific arguments, as all paranets will be queried by default using the default triple store repository.

To execute a federated SPARQL query, you can use the `SERVICE` keyword to specify the paranet UALs you want to query. This keyword allows you to include data from different sources in your query.

Here’s an example of a federated query targeting two out of three paranets:

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

* **`SERVICE` keyword:** The `SERVICE` keyword is used to include data from Paranet 3 (`paranetUAL3`) in the query, while the primary paranet is set to Paranet 1 (`paranetUAL1`).
* **Query structure:** The query retrieves distinct subjects (`?s`), cities, users, and companies from Paranet 1, and performs a sub-query within Paranet 3 to get data where the city is `Belgrade`.
* **Filter clause:** The `filter` clause is used to ensure that the city data from Paranet 3 contains the string "Belgrade".

Federated SPARQL queries provide a powerful way to aggregate and analyze data across multiple paranets, this enables more complex data retrieval and cross-paranet data integration, making it easier to gather comprehensive insights from diverse data sources.
