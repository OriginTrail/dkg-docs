# 🐛 Staking bug bounty

With intention to ensure the desired functioning of staking smart contracts, Trace Labs is opening a bounty programme. Each submission will be assessed according to its severity and will be associated with a particular bounty size.\


**Vulnerability categories:**

* Minor Bug: 500 TRAC
* Medium Bug: 2,500 TRAC
* Serious Bug: 5,000 TRAC
* Critical Bug: 10,000 TRAC

### Bug bounty rules

The assessment of the bug rating is in sole discretion of Trace Labs and will be based on both the likelihood and impact of the bug. All reward decisions are final.

Please send your bug reports to _bounty@origin-trail.com_, with the subject “STAKING BUG BOUNTY.” As soon as your bug report is received, we will evaluate the severity of the bug and will contact you. Bug submissions through other channels (eg. Telegram) will not be accepted. \


Additional rules of engagement that will apply:

* First come, first served.
* Issues that have already been submitted by another user are not eligible for bounty rewards.
* Public disclosure of a vulnerability makes it ineligible for a bounty.
* Paid auditors of the code are not eligible for rewards.

Other variables that can contribute to higher severity rating:

* Quality of description. Higher rewards are paid for clear, well-written submissions.
* Quality of reproducibility. Please include test code, scripts or detailed instructions. The easier it is for us to reproduce and verify the vulnerability, the higher the reward.
* Quality of fix, if included. Higher rewards are paid for submissions with a clear description of how to fix the issue.

### Bug bounty scope

The scope of this bug bounty program focuses on potential exploits specifically in the smart contracts relevant to the staking functionalities in the [dkg-evm-module](https://github.com/OriginTrail/dkg-evm-module), specifically:

* contracts/v2/Staking.sol contract and its dependencies.&#x20;
* contracts/v2/CommitManagerV1.sol
* contracts/v2/CommitManagerV1U1.sol
* contracts/v1/Profile.sol
* contracts/v1/ProofManagerV1.sol
* contracts/v1/ProofManagerV1U1.sol

The bounty branch can be found here: [https://github.com/OriginTrail/dkg-evm-module/tree/staking-bounty](https://github.com/OriginTrail/dkg-evm-module/tree/staking-bounty)

### Important restrictions

Please ensure that while doing testing you are not harming any live contracts on public networks, otherwise you will not be eligible for bug bounty.

Leaking any vulnerability of the smart contracts on any social media platforms or public channels will lead to cancellation of Bounty and might also invite legal action.

### Legal notice

We cannot issue rewards to individuals on sanctions lists, or who are in countries on sanctions lists. You are responsible for any tax implications depending on your country of residency and citizenship. There may be additional restrictions depending upon your local law.

This is a discretionary rewards program. We can cancel the program at any time, and the decision to pay a reward is entirely at Trace Labs discretion.

Your testing must not violate any law, or disrupt or compromise any data that is not your own.

To avoid potential conflicts of interest, we will not grant rewards to Trace Labs employees and contractors.

\
