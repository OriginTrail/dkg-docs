---
description: >-
  Help publishers by providing API access to the DKG and increase your node
  reward potential
---

# How to open up your node for publishing

One way to increase your Node Power is to make your DKG Core node endpoint publicly accessible to enable publisher access to the DKG. This servers a useful purpose to the network by opening access to the DKG, enabling easier usage and sharing resources, for which Core nodes are incentivised through increasing Node power.&#x20;

To make your DKG Core node endpoint publicly accessible, all you need to do is disable both IP-based and token-based authentication. This is done by setting `ipBasedAuthEnabled` and `tokenBasedAuthEnabled` to `false` in the `.origintrail_noderc` file located inside your `ot-node` directory.&#x20;

{% hint style="info" %}
`ipBasedAuthEnabled` and `tokenBasedAuthEnabled` fields are not present by default, so you must add them manually.
{% endhint %}

Below is an example of how your `"auth"` section should be configured in order to disable IP-based and token-based authentication.

```json
...
    },
    "auth": {
        "ipBasedAuthEnabled": false,
        "tokenBasedAuthEnabled": false,
        "ipWhitelist": [
            "::1",
            "127.0.0.1",
            "<any_whitelist_ip_of_choice>"
        ]
    }
...
```

{% hint style="success" %}
Opening your node endpoint by disabling authentication is considered a safe operation. This configuration exposes the node’s API to the public but does not expose any sensitive data such as your node wallets, private keys, or tokens.&#x20;
{% endhint %}

{% hint style="warning" %}
Managing rate limits and protecting the endpoint excessive requests is the responsibility of the node operator.
{% endhint %}

Changes to `.origintrail_noderc` only take effect after a restart. Once the node is back online, its endpoint will be accessible without authentication restrictions.&#x20;

Anyone can now use one of the [dkg clients](../../../build-a-dkg-node-ai-agent/advanced-features-and-toolkits/dkg-sdk/) to connect to your Core node an publish through it. So if for example your node URL is _https://super-dkg-node.com_, this is how dkg.js can connect to it:

```javascript
const dkg = new DKG({
    endpoint: 'https://super-dkg-node.com',  // your node URL
    port: 8900 // your node DKG Port
});

const nodeInfo = await dkg.node.info(); 
// if successfully connected, the will return an object indicating the node version
// { 'version': '8.X.X' }
```
