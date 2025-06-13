# Permissioned Paranets

Paranet Permission Policies define which Nodes and Knowledge Miners can participate in a Paranet. These policies are set by the Paranet Operator at the time of creation.

{% hint style="info" %}
A Paranet Operator is the account that owns the Knowledge Asset from which the Paranet was created.
{% endhint %}

There are two permission policies:

• PARANET\_NODES\_ACCESS\_POLICY – governs which nodes can sync Knowledge Collections.

• PARANET\_MINERS\_ACCESS\_POLICY – governs which knowledge miners (wallet addresses) can submit Knowledge Collection

{% hint style="info" %}
Here is demo code for a [Permissioned Paranet](https://github.com/OriginTrail/dkg.js/blob/v8/develop/examples/curated-paranet-demo.js).&#x20;
{% endhint %}

### Paranet Node Access Permissioned Policy

This policy controls which nodes are allowed to sync the Paranet’s Knowledge Collections and whether they can sync the private part of the collection.

* OPEN — any node can sync the Paranet and only the public part of Knowledge Collections is included
* PERMISSIONED — only approved nodes sync the Paranet and both public and private part of Knowledge Collection are included. Enabled private knowledge sharing!

#### Interacting with Node Acess Permisioned Paranet

Paranet Operator can add Nodes to Permissioned Paranet

```javascript
await DkgClient.paranet.addPermissionedNodes(paranetUAL, identityIds)
```

Paranet Operator can remove Nodes from Permissioned Paranet

```javascript
await DkgClient.paranet.removePermissionedNodes(paranetUAL, identityIds);
```

Anybody can check which nodes are part of Paranet:

```javascript
await DkgClient.paranet.getPermissionedNodes(paranetUAL);
```

### Paranet Miner Access Permissioned Policy

This policy defines who can submit Knowledge Collections to a Paranet.

* OPEN — any knowledge miner (address) can submit Knowledge Collection&#x20;
* PERMISSIONED — only allowed knowledge miner (address) can submit Knowledge Collection.  Allows fine-grained control over who contributes data!

{% hint style="info" %}
**Knowledge collection(KC)** is a **collection of knowledge assets.** It refers to structured data that can be stored, shared, and validated within a distributed network.
{% endhint %}

#### Interacting with Miner Access Permissioned Paranet

Paranet Operator can add Miners to Permissioned Paranet

```javascript
await DkgClient.paranet.addParanetPermissionedMiners(paranetUAL, minerAddresses);
```

Paranet Operator can removes Miners from Permissioned Paranet

```javascript
await DkgClient.paranet.removeParanetPermissionedMiners(paranetUAL, minerAddresses);
```

### Combining policies

These two policies can be combined in any way:

| Node Access Policy | Miner Acces Policy | Result                                                                                                                             |
| ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| OPEN               | OPEN               | Any node can sync public part of KC from Paranet and any miner can add knowledge to Paranet                                        |
| OPEN               | PERMISSIONED       | Any node can sync public part of KC from Paranet and only selected miners can add knowledge to Paranet                             |
| PERMISSIONED       | OPEN               | Only selected nodes can sync  both private and public part of KC from paranet and any miner can add knowledge to Paranet           |
| PERMISSIONED       | PERMISSIONED       | Only selected nodes can sync  both private and public part of KC from parane and only selected miners can add knowledge to Paranet |

### Access policis and Knowledge Currations

These permisions will also interact with Staging Paranets. If a Paranet has PARANET\_KC\_SUBMISSION\_POLICY STAGING and  PERMISSIONED PARANET\_MINERS\_ACCESS\_POLICY only allowed knowledge miners can stage knowledge collections.



