# Querying data from the DKG

## Querying the data

### Decentralized Knowledge Graph querying - Network query

Querying the DKG is done using the network query API. It is used to look up all datasets containing a specific identifier \(such as a supply chain identifier, like a GS1 barcode or RFID value\).

The query request is an array values that identify a particular object in a dataset. These identifiers are sent as an array of objects, where the `path` parameter is the type of identifier \(such as ean13, sgtin, sgln, or id for general identifier\), `value` is the identifier value or an array of possible values, and `opcode` is either EQ or IN, depending on whether the queried object identifier needs to equal or belong to the given value parameter

```text
{
  "query": [
    {
      "path": "sgtin",
      "value": "urn:epc:id:sgtin:271119.100294475",
      "opcode": "EQ"
    },
    {
      "path": "urn:epcglobal:cbv:mda#bestBeforeDate",
      "value": ["20-09-2020","21-09-2020", "22-09-2020"],
      "opcode": "IN"
    }
  ]
}
```

The returned responses contain an array of datasets which contain objects whose identifiers fit the given query. This response can then be used to import a desired dataset on one’s node, which will enable querying the graph locally or exporting and viewing the dataset.

The network query API details are explained on the following link

[https://app.swaggerhub.com/apis-docs/otteam/ot-node-api/v2.0\#/network/post\_network\_query](https://app.swaggerhub.com/apis-docs/otteam/ot-node-api/v2.0#/network/post_network_query)

### Local Knowledge Graph querying - Graph Trail

#### Identifier types and values and trail depth

Querying the local knowledge graph performs a graph traversal starting from a particular vertex in the graph and traversing over the specified edge types.

The result of the trail represents all objects found on the trail \(the historical provenance trail spanning all datasets\), along with an array that indicates which datasets those objects belong to.

```text
{
  "identifier_types": [
    "ean13"
  ],
  "identifier_values": [
    "83213023"
  ],
  "depth": 5,
  "connection_types": [
    "EPC"
  ]
}
```

`identifier_types` and `identifier_values` are two arrays used to determine the starting object of the trail traversal. Note that these two arrays must be of the same length, and will be paired in the order they were given \(first element of the `identifier_types` array corresponds to the first element of the `identifier_values` array, etc\).

The `depth` parameter determines how far from the starting vertex will the traversal go. If the depth is set to 0 the traversal will return only the objects identified by the given parameters.

#### Connection types

`connection_types` is an array which serves as a filter in the graph trail traversal operation. When observing a vertex in the graph, only the vertices which are connected to the currently observed vertex by a relation type which is in the `connection_types` array will be visited and included in the graph.

[![../\_images/connection-example1.png](https://docs.origintrail.io/en/latest/_images/connection-example1.png)](https://docs.origintrail.io/en/latest/_images/connection-example1.png)

**Example**: In the graph pictured above, if the `connection_types` contained `rel_type_1` and not `rel_type_2`, a traversal starting from vertex **B** would return vertex **A** and would not return vertex **C**

In order to avoid backtracking in the trail and attaching superfluous information, a vertex will not be visited if the relation types on the path to that vertex are the same two times in a row.[![../\_images/connection-example2.png](https://docs.origintrail.io/en/latest/_images/connection-example2.png)](https://docs.origintrail.io/en/latest/_images/connection-example2.png)

**Example**: In the graph pictured above, if the `connection_types` contained `rel_type_1`, a traversal starting from vertex **A** would return vertex **B** and would not return vertex **C**

If the `connection_types` parameter is omitted, the entire graph is traversed \(to the specified depth\), without the backtracking prevention feature. It should be noted that the knowledge graph can be a highly dense graph, and traversing without filters can return extremely large results and might cause problems with node performance.

#### Reach parameter

Reach is an optional parameter that can be used to modify which objects are retrieved. When the `reach` parameter is specified as `extended` the node will execute the trail, then check which objects are referenced in the trail but are not included in it. These objects are then additionally retrieved from the local knowledge graph and appended to the trail response.

The default behaviour can be explicitly called by setting the `reach` parameter value to `narrow` .

The trail API details are explained on the following link

[https://app.swaggerhub.com/apis-docs/otteam/ot-node-api/v2.0\#/trail](https://app.swaggerhub.com/apis-docs/otteam/ot-node-api/v2.0#/trail)

