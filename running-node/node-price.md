# Price setup

The data creators have the ability to set pricing through simplified setting called Lambda, which is a combination of dataset size, duration of the data, and gas fees required to start and finalize the bidding process. Lambda could range from 0 to 15.

In similar fashion, the data holders can choose how well paid jobs they want to accept and set accordingly their node settings.

The Lambda setting is present in the node configuration file, which can be accessed through:

```text
nano /root/.origintrail_noderc
```

The actual setting is called dh\_price\_factor and can be setup for each separate blockchain network.

```text
"dh_price_factor" : "1",
```





