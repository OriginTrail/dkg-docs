---
description: >-
  In order to configure your node, you will need to update your
  .origintrail_noderc (configuration) file located inside of your ot-node
  directory.
---

# Configuring your node

Below is an example configuration that indicates how to configure some of the modules:

* Configure auto updater&#x20;
* Configure multiple blockchains (coming soon)&#x20;
* Configure RPC endpoints&#x20;
* Configure triple store

```json
{
    "modules": {
        "autoUpdater": {
            "enabled": true,
            "implementation": {
                "ot-auto-updater": {
                    "package": "./auto-updater/implementation/ot-auto-updater.js",
                    "config": {
                        "branch": "v6/release/..."
                    }
                }
            }
        },
        "blockchain": {
            "defaultImplementation": "otp",
            "implementation": {
                "otp": {
                    "config": {
                        "rpcEndpoints": [
                            "wss://lofar.origintrail.network",
                            "wss://lofar.origin-trail.network"
                        ],
                        "evmOperationalWalletPublicKey": "0x8385...",
                        "evmOperationalWalletPrivateKey": "0x88b...",
                        "evmManagementWalletPublicKey": "0x813..."
                    }
                }
            }
        },
        "tripleStore": {
            "defaultImplementation": "ot-blazegraph"
        },
        "httpClient": {
            "implementation": {
                "express-http-client": {
                    "config": {
                        "useSsl": true
                    }
                }
            }
        }
    },
    "auth": {
        "ipWhitelist": [
            "::1",
            "127.0.0.1"
        ]
    },
    "hostname": "https://my-node.hostname"
}

```

{% hint style="info" %}
After each update of the configuration, the node needs to be restarted.
{% endhint %}
