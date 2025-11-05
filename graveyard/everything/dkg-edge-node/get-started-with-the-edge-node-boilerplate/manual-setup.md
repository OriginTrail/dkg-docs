---
description: >-
  Setting up an Edge Node project to explore its capabilities and build your own
  projects. As an open-source solution, the Edge Node offers complete
  customization to fit your needs.
---

# Manual setup

To manually set up the DKG Edge Node in your local environment, you can choose between the following two options:

1. **\[Recommended]** [**Set up local Edge Node services with a local DKG network**](manual-setup.md#setup-with-a-local-dkg-network)
2. [**Configure local Edge Node services with a pre-deployed V8 DKG Core Testnet Node**](manual-setup.md#setup-with-pre-deployed-v8-dkg-runtime-testnet-node)

## Setup with a local DKG network \[Recommended]

This option allows you to configure the Edge Node services within your local development environment, utilizing a locally deployed DKG network. This setup provides full control over the environment and is ideal for developing custom processing pipelines and testing in a self-contained network.

### System Requirements

* **Operating System:** macOS, Linux
* **RAM:** At least 8 GB
* **CPU:** 4
* **Storage:** At least 20 GB of available space
* **Network:** Stable internet connection

### Software Dependencies

Make sure the following services are installed and properly configured:

* **Git:** Version control system
  * **Windows**: [Download Git for Windows](https://git-scm.com/download/win)
  * **Linux**: [Install Git on Linux](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) (via a package manager such as`sudo apt install git` for Ubuntu)
  * **macOS**: [Download Git for macOS](https://git-scm.com/download/mac)
* **MySQL 8:** Database service
  * **Windows**: [Download MySQL Installer for Windows](https://dev.mysql.com/downloads/installer/)
  * **Linux**: [Install MySQL on Linux](https://dev.mysql.com/doc/refman/8.0/en/linux-installation.html) (via `sudo apt install mysql-server` for Ubuntu)
  * **macOS**: [Download MySQL for macOS](https://dev.mysql.com/downloads/mysql/)
*   **Redis:** In-memory data structure store ([documentation](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/))

    * **Windows**: [Install Redis on Windows](https://github.com/microsoftarchive/redis/releases)
    * **Linux**:&#x20;

    ```
    sudo apt update
    sudo apt install redis-server
    ```

    * **macOS**:

    ```
    brew install redis
    ```
* **Node.js:** JavaScript runtime environment
  * **v20.04:** Used for the local network/ot-node setup
  * **v22.4.0:** Used for Edge Node services
* [**Java**](#user-content-fn-1)[^1] **v11:** for running Blazegraph triple store
* **Python** v3.11.7

{% hint style="info" %}
We recommend using NVM and Pyenv in order to be able to switch Node.js versions easily and install Python.
{% endhint %}

## Setup process

### **1 - Setting up local DKG network:**

Edge Node services require a V8 DKG Runtime Node endpoint in order to be configured and initialized so for this setup, running a local DKG network is essential.&#x20;

In order to deploy a local DKG network, do the following:

* Clone the OriginTrail node engine: `git clone https://github.com/OriginTrail/ot-node`&#x20;
* Enter **ot-node** directory and checkout to v8/develop branch: `cd ot-node && git checkout v8/develop`&#x20;
* Switch to Node.js v20 and install node modules: `npm install`&#x20;
* Download blazegraph.jar (Triple store db) from the following [link](https://github.com/blazegraph/database/releases/tag/BLAZEGRAPH_2_1_6_RC) and save it to the location of your choice locally
* Run blazegraph.jar file with the following command: `java -server -Xmx4g -jar blazegraph.jar` in order to start the triple store database (from the directory where Blazegraph is downloaded)
* Make sure that the MySQL service is running
* In ot-node directory, create .env file in ot-node directory and populate it with the following parameters (If your MySQL is password protected, add the password to REPOSITORY\_PASSWORD):

<pre class="language-bash"><code class="lang-bash">NODE_ENV=development
RPC_ENDPOINT_BC1=http://127.0.0.1:8545
RPC_ENDPOINT_BC2=http://127.0.0.1:9545
<strong>REPOSITORY_PASSWORD=
</strong></code></pre>

* Start the local DKG network by executing the following command from the ot-node directory: `bash tools/local-network-setup/setup-macos-environment.sh --nodes=5`&#x20;
* Once the network deployment is initiated, you will be provided with the local hardhat blockchain and the amount of local DKG nodes that you defined via **--nodes** flag

Once the network is up and running, you will select one of the local node endpoints to configure the Edge Node services, which will be explained in the continuation of these instructions.

### **2 - Cloning DKG Edge Node services:**

In order to kick off the installation process, you need to clone all Edge Node services to your local environment using **`git clone`** command.

1. [Authentication service](https://github.com/OriginTrail/edge-node-authentication-service)
2. [Edge Node API](https://github.com/OriginTrail/edge-node-api)
3. [Edge Node interface](https://github.com/OriginTrail/edge-node-interface)
4. [Knowledge mining API](https://github.com/OriginTrail/edge-node-knowledge-mining)
5. [dRAG](https://github.com/OriginTrail/edge-node-drag)

### **3 - Configuring DKG Edge Node services**

The instructions for configuring DKG Edge Node services are also available in the README file of each service's GitHub repository, where you can follow the steps provided.&#x20;

#### **3.1 Setup Edge Node Authentication Service:**

* Create database **'edge-node-auth-service'**
* Create .env file with `cp .env.example .env` in the dir.
* Generate random strings for the following .env variables:&#x20;
  * **JWT\_SECRET** and&#x20;
  * **SECRET** (you can use `openssl rand -hex 64` for example)
* Install node modules with `npm install`  (use Node.js  **v22.4.0**)
* Setup your database with `npx sequelize-cli db:migrate` and `npx sequelize-cli db:seed:all` - This will generate a demo user, a wallet with funds for the local network, and configure your local Edge Node Authentication Service to connect to the first node from your local network.
* Run the following MySQL query on **edge-node-auth-service** database: [UserConfig.sql](https://github.com/OriginTrail/edge-node-authentication-service/blob/main/UserConfig.sql)

{% hint style="info" %}
`seed` command will create an example user with the following credentials:

**username** `admin` and password `admin123`
{% endhint %}

* Initiate Edge Node Authentication service with: `npm run start`

#### **3.2 - Configuring Edge Node API** **service:**

1. Create .env file with `cp .env.example .env` in the service directory
2. Create the database mentioned in `.env`
3. Install node modules with `npm install` (use Node.js  **v22.4.0**)
4. Execute migrations: `npx sequelize-cli db:migrate`
5. Setup Runtime node MySQL operational db connection by populating the following values in the .env file:

```bash
RUNTIME_NODE_OPERATIONAL_DB_USERNAME=root
RUNTIME_NODE_OPERATIONAL_DB_PASSWORD=
RUNTIME_NODE_OPERATIONAL_DB_DATABASE=operationaldb0
RUNTIME_NODE_OPERATIONAL_DB_HOST=127.0.0.1
RUNTIME_NODE_OPERATIONAL_DB_DIALECT=mysql
```

{% hint style="info" %}
When your local DKG network is deployed, each of the local nodes will create its own operational database named **operationaldb0**, **operationaldb1**, **operationaldb2**, and so on, depending on the size of your local network.
{% endhint %}

7. Initialize Redis and make sure that it's running on its default port 6379
8. Start the service: `npm run start`

#### **3.3 - Configuring Edge Node UI:**

In order to set up the Edge Node UI locally, please run the following commands:

* Create .env file: `cp .env.example .env`&#x20;
* Install ionic/cli: `npm install -g @ionic/cli`&#x20;
* Install electron: `npm install -g electron`&#x20;
* Install node modules: `npm install` (use Node.js  **v22.4.0**)
* To run the application in your browser: `ionic serve`
* To run the application in your desktop app: `npm run start-electron`&#x20;

Once the Edge Node UI is ready, the only accessible screen will be **/login**. Use the credentials created during the Auth service setup previously.

#### **3.4 - Configuring Edge Node Knowledge Mining:**

In order to setup Edge Node UI locally, please follow the steps below:

* Create .env file with `cp .env.example .env` in the dir.
* Add the absolute path to your DAGs folder into the `DAG_FOLDER_NAME` variable in the `.env` file
* Setup Python environment: `pyenv local 3.11.7`

{% hint style="info" %}
It's recommended to use pyenv and install Python 3.11 locally within the app's directory to avoid conflicts with other Python versions on your machine.
{% endhint %}

* A virtual environment should be set up to install the required dependencies. You can do this by running the following command: `python -m venv .venv && source .venv/bin/activate`&#x20;
* Install Python requirements: `pip install -r requirements.txt`&#x20;
* Setup Apache Airflow service:&#x20;

{% hint style="info" %}
Airflow pipelines are an integral part of the Knowledge Mining Service, used to create automated data processing workflows. The primary purpose of these pipelines is to generate content for Knowledge Assets based on input files.
{% endhint %}

* Generate default Airflow config: `airflow config list --defaults`&#x20;
* Open the Airflow configuration file located at "\~/**airflow/airflow.cfg"** file and update the following parameters as presented below:

```bash
load_examples = False
dags_folder = YOUR_PATH_TO/edge-node-knowledge-mining/dags
parallelism = 32
max_active_tasks_per_dag = 16
max_active_runs_per_dag = 16
enable_xcom_pickling = True
```

* Initiate Airflow database and create an admin user with:

```bash
airflow db init
airflow users  create --role Admin --username admin --email admin --firstname admin --lastname admin --password admin
```

* Initiate Airflow scheduler: `airflow scheduler`&#x20;
* Pick up new jobs and start them:

```bash
airflow dags unpause exampleDAG
airflow dags unpause pdf_to_jsonld
airflow dags unpause simple_json_to_jsonld
```

* Initiate Airflow webserver: `airflow webserver --port 8080`&#x20;
* Once the Airflow webserver is initiated, your pipelines should be available on [http://localhost:8080/home](http://localhost:8080/home)&#x20;
* Initiate Edge Node Knowledge Mining: `python app.py`&#x20;

{% hint style="info" %}
`airflow scheduler, airflow webserver` and `python app.py`  should be initiated in parallel inside the virtual environment (use separated terminal windows to run them).
{% endhint %}

* Create MySQL logging: ``CREATE DATABASE `ka-mining-api-logging` CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;``&#x20;

Edge Node Knowledge Mining README is available [here](https://github.com/OriginTrail/edge-node-knowledge-mining).

#### **3.5 - Configuring Edge Node dRAG:**

In order to set up the Edge Node dRAG locally, please follow the steps below:

* Install node modules: `npm install` (use Node.js  **v22.4.0**)
* Create .env file: `cp .env.example .env`&#x20;
* Add your LLM\_API\_KEY  into the .env (dRAG uses LLM to formulate the answer)
* Create a database for dRAG logging: `CREATE DATABASE drag_logging;`&#x20;
* Run migrations: `npx sequelize-cli db:migrate`&#x20;
* Initiate the service: `npm run start`&#x20;

(Optional) If you want to use the vectorization controller, you have to set up the following services: HuggingFace, Zilliz, and Cohere. If you want to customize the experience further, you can also modify the code to use any other service for embedding/vector search and reranking.

* HuggingFace - used for vectorization embedding model [https://huggingface.co/](https://huggingface.co/)
* Zilliz - used for hosting the vector database [https://cloud.zilliz.com/](https://cloud.zilliz.com/)
* Cohere ReRanker - used for improving retrieval results accuracy [https://dashboard.cohere.com/](https://dashboard.cohere.com/)



Once you've finalized configuring all DKG Edge Node services, please make sure that they are exposed on the following ports:

* **Edge Node Authentication Service:** [http://localhost:3001](http://localhost:3001)
* **Edge Node API:** [http://localhost:3002](http://localhost:3002)
* **Edge Node UI:** [http://localhost:5173](http://localhost:5173)
* **Edge Node Knowledge Mining:** [http://localhost:5005](http://localhost:5005)
* **Edge Node dRAG:** [http://localhost:5002](http://localhost:5002)



## Setup with pre-deployed V8 DKG Runtime Testnet Node

{% hint style="warning" %}
Prior to proceeding with this setup option, it is essential to have a V8 DKG Core Node operational on the testnet, as this is a critical requirement. If you have not yet deployed a Testnet Core Node, please consult the installation guide available on the following [page](https://docs.origintrail.io/dkg-v8-upcoming-version/run-a-v8-core-node-on-testnet) for detailed instructions.
{% endhint %}

### System Requirements

* **Operating System:** macOS, Linux, Windows with WSL
* **RAM:** At least 8 GB
* **CPU:** 4
* **Storage:** At least 20 GB available space
* **Network:** Stable internet connection

### Software Dependencies

Make sure the following services are installed and properly configured:

* **Git:** Version control system
* **MySQL 8:** Database service
* **Redis:** In-memory data structure store ([documentation](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/))
* **Node.js v22.4.0:** JavaScript runtime environment
* **Python** v3.11.7

{% hint style="info" %}
We recommend using NVM and Pyenv in order to be able to switch Node.js versions easily and install Python.
{% endhint %}

## **Setup process:**

### **1 - Cloning DKG Edge Node services:**

In order to kick off the installation process, you need to clone all Edge Node services to your local environment using **`git clone`** command.

1. [Authentication service](https://github.com/OriginTrail/edge-node-authentication-service)
2. [Edge Node API](https://github.com/OriginTrail/edge-node-api)
3. [Edge Node interface](https://github.com/OriginTrail/edge-node-interface)
4. [Knowledge mining API](https://github.com/OriginTrail/edge-node-knowledge-mining)
5. [dRAG](https://github.com/OriginTrail/edge-node-drag)

### **2 - Whitelisting your local IP on the pre-deployed V8 DKG Runtime Node:**

* SSH to the server where you have your V8 DKG Core Node up and running
* Edit .origintrail\_noderc configuration file with `nano` or any other editor
* Locate the `auth` section in the configuration file and add your local IP as presented below:

```json
    "auth": {
        "ipWhitelist": [
            "::1",
            "127.0.0.1",
            "<your_local_ip_address>"
        ]
    }
```

* Restart your node with **`otnode-restart`** command in order for changes to configuration to be applied

### **3 - Configuring DKG Edge Node services**

The instructions for configuring DKG Edge Node services are also available in the README file of each service's GitHub repository, where you can follow the steps provided.&#x20;

#### **3.1 Setup Edge Node Authentication Service:**

* Create database **'edge-node-auth-service'**
* Create .env file with `cp .env.example .env` in the dir.
* Generate random strings for the following .env variables:&#x20;
  * **JWT\_SECRET** and&#x20;
  * **SECRET** (you can use `openssl rand -hex 64` for example)
* Install node modules with `npm install`  (use Node.js  **v22.4.0**)
* Setup your database with `npx sequelize-cli db:migrate` and `npx sequelize-cli db:seed:all` - This will generate a demo user, a wallet with funds for the local network, and configure your local Edge Node Authentication Service to connect to the first node from your local network.

{% hint style="info" %}
`seed` command will create an example user with the following credentials:

**username** `admin` and password `admin123`
{% endhint %}

* Run the following MySQL query on **edge-node-auth-service** database: [UserConfig.sql](https://github.com/OriginTrail/edge-node-authentication-service/blob/main/UserConfig.sql)
* Since the node is by default configured to automatically work with your local network, the following variables inside of the **UserConfigs** table (database: edge-node-auth-service) should be updated to match your pre-deployed V8 DKG Runtime Node information:
  * "**run\_time\_node\_endpoint**": http://\<your\_node\_endpoint\_or\_ip>
  * "**run\_time\_node\_port**": 8900
  * "**edge\_node\_environment**": testnet
  * "**blockchain**": base:84532
* Replace placeholder wallet - The following table "**user\_wallets**" will be populated with a pre-defined wallet address (local network related) which should be replaced by your Base Sepolia wallet with funds (ETH and TRAC)

{% hint style="info" %}
Instructions on how to use the TRAC faucet can be found [here](../../../../dkg-knowledge-hub/useful-resources/test-token-faucet.md).
{% endhint %}

* Initiate Edge Node Authentication Service with: `npm run start`

#### **3.2 - Configuring Edge Node API** S**ervice:**

1. Create .env file with `cp .env.example .env` in the service directory
2. Create the database mentioned in `.env`
3. Install node modules with `npm install` (use Node.js  **v23**)
4. Execute migrations: `npx sequelize-cli db:migrate`
5. Expose V8 DKG Core node operational database (MySQL) to a local Edge Node API service:
   * SSH to your Runtime Node server
   * Expose port 3306 on your server to your local IP address (firewall configuration)
   * Enable MySQL remote connection by changing the bind-address from **127.0.0.0** to **0.0.0.0** in `/etc/mysql/mysql.conf.d/mysqld.cnf`&#x20;
   * Restart mysql.service: `systemctl restart mysql.service`
   * Create new MySQL user for Edge Node API service to use:
     * mysql -u root -p
     * When asked for the password, use the password you created during the node setup process
     * Create a user for remote access: CREATE USER'**username**'@'%' IDENTIFIED BY'**your\_password**';
     * GRANT ALL PRIVILEGES ON\*.\*TO'**username**'@'%'WITH GRANT OPTION;
     * FLUSH PRIVILEGES;
   *   Setup Runtime Node MySQL operational db connection by populating the following values in the .env file:

       ```bash
       RUNTIME_NODE_OPERATIONAL_DB_USERNAME=root
       RUNTIME_NODE_OPERATIONAL_DB_PASSWORD=<runtime_node_operationaldb_password>
       RUNTIME_NODE_OPERATIONAL_DB_DATABASE=operationaldb
       RUNTIME_NODE_OPERATIONAL_DB_HOST=<endpoint/ip_of_your_runtime_node>
       RUNTIME_NODE_OPERATIONAL_DB_DIALECT=mysql
       ```
6. Initialize Redis and make sure that it's running on its default port **6379**
7. Start the service: `npm run start`

#### **3.3 - Configuring Edge Node UI:**

In order to set up the Edge Node UI locally, please run the following commands:

* Create .env file: `cp .env.example .env`&#x20;
* Install ionic/cli: `npm install -g @ionic/cli`&#x20;
* Install electron: `npm install -g electron`&#x20;
* Install node modules: `npm install` (use Node.js  **v23**)
* To run the application in your browser: `ionic serve`
* To run the application in your desktop app: `npm run start-electron`

Once the Edge Node UI is ready, the only accessible screen will be **/login**. Use the credentials created during the Auth Service setup previously.



#### **3.4 - Configuring Edge Node Knowledge Mining:**

In order to setup Edge Node UI locally, please follow the steps below:

* Create .env file with `cp .env.example .env` in the dir.
* Add the absolute path to your DAGs folder into the `DAG_FOLDER_NAME` variable in the `.env` file
* Setup Python environment: `pyenv local 3.11.7`

{% hint style="info" %}
It's recommended to use pyenv and install Python 3.11 locally within the app's directory to avoid conflicts with other Python versions on your machine.
{% endhint %}

* A virtual environment should be set up to install the required dependencies. You can do this by running the following command: `python -m venv .venv && source .venv/bin/activate`&#x20;
* Install Python requirements: `pip install -r requirements.txt`&#x20;
* Setup Apache Airflow service:&#x20;

{% hint style="info" %}
Airflow pipelines are an integral part of the Knowledge Mining service, used to create automated data processing workflows. The primary purpose of these pipelines is to generate content for Knowledge Assets based on input files.
{% endhint %}

* Generate default Airflow config: `airflow config list --defaults`&#x20;
* Open the Airflow configuration file located at "\~/**airflow/airflow.cfg"** file and update the following parameters as presented below:

```bash
load_examples = False
dags_folder = YOUR_PATH_TO/edge-node-knowledge-mining/dags
parallelism = 32
max_active_tasks_per_dag = 16
max_active_runs_per_dag = 16
enable_xcom_pickling = True
```

* Initiate Airflow database and create an admin user with:

```bash
airflow db init
airflow users  create --role Admin --username admin --email admin --firstname admin --lastname admin --password admin
```

* Initiate Airflow scheduler: `airflow scheduler`&#x20;
* Pick up new jobs and start them:

```
airflow dags unpause exampleDAG
airflow dags unpause pdf_to_jsonld
airflow dags unpause simple_json_to_jsonld
```

* Initiate Airflow webserver: `airflow webserver --port 8080`&#x20;
* Once the Airflow webserver is initiated, your pipelines should be available on [http://localhost:8080/home](http://localhost:8080/home)&#x20;
* Initiate Edge Node Knowledge Mining: `python app.py`&#x20;

{% hint style="info" %}
`airflow scheduler, airflow webserver` and `python app.py`  should be initiated in parallel inside the virtual environment (use separated terminal windows to run them).
{% endhint %}

* Create MySQL logging: ``CREATE DATABASE `ka-mining-api-logging` CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;``&#x20;

#### **3.5 - Configuring Edge Node dRAG:**

In order to set up Edge Node dRAG locally, please follow the steps below:

* Install node modules: `npm install` (use Node.js  **v22.4.0**)
* Create .env file: `cp .env.example .env`&#x20;
* Add your LLM\_API\_KEY  into the .env (dRAG uses LLM to formulate the answer)
* Create a database for dRAG logging: `CREATE DATABASE drag_logging;`&#x20;
* Run migrations: `npx sequelize-cli db:migrate`&#x20;
* Initiate the service: `npm run start`&#x20;

**(Optional)** In case you want to use the vectorization controller, you have to set up the following services: HuggingFace, Zilliz, and Cohere. If you want to customize the experience further, you can also modify the code to use any other service for embedding/vector search and reranking.

* HuggingFace - used for vectorization embedding model [https://huggingface.co/](https://huggingface.co/)
* Zilliz - used for hosting the vector database [https://cloud.zilliz.com/](https://cloud.zilliz.com/)
* Cohere ReRanker - used for improving retrieval results accuracy [https://dashboard.cohere.com/](https://dashboard.cohere.com/)



Once you've finalized configuring all DKG Edge Node services, please make sure that they are exposed on the following ports:

* **Edge Node Authentication Service:** [http://localhost:3001](http://localhost:3001)
* **Edge Node API:** [http://localhost:3002](http://localhost:3002)
* **Edge Node UI:** [http://localhost:5173](http://localhost:5173)
* **Edge Node Knowledge Mining:** [http://localhost:5005](http://localhost:5005)
* **Edge Node dRAG:** [http://localhost:5002](http://localhost:5002)

[^1]: 
