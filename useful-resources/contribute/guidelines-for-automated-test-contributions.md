---
description: Contribute to DKGv6 by growing the automated test suite for the ot-node!
---

# Guidelines for automated test contributions

Welcome to the automated tests contribution guidelines! By contributing to ot-node automated test suite, you help further the progress of OriginTrail technology development and increase the robustness of the DKG implementation. Detailed instructions on how you can participate are described below, however if you need any assistance feel free to [jump into Discord](https://discord.com/invite/FCgYk2S) and ask for help from the community or core developers there.

{% hint style="info" %}
This guide applies to the DKG node Github repo, particularly for the v6 branches (v6/develop being the default branch). If you are creating a contribution, branch off from v6/develop.
{% endhint %}

\
We use [**Cucumber.js**](https://cucumber.io/) for running automated tests. This framework uses the Gherkin language, which allows expected software behaviors to be specified in a logical language that can be easily understood.

For a detailed guide on how to write BDD scenarios, visit [Cucumber docs](https://cucumber.io/docs/gherkin/reference/).

Tests need to cover errors listed in [github discussions](https://github.com/OriginTrail/ot-node/discussions/2095) page. Different errors are thrown in different commands, all of which are executed by the **command executor**. To learn what the command executor is and how it works, please visit [command-executor.md](../../decentralized-knowledge-graph/implementation-details/command-executor.md "mention").

### Steps to contribute BDD tests

1. Check out [github discussions](https://github.com/OriginTrail/ot-node/discussions/2095) to see current test requirements. Check out the existing steps available in `./ot-node/test/bdd/steps`.
2. Create a feature file where you'll define new scenarios. Features should be located in **test/bdd/features** directory with the appropriate file name format: _**\<operation>**_**-errors.feature** (e.g. _publish-errors.feature, get-errors.feature_).&#x20;
3. When you're done with the scenarios that you've created, following the [.](./ "mention"), create a **draft PR** and tag at least two core developers (and as many other community members as you wish). The team members will review the feature files and either give approval or request for changes. Once you get a confirmation that the feature files are satisfactory, you can continue with corresponding step definitions. This helps provide feedback on the contribution early on.
4. Put step definitions in the `./ot-node/test/bdd/steps` directory.
5. Implement the steps and ensure that both old tests and the new ones you just created are passing locally (use the `npm run test:bdd` command). Node logs can be found in **./ot-node/test/bdd/log/**_**\<scenario-name>**_**/origintrail-test-**_**\<index>**_**.log**(e.g. _test/bdd/log/Publishing-a-valid-assertion/origintrail-test-0.log)._
6. When you're satisfied with the scenarios and their step definitions, you may now mark your PR draft as "Ready for review".
7. There will likely be feedback on your PR before it gets approved, so make sure to follow the status of your PR contribution. After PR approval, your changes will be merged.&#x20;
8. Congratulations! You've just made ot-node more robust :tada:

