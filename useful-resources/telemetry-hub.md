---
description: The OriginTrail v6 network monitoring system
---

# 👾 Telemetry Hub

The OriginTrail v6 telemetry hub is a system designed to monitor the Decentralized Knowledge Graph network performance and provide feedback on the network activity.&#x20;

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

### What should you do if you observe issues?

After checking the above list and not being able to resolve any issues, please contact the developers directly [on Discord](https://discordapp.com/invite/FCgYk2S).

