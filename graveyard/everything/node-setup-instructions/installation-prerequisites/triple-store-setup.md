# Triple store setup

DKG nodes are designed to handle and store graph data using multiple triple store implementations. By supporting various triple stores, DKG nodes ensure flexibility, scalability, and robustness in managing knowledge assets. Currently, several triple store implementations are supported directly:

* [Ontotext GraphDB](https://www.ontotext.com/products/graphdb/)
* [Blazegraph](https://blazegraph.com/)
* [Apache Jena Fuseki](https://jena.apache.org/documentation/fuseki2/)

#### Ontotext GraphDB

To use Ontotext GraphDB with your DKG node, follow these steps:

1. **Visit the GraphDB website**: Go to the official [Ontotext GraphDB website](https://www.ontotext.com/products/graphdb/).
2. **Request and download GraphDB**: Follow the instructions to request and download the GraphDB software.
3. **Setup GraphDB on your server**: Install and configure GraphDB according to the provided guidelines.
4. **Modify your DKG node configuration**: Edit the configuration file of your DKG node to use GraphDB as the default triple store implementation.
   * Navigate to: [Broken link](broken-reference "mention")
   * Locate the `tripleStore` object and set the `defaultImplementation` to `ot-graphdb`.

#### Blazegraph

Blazegraph setup is streamlined with the OriginTrail Automatic Installer. Follow these steps:

1. **Run the OriginTrail Automatic Installer**: The installer will handle the setup and configuration of Blazegraph for you.
2. **Verify the configuration**: Ensure that your node's configuration file is correctly set to use Blazegraph as the triple store implementation.

#### Apache Jena Fuseki

Similar to Blazegraph, the setup for Apache Jena Fuseki is managed by the OriginTrail Automatic Installer. Here’s what you need to do:

1. **Run the OriginTrail Automatic Installer**: The installer will automatically set up and configure Fuseki.
2. **Verify the configuration**: Confirm that your node's configuration file is properly configured to use Fuseki.

#### Custom Triple Store Integrations

However due to the standard implementation (W3C RDF / SPARQL standards) it is easy to integrate DKG nodes with any standardized RDF triple store. While the above triple stores are directly supported, you can adapt your DKG node to work with other RDF triple store implementations by simple modifications of the code and the configuration settings.

