# IPO registration

The following parameters are necessary for starting an IPO referendum on Neuroweb:&#x20;

#### 1. Pick your blockchain.&#x20;

Initially starting on NeuroWeb blockchain, the paranets feature will be rolled out in the future to all other DKG enabled blockchains as well.

#### 2. Create your Paranet Registry Knowledge Asset.&#x20;

You can use the following template JSON-LD object as a template for your Paranet Registry Knowledge Asset. Once created, make sure to store its UAL to use in the IPO proposal.

```json
{
  "@context": "http://schema.org/",
  "@type": "DataCatalog",
  "name": "Your Paranet Name",
  "description": "Description of your paranet",
  "keywords": "keyword1, keyword2, keyword3 ...",
}
```

#### 3. Create the Paranet incentive contract&#x20;

The paranet incentive contract is the only type of contract that can receive NEURO incentives, as it implements the incentivisation logic. Other addresses, such as EOA addresses will not be accepted and are not eligible for incentives.&#x20;

To deploy your paranet incentive contract, submit the contract initialization transaction via the Paranet Factory contract. A paranet registration UI enabling this feature is coming soon.

{% hint style="info" %}
The wallet address you use for this transaction will be recorded as the paranet operator wallet address and will be the address claiming the operator NEURO incentives.
{% endhint %}



{% hint style="success" %}
Have any questions or feedback for this page? Hop into our [Discord channel](https://discord.com/invite/qRc4xHpFnN) and get in touch
{% endhint %}
