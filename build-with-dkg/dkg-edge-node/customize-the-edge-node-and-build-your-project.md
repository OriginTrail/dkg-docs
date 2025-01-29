# Customize the Edge node & Build your project

Now that you've set up the boilerplate project with all the essential components, it's time to explore the customization options. Each service in the app - Interface, API, Knowledge mining API, DRAG API, and Authentication service — is **open** **source** and **fully** **customizable**. You can fork any of these repositories to modify them to better suit your specific requirements.

This section will focus primarily on customizing the **Knowledge mining API** and **DRAG API**, two core services that empower you to process data and build decentralized Retrieval-Augmented Generations (dRAGs) based on Knowledge assets.

## Introduction to customization

Each service is hosted in a separate GitHub repository, enabling you to fork the code, make your changes, and deploy your customized versions. The default setup provides a boilerplate project with out-of-the-box functionality, serving as a solid foundation for customization.

Before diving into how you can customize Edge node services, it's important to highlight the role of the Authentication service, which acts as the connecting hub between all components. This service manages the `UserConfig` data, including both required and optional parameters that are shared across all services to ensure the system functions cohesively.

Users can add custom variables to the `UserConfig` table, making them accessible across all services. For instance, if a use case requires an external tool with an authentication key, the `UserConfig` table is the ideal place to store this key, ensuring that the variable is available to all services in the system.

## Common customization scenarios

### Creating a custom Knowledge mining pipeline

The **Knowledge mining API** is one of the most powerful services in the Edge node, offering builders the flexibility to create custom processing pipelines without limitations. Registering new pipelines is straightforward, and the service is built in Python, a versatile environment well-suited for **data** **processing**, **AI** **tools**, **models**, and more. It’s up to the builder to decide how to parse the input data from incoming requests. The only requirement is that the pipeline outputs data in JSON-LD format, as this is necessary for publishing it as a Knowledge asset on the DKG.

* **Forking the Repository**
  * Start by **forking** the Knowledge mining API repository from GitHub. This creates a copy of the original repository under your GitHub account, which you can modify as needed.
  *   Clone your forked repository locally:

      ```bash
      git clone https://github.com/your-username/edge-node-knowledge-mining.git
      ```
* **Creating your pipeline**
  * To create a new processing pipeline, add a new file in the "dags" folder of your project.
  * As a starting point, you can use the existing example file `dags/exampleDAG.py`. Duplicate this file and modify it as needed:
    * The example pipeline serves as a basic illustration. It performs two tasks:
      * Extracting parameters from the incoming request.
      * Converting the input file to JSON-LD format.
* **Building the pipeline**
  * There are no limitations on how you build your pipeline. You can:
    * Install additional packages as needed.
    * Use external APIs for data enrichment.
    * Incorporate any processing logic to transform incoming data into the required graph structure (JSON-LD).
  * **Requirement:** The pipeline must output data in JSON-LD format (in the same format as existing mining pipelines) so that the Edge node API can process it and pass it to the Publish service for creating a Knowledge asset on the DKG
* **Starting the pipeline**
  * **Restart the services** - After creating the pipeline (DAG), Edge node Knowledge mining API should be restarted
    * _python app.py_ and _airflow scheduler_ (scripts mentioned in previous chapter, required to be running in order to use the Knowledge mining service)
    * optionally: If _airflow webserver_ is used, it should also be restarted
  * **Unpause** your pipeline\
    `airflow dags unpause ${YOUR_DAG_NAME}`\
    &#xNAN;_&#x65;.g. If your pipeline filename is xlsx\_to\_jsonld.py, unpause command should be "airflow tags unpause xlsx\_to\_jsonld"_\
    \
    **NOTE:** If you are using airflow webserver, you should be able to see your pipeline on http://localhost:8080 (or any other port you selected for the service) inside of "unpaused DAGS"
