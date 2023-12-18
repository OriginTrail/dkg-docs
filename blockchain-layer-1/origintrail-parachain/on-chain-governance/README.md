# On-chain Governance

In the OriginTrail Parachain Governance , **active OTP token holders** and **the council** together administrate network upgrade decisions and can vote on various topics. Whether the proposal is proposed by the public (token holders) or the council, it will eventually have to go through a **referendum** to let all OTP holders, weighted by stake and conviction, collectively make a decision on the proposal. To ensure timely governance, a General Council is elected to propose, cancel and fast track referendums.

## General council

The General council is an on-chain entity comprising several actors, each represented as an on-chain account. On OriginTrail Parachain, the initial council consists of 5 members, however the number of council members can be increased over time via governance proposals. The council is called upon primarily for three tasks of governance:

1. proposing sensible referenda,
2. canceling uncontroversially dangerous or malicious referenda,
3. fast track referenda proposal.

Members of the council can be checked [here](https://origintrail.subscan.io/account?role=councilMember).

## Democracy

Democracy module handles the administration of general stakeholder voting and has the ability to perform root calls.

There are two different queues that a proposal can be added to before it becomes a referendum:

1. the proposal queue consisting of all public proposals,
2. the external queue consisting of a single proposal that originates from one of the external origins (such as the council).

Every launch period, the [Democracy pallet](https://crates.parity.io/pallet\_democracy/index.html) launches a referendum from a proposal that it takes from either the proposal queue or the external queue in turn. Any token holder in the system can vote on referenda. The voting system uses **time-lock token based voting** by allowing the token holder to set their **conviction** behind a vote. The conviction will dictate **the length of time the tokens will be locked**, as well as the multiplier that scales the vote power. For more details on the implementation of the Democracy module in Substrate, please refer to this [link](https://crates.parity.io/pallet\_democracy/index.html), and for more details on how to participate in democracy, please refer to this [link](https://wiki.polkadot.network/docs/maintain-guides-democracy).

### Referenda

Referenda are simple, inclusive, stake-based voting schemes. Each referendum has a specific proposal associated with it that takes the form of a privileged function call in the runtime (that includes the most powerful call: set\_code = runtime upgrade).

Referenda are discrete events, have a fixed period during which the voting happens, and then are tallied and the function call is made if the vote is approved. Referenda are always binary; your only options in voting are "**aye**", "**nay**", or abstaining entirely.

Referenda can be launched in one of 3 ways:

1. Publicly submitted proposals;
2. Proposals submitted by the general council, either through a majority or unanimously;
3. Emergency proposals submitted by the general council (fast-tracked).

In case of options 1 and 2, the voting lasts for a fixed period of time, and for option 3, the period can be set differently every time.

#### Voting

To vote in a referendum, a voter generally must lock their tokens up for at least the enactment delay period beyond the end of the referendum. This is in order to ensure that some minimal economic buy-in to the result is needed and to dissuade vote selling.

Depending on which entity proposed the proposal and whether all council members voted yes, there are three different scenarios:

1. Public - Positive Turnout Bias (Super-Majority Approve);
2. The general council (Complete agreement) - Negative Turnout Bias (Super Majority Against);
3. The general council (Majority agreement) - Simple majority.

**Super-Majority Approve**

A positive turnout bias, whereby a heavy super-majority of aye votes is required to carry at low turnouts, but as turnout increases towards 100%, it becomes a simple majority-carries as below.

[![alt\_text](https://github.com/OriginTrail/OT-RFC-repository/raw/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image1.png)](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image1.png)

**Super-Majority Against**

A negative turnout bias, whereby a heavy super-majority of nay votes is required to reject at low turnouts, but as turnout increases towards 100%, it becomes a simple majority-carrying as below.

[![alt\_text](https://github.com/OriginTrail/OT-RFC-repository/raw/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image2.png)](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image2.png)

**Simple-Majority**

Majority-carries, a simple comparison of votes; if there are more aye votes than nay, then the proposal is carried, no matter how much stake votes on the proposal.

[![alt\_text](https://github.com/OriginTrail/OT-RFC-repository/raw/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image3.png)](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image3.png)

**Example**

For the demonstration below, let’s assume there are 1500 OTP tokens in the network and the proposal is issued by the public (not by the general council).

* Peter: Votes No with 150 OTP for a 16 week lock period => 150 x 3\* = 450 Votes
* Logan: Votes Yes with 500 OTP for a 4 week lock period => 500 x 1 = 500 Votes
* Kevin: Votes Yes with 100 OTP for a 4 week lock period => 100 x 1 = 100 Votes

\*The conviction multiplier increases the vote multiplier by one every time the number of lock periods doubles.

To calculate the voting result, we need 4 variables and the formulas listed below:

* Approve (number of aye votes) = 600
* Against (number of nay votes) = 450
* Turnout (total number of voting tokens, does not include conviction) = 750
* Electorate (total number of tokens issued in the network) = 1500

Since the referendum was proposed by the public (not the general council), “Super Majority Approve” formula would be used to calculate the result.

[![alt\_text](https://github.com/OriginTrail/OT-RFC-repository/raw/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image4.png)](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image4.png)\
which yields

[![alt\_text](https://github.com/OriginTrail/OT-RFC-repository/raw/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image5.png)](https://github.com/OriginTrail/OT-RFC-repository/blob/main/RFCs/OT-RFC-15-OriginTrail-Parachain-Governance/images/image5.png)

Super Majority Approve requires more aye votes to pass the referendum when turnout is low, therefore, based on the above result, the referendum will be rejected. In addition, only the winning voter's tokens are locked. If the voters on the losing side of the referendum believe that the outcome will have negative effects, their tokens are transferable so they will not be locked into the decision.

More details on voting and referendums are available [here](https://wiki.polkadot.network/docs/learn-governance#council).
