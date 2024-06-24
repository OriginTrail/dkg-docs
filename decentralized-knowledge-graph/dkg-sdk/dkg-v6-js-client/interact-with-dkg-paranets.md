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

The DKG JavaScript SDK provides functionality for interacting with Paranets on the OriginTrail Decentralized Knowledge Graph. This section of the SDK allows developers to create, manage, and utilize paranets effectively.

#### Setup and Installation

To interact with Paranets, you need to connect to a running OriginTrail node (either local or remote) and ensure you have the dkg.js SDK installed and properly configured. Follow the general setup instructions for[ installing dkg.js](./) and read more about Paranets [in the following section](../../autonomous-ai-paranets/).

#### Creating a Paranet

Before creating a Paranet, you must first create a Knowledge Asset (KA) on the Decentralized Knowledge Graph (DKG) that will represent the Paranet. To create a Knowledge Asset on the DKG refer to [the following page.](./)

Once the Knowledge Asset is created, it will have a unique identifier known as a Universal Asset Locator (UAL). To create a Paranet, you will use this UAL. The Paranet creation process essentially links the Paranet to the Knowledge Asset, establishing it on the blockchain. This on-chain representation allows for decentralized management and interaction with the Paranet.

Here is an example of how to create a new Paranet using the `create` function from the Paranet module. This function requires the UAL of the previously created Knowledge Asset, along with other details such as the Paranet's name and description:

```javascript
const UAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
await dkg.paranet.create(UAL, {
        paranetName: 'AiParanet',
        paranetDescription: 'AI agents paranet for demonstration purposes.',
});
```

In this example:

* `UAL` is the unique identifier of the Knowledge Asset created on the DKG.
* `paranetName` is the name you want to give to your Paranet. It should be descriptive enough to indicate the Paranet's purpose or focus.
* `paranetDescription` provides additional context about the Paranet, explaining its purpose and the types of knowledge assets or services it will involve.

After the Paranet is successfully created, the Paranet UAL can be used to interact with the specific Paranet. This includes deploying services within the Paranet, managing incentives, and claiming rewards associated with the Paranet's operations.

#### Deploying Incentives for a Paranet

The `deployIncentivesContract` function sets up the incentive mechanism for a Paranet, ensuring that contributors are fairly rewarded for their efforts. This function requires the `paranetUAL` as the first parameter, which is the Universal Asset Locator for the Paranet. The second parameter specifies the type of incentivization mechanism, currently limited to 'Neuroweb'.

The incentivization mechanism is only available on the NeuroWeb blockchain, meaning 'Neuroweb' is the only supported `incentiveType` at this time. When the Paranet receives incentives, these will be distributed according to predefined rules: a portion goes to the Paranet operator, another portion is shared among voters who supported proposals, and the remainder is dedicated to knowledge miners who contributed to the Paranet.

```javascript
const paranetUAL = 'did:dkg:hardhat1:31337/0x791ee543738b997b7a125bc849005b62afd35578/1';
await dkg.paranet.deployIncentivesContract(paranetUAL, 'Neuroweb', {
    tracToNeuroEmissionMultiplier: 2.5,
    operatorRewardPercentage: 10.00,
    incentivizationProposalVotersRewardPercentage: 10.00,
});
```

In this example:

* `paranetUAL` is the identifier of the Paranet on the DKG.
* `'Neuroweb'` specifies the type of incentivization mechanism, currently limited to the NeuroWeb blockchain.

The object passed as the third parameter includes the following properties:

* **TRAC to NEURO Emission Multiplier:** This defines the conversion rate for emissions. For instance, with a multiplier of `2.5`, for every 1 TRAC used in knowledge mining, 2.5 NEURO will be emitted. This is distributed among the contributors as follows:
  * **Paranet Operator:** Receives a percentage of the emissions, calculated as a fraction of the TRAC used (10% of 2.5 NEURO).
  * **Proposal Voters:** Share the remaining portion of the emissions, rewarded for supporting incentivization proposals (10% of 2.5 NEURO).
  * **Knowledge Miners:** Receive the rest of the emissions, equating to 2 NEURO per 1 TRAC used in this case.
* **Operator Reward Percentage:** Defines the portion of the NEURO emissions that will be allocated to the Paranet operator as a fee. For example, if set to `10.00%`, the operator receives 0.25 NEURO per 1 TRAC used for knowledge mining.
* **Incentivization Proposal Voters Reward Percentage:** Specifies the percentage of NEURO emissions that will be distributed among the voters who supported incentivization proposals. For instance, with a `10.00%` setting, 0.25 NEURO will be shared among the voters per 1 TRAC used.

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

To query a specific Paranet, ensure that the node you are querying has already enabled Paranet syncing for the Paranet you wish to query. Without this setup, the node may not have the relevant data required to process your queries.[ Read here](../../node-setup-instructions/sync-a-dkg-paranet.md) how to setup node to sync a Paranet.

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
