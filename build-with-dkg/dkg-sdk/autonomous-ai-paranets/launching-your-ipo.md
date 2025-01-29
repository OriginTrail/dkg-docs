# Launching your IPO

{% hint style="danger" %}
**Paranets are not currently supported in V8. Expect the support to be back latest by the end of February.**
{% endhint %}

This page assumes you have completed the previous steps:

* you have [deployed your paranet](../../../dkg-v6-previous-version/autonomous-ai-paranets/deploying-a-paranet.md)
* you have [specified your ](../../../dkg-v6-previous-version/autonomous-ai-paranets/ipo-specification.md)[IPO](../../../dkg-v6-previous-version/autonomous-ai-paranets/ipo-specification.md) (defined all the properties including incentives, knowledge graph properties etc)

Once you have all these steps completed, you are able to initiate the IPO.

### 1.  Deploy your paranet incentives contract

The paranet incentive contract is the only type of contract that can receive NEURO incentives, as it implements the incentivisation logic. Other addresses, such as EOA addresses will not be accepted and are not eligible for incentives.&#x20;

To deploy your paranet incentive contract, either use the Paranet UI (coming soon) or execute the transaction directly on the contract.&#x20;

### 2. Publish your IPO specification to the Github repo

Provide details for your paranet [on the Paranets Github repo](https://github.com/OriginTrail/dkg-paranets) and provide as many details as possible. We recommend engaging with the community through other channels and social media to garner support for your IPO.

### 3. Launch a Governance proposal on Neuroweb

For a successful governance vote, your Neuroweb governance proposal should initiate a _forceTransfer_ extrinsic towards the _ParanetIncentivesPool_ contract address on Neuroweb.

More on Neuroweb governance proposals mechanics is available in the [Neuroweb docs](https://docs.neuroweb.ai/on-chain-governance/submit-a-governance-proposal).

### 4. Incentives are deployed to the paranet incentives contract

If your proposal is voted in by the Neuroweb governance voters, the requested funds will be dispatched to the paranet incentives contract. Once the contract is funded, the incentives can be claimed by knowledge miners, the operator and voters in the specified percentage. Incentives are only available though when knowledge mining occurs.

In the current version, IPO incentive emissions are directly correlated with the amount of TRAC tokens spent for publishing to the DKG through knowledge mining (if no knowledge is mined, no incentives can be claimed).

In the upcoming versions the IPOs will enable even more configurability of the emission mechanics, as we expect to see paranet and IPOs innovations to rapidly occur with the first IPOs. If you have ideas on how IPOs can be improved, come and share them in [Discord](https://discord.com/invite/qRc4xHpFnN)!

{% hint style="success" %}
Have any questions or feedback for this page? Hop into our [Discord channel](https://discord.com/invite/qRc4xHpFnN) and get in touch
{% endhint %}