* **Registering the pipeline**
  * In order for Edge node to **recognize** and **use** your new pipeline for certain filetypes, it needs to be registered in your main **UserConfig** **table** inside of Authentication service MYSQL DB (edge-node-auth-service)
  * By default Edge node will offer three variables for three main file types
    * _kmining\_json\_pipeline\_id_ - this pipeline will be used when input file MIME type is detected as **"application/json"**
    * _kmining\_pdf\_pipeline\_id_ - this pipeline will be used when input file MIME type is detected as **"application/pdf"**
    * _kmining\_csv\_pipeline\_id_ - this pipeline will be used when input file MIME type is detected as **"text/csv"**
  * If your pipeline handles one of the above file types, simply replace the default pipeline with your custom one. **Here are some ideas:**
    * **Convert Science Paper PDFs to JSON-LD Using a Bibliographic Ontology**\
      Extract metadata from science paper PDFs, such as title, authors, publication date, and references, and convert the data into JSON-LD following a bibliographic ontology like BIBO. This allows for structured, machine-readable representation of academic papers for easier citation management and searchability.
    * **Convert Supply Chain Excel Documents to JSON-LD Using GS1 Standard Ontology**\
      Parse supply chain-related data from Excel files (e.g., product lists, inventory records) and convert it into JSON-LD using the GS1 standard ontology.&#x20;
    * **Convert Images to JSON-LD Using OCR**\
      Use Optical Character Recognition (OCR) to extract text and metadata from image files and represent it as JSON-LD.&#x20;
    * **Convert Videos to Knowledge Assets by Transcribing the Audio and Extracting Key Points**\
      Transcribe the audio from videos and extract key points or insights, then represent this information as JSON-LD knowledge assets.&#x20;
  * If you need to support a different file type:
    * Create a new variable for the file type, e.g., `kmining_xlsx_pipeline_id`
    * adapt the code in [Edge node API - kMiningService](https://github.com/OriginTrail/edge-node-api/blob/main/services/kMiningService.js) to handle the new variable based on the input file's MIME type
* You should now be ready to test your setup. Visit the Edge node interface, go to the "Contribute" page, import a file, and verify that the pipeline processes it correctly.

### Creating a custom DRAG pipeline

Now that you have created your processing pipelines and published Knowledge assets on the DKG, you can customize the DRAG (Decentralized Retrieval-Augmented Generation) service to build your own decentralized RAGs. The DRAG service is built in Node.js, providing a flexible environment that supports integrations with LLMs, AI tools, and more, giving you limitless possibilities to customize your RAGs.

The native query language for interacting with the DKG is SPARQL, as we use a triple store for data storage. You can combine SPARQL, LLMs, vector databases, or other tools to extract and process data from the DKG, refine the results, and deliver answers to natural language questions. The DRAG service functions like any other RAG, but with the added benefits of decentralized data sources from the DKG.

* **Forking the Repository**
  * Start by **forking** the DRAG API repository from GitHub. This creates a copy of the original repository under your GitHub account, which you can modify as needed.
  *   Clone your forked repository locally:

      ```bash
      git clone https://github.com/your-username/edge-node-drag.git
      ```
* **Creating your DRAG**
  * App currently contains two DRAGs as demonstration how NL question can be understood, processed and answered using SPARQL and Vector similarity search
  * Creating a new DRAG is basically creating a new API route in the app and those steps are recommended but not mandatory: \
    NOTE: (_you can create your own path as long as they are compatible with Edge node interface, which also can be customized by your needs_)
    * Create new Controller in controllers directory
    * Create your DRAG method in Controller
    * Register route in route.js using created Controller and DRAG method
* **Building a new DRAG**
  * The DRAG service is highly customizable and supports various tools and libraries that can help you extract meaningful insights from the DKG. You can:
    * Combine SPARQL queries with AI-powered analysis tools to answer complex natural language questions.
    * Use LLMs for text generation or summarization based on the retrieved data.
    * Integrate vector databases to enhance search capabilities with similarity search or semantic search.
  * **Requirement:** Current version of Edge node interface works with defined response that you can see in two provided examples. It contains two parameters in response:
    * **Answer** - NL answer on defined questions
    * **Knowledge assets -** this will be use to show based on which Knowledge assets answer is created\
      NOTE: As mentioned earlier, you can fork and update [Edge node Interface](https://github.com/OriginTrail/edge-node-interface) as well and adapt the responses of your DRAGs to be compatible with adapted Interface
* **Integration with Interface**
  * As mentioned earlier, the AI Assistant is available in the current version of the Edge node interface. To connect your DRAG with the interface, all you need to do is update the route used for fetching answers.
* **Potential DRAG ideas:**
  * **Teach an LLM to Convert Natural Language to SPARQL:** Leverage few-shot learning to train an LLM to convert natural language queries into SPARQL, tailored to your specific ontology and data model. Provide a set of example queries and responses to guide the model's understanding. (Example: `exampleSparqlController.js`)
  * **Integrate Vector Search with Reranking for Precision:** Use a vector database to retrieve content similar to the user's question, then refine the results with AI-based reranking tools to improve relevance and accuracy. This can enhance both the speed and precision of the search. (Example: `exampleVectorController.js`)
  * **Intent-Matching AI for Predefined SPARQL Queries:** Create a set of predefined SPARQL queries and use an intent-matching algorithm powered by AI to map user queries to the most relevant SPARQL queries. This allows for efficient querying with minimal overhead.
  * **Feedback-Loop-Based SPARQL Refinement:** Combine the LLM's natural language to SPARQL conversion with a feedback loop where the AI iteratively enhances the generated SPARQL queries, ensuring they align with the ontology and avoid errors.
  * **Hybrid Search: Combine Vector and Symbolic Search:** Use a hybrid approach where both vector search (for semantic similarity) and symbolic search (e.g., SPARQL) work in tandem. This can help ensure both accuracy and broad coverage by balancing structured queries with open-ended search results.
  * **Ontology-aware LLM fine tuning:** Create a system to fine-tune a large language model (LLM) specifically on a given ontology. This approach involves providing the LLM with structured data from the ontology, including relationships, entities, and definitions, so it can learn to generate responses that align with the specific concepts and rules of the ontology. Then use the trained model to formulate SPARQL queries based on the natural language ones.
* You should now be ready to test your setup. Visit the Edge node interface, go to the "AI Assistant" page, ask a question and verify that your DRAG is being able to answer it based on your custom logic.\


### Customizing other services

Since all services are open source, you have the freedom to customize any component to suit your specific needs, and contributions are highly encouraged! For example, if you need to implement a new authentication mechanism, you can add it directly to the Authentication service and seamlessly integrate it across the other components.

The open-source nature not only allows you to tailor the system to your requirements but also gives you the opportunity to share your improvements with the community, potentially influencing future features and enhancing the Edge node ecosystem. Whether you're adding new functionality, optimizing existing features, or experimenting with innovative integrations, your contributions can help drive the evolution of the platform.

