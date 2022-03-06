---
description: The OriginTrail v6 network monitoring system
---

# 👾 Telemetry Hub

The OriginTrail v6 telemetry hub is a system designed to monitor the Decentralized Knowledge Graph (DKG) network performance and provide feedback on the network activity.&#x20;

### What kind of data does the Telemetry hub collect?

The Telemetry hub aggregates node telemetry measurements - values such as the timestamps and durations of graph queries, inserts, network operations etc as well as errors observed during execution. These measurements are collected by each individual node on the v6 network and submitted to Telemetry hub in the following way:

* by generating measurement data assertions once per hour and publishing them to the DKG&#x20;
* by submitting a log of published assertion IDs to a centralized signalling server, used for double-checking the data pipeline incurs no data loss (potentially due to Telemetry Hub ingestion service or network communication issues)

![Nodes submit telemetry data to the DKG, later ingested by the Telemetry hub. Nodes also submit basic assertion information to a signalling server, used to double-check that all data has been successfully received by the Telemetry Hub](<../.gitbook/assets/ODN v6 diagrams - Page 41 (1).png>)

The telemetry hub then aggregates all information by operation and displays this information via several graphic dashboards. This information is useful for DKG developers when introducing new releases to the network and verifying the correct and efficient operation of the v6 implementation.



![Telemetry dashboard example](../.gitbook/assets/aa.png)

{% hint style="info" %}
Note: no personal data, keys or sensitive information is collected via the Telemetry system.
{% endhint %}

### The dual purpose of the Telemetry hub during OriginTrail v6 Beta&#x20;

The telemetry hub is in essence a Semantic Web3 application collecting and analysing telemetry data on the usage of the DKG, by using the DKG itself for monitoring its **performance**. During the beta however there is one more purpose - testing the DKG **functionalities** in the real-world environment, in order to be able reach of TRL8 and TRL9 (see "[NASA technology readiness levels](https://www.nasa.gov/directorates/heo/scan/engineering/technology/technology\_readiness\_level)").

Therefore it is expected that during beta stages the Telemetry will collect errors, reveal previously undetected issues and problems - all of these are valuable to the OriginTrail Developer community. By running a v6 node you can contribute to the mission [and earn bounty rewards](v6-bounty-program.md)!

### How can you verify your node is submitting data to telemetry?

If you are running an OriginTrail v6 testnet node, you can contribute to the Telemetry system and increase your bounty score. You will need to verify the following:

* Check that your node is up to date with the latest v6 node version (you can find the latest release [on Github](https://github.com/OriginTrail/ot-node/releases)). There is an autoupdating feature during the beta stage to make sure your node is updated constantly. This feature is turned on by default. To confirm this and also your node's current version, point your browser to http://<ip--of-ot-node>:8900/info (see screenshot below)
* Make sure that the node operational wallet has enough tokens&#x20;
  * Polygon Mumbai MATIC testnet tokens (from launch stage 1 onwards). You can request testnet MATIC tokens for free from [this faucet](https://faucet.polygon.technology/). Currently the testnet node is spending about 0.076 MATIC per day. The faucet will transfer 0.5 MATIC on each request. The faucet has not been working 100% of the time lately. In case you don't receive any MATIC within a few minutes, you can check if the faucet is working by looking for errors in recent transactions [at this contract address](https://mumbai.polygonscan.com/address/0x7f092e65c688a509737fcd8d0998dd12208f5297)
  * Test TRAC tokens (from launch stage 2 onwards) - not applicable yet
* Make sure your node is communicating properly [with the Polygon Mumbai RPC](https://docs.polygon.technology/docs/develop/network-details/network/) endpoints. (? how to do this? check logs? then is redudant with the next point). 
* Make sure that your node is operating properly by checking the node logs. Login to your testnet server and monitor the log with the command `journalctl -u otnode --output cat -fn 100`
* Check if your node telemetry plugin has been enabled by using the node API info route on your browser (http://<ip--of-ot-node>:8900/info See screenshot below from Postman)

![Example of the response from a node /info API call showing the latest version and if telemetry data is being sent ](<../.gitbook/assets/Screen Shot 2022-03-04 at 14.27.16.png>)

Additionally, check the [Telemetry Debug Dashboard](https://telemetry.origintrail.io/d/ddf1iEf7k/bounty-scoreboards) to find your node's contribution:

* Find your node wallet address in the table
* Check that the "records\_seen\_by\_signaling\_server" is greater than 0 (the number should be close to 24 as the node should submit one telemetry report assertion every hour)
* Check that the "records\_fetched\_from\_the\_network" is greater than 0. We expect this number to be equal or close to the "records\_seen\_by\_signaling\_server" - a lower number would mean that the assertion data submitted by your node has not been processed by the telemetry hub yet&#x20;
* Check the latest timestamps of submission, particularly the "signaling\_timestamp\_of\_last\_record\_seen" - if this number is not close to the current time (in GMT), that means your node might not be operating properly

{% hint style="info" %}
The Telemetry data received might be lagging behind (not realtime) which is expected. The Telemetry hub data processing pipeline is constantly being tuned in such a way that the network telemetry data can be visualized as close as possible to real-time.
{% endhint %}

{% hint style="info" %}
The bounty scoreboard table is only showing a list of nodes, ranked randomly **until the official launch of the Telemetry bounty** (tentatively scheduled for March 9th 2022). The table is only used to check if the bounty results are being received, the ranking positions are not relevant.
{% endhint %}



### What should you do if you observe issues?

After checking the above list and not being able to resolve any issues, please contact the developers directly [on Discord](https://discordapp.com/invite/FCgYk2S).



