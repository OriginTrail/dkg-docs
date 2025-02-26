# Paranets Incentives Pool Implementation

**The Incentives Pool** is designed to motivate key participants in the Paranet ecosystem by rewarding them for their contributions. Knowledge miners, voters, and operators all play crucial roles in maintaining and growing the system. These incentives ensure the continued success and proper functioning of the network.

### Incentives pool options&#x20;

The `incentivesPoolOptions` object defines the parameters for the reward system within the Paranet ecosystem. It includes the following key settings:

```javascript

const incentivesPoolOptions = {
        tracToTokenEmissionMultiplier: 5,
        operatorRewardPercentage: 10.0,
        incentivizationProposalVotersRewardPercentage: 12.0,
        incentivesPoolName: 'YourIncentivesPoolName',
        rewardTokenAddress: '0x0000000000000000000000000000000000000000',
 };
```

* **tracToTokenEmissionMultiplier**: A multiplier that affects the token emission rate, determining how much reward is distributed based on user actions.
* **operatorRewardPercentage**: Operators, who are responsible for managing and maintaining the Paranet.
* **incentivizationProposalVotersRewardPercentage**: Voters who participate in proposals.
* **incentivesPoolName**: Sets the name of the pool.
* **rewardTokenAddress**: This specifies the address of the reward token. If zero address is set than chain's native toke is used for Incentivization.

### Deployment of incentives pool&#x20;

This code deploys the incentives contract for the Paranet using the specified options and `paranetUAL`, then logs the deployment result to verify its success.

```javascript
    const paranetDeployed = await DkgClient.paranet.deployIncentivesContract(
        paranetUAL,
        incentivesPoolOptions,
    );
    console.log('======================== PARANET INCENTIVES POOL DEPLOYED');
    console.log(paranetDeployed);
    divider();
```
