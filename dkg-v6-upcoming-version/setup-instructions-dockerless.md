# Setup instructions (Dockerless)

{% hint style="info" %}
These setup instructions for DKGv6 are "Work in progress" and are subject to change. The development team expects to introduce improvements as well as a more automated process of setting up the DKGv6 node in the future.
{% endhint %}

{% hint style="success" %}
Need any assistance with node setup? Join the DKGv6 Discord chat and find help within the OriginTrail tech community!
{% endhint %}

{% hint style="warning" %}
**IMPORTANT: These instructions are not intended for migrating your current v5 node to v6. Attempting this will most likely break your v5 node at this point. You should only use these instructions in order to setup a fresh OriginTrail v6 testnet node.**
{% endhint %}

### Prerequisites <a href="#docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b" id="docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b"></a>

* A dedicated **4GB RAM/2CPUs** **Ubuntu** server (minimum hardware requirements)
* An installed and running **GraphDB**

**GraphDB installation process:**

In order to download GraphDB, please visit their [official website](https://www.ontotext.com/products/graphdb/graphdb-free/) and fill out a form. Installation files will be provided to you via email. Use the standalone version of GraphDB.\
Upload the **\<graphDB\_file>.zip** file to your server (e.g. using **scp** or some other way).

```
apt install default-jre
unzip graphdb-free-9.10.1-dist.zip
nohup ~/graphdb-free-9.10.1/bin/graphdb &
```

When graphDB is started, please check the **nohup.out** file that was generated in order to confirm that it is running in the background .\


### Installation steps

#### Step 1:

OriginTrail v6 node requires **npm** and **Node.js (v14)** or higher. In order to install them, please execute the following set of commands:

```
cd ~
curl -sL https://deb.nodesource.com/setup_14.x -o setup_14.sh
sudo sh ./setup_14.sh
sudo apt update
sudo apt install nodejs npm
```

Alternatively, you can use [**nvm**](https://www.npmjs.com/package/nvm) to manage your npm/nodejs version.

#### Step 2 - Install forever

```
npm install forever -g
```

#### Step 3 - Install **mysql** and create a local operational database

```
apt install tcllib
apt install mysql-server
service mysql start
mysql -u root  -e "CREATE DATABASE operationaldb /*\!40100 DEFAULT CHARACTER SET utf8 */;" 
mysql -u root -e "update mysql.user set plugin = 'mysql_native_password' where User='root';"
mysql -u root -e "flush privileges;"
```

#### Step 4 - Get the DKG code by cloning the  repo and checking out the proper branch

```
git clone https://github.com/OriginTrail/ot-node
cd ot-node
git checkout v6/release/testnet
```

#### Step 5 - Install dependencies

```
npm install
```

#### Step 6 - Run DB migrations

```
npx sequelize --config=./config/sequelizeConfig.js db:migrate
```

#### Step 7 - Allow traffic on ports 8900 (RPC) and 9000 (libp2p)

\
**Step 8 -** Create **.env** file:&#x20;

```
nano .env
```

Paste the following variable into the .**env** file, save and close:

```
NODE_ENV=testnet
```

**Step 9 -** Create **.origintrail\_noderc** file \
\
.**origintrail\_noderc** example can be found on our [GitHub](https://github.com/OriginTrail/ot-node/blob/v6/develop/.origintrail\_noderc\_example).\


{% hint style="info" %}
OriginTrail v6 testnet node is running on **Polygon Mumbai (testnet)** network **** and it is currently not requiring any test TRAC tokens. Make sure that the wallet you are using in your configuration file is funded with test MATIC tokens.
{% endhint %}

#### Polygon Mumbai MATIC faucet: [https://faucet.polygon.technology/](https://faucet.polygon.technology)

#### Step **10 -** Run DB migrations:

```
npx sequelize --config=./config/sequelizeConfig.js db:migrate
```

****\
**Step 11 - Start OriginTrail v6 node**\
****In order to start the node, execute the following command:

```
forever start -a -o out.log -e out.log index.js
```

**Checking node logs:**\
****In order to check if the node started successfully, you can access node logs byecuting the following command:

```
tail -f -n100 out.log
```

![Successfully started](<../.gitbook/assets/Screenshot 2021-12-27 at 15.49.28.png>)

In order to stop your node, use the following command:

```
forever stop index.js
```

****\
**Step 12 - Enable SSL (optional, but recommended):**\
Ensure that the following certificate files are in the right directory: **`/root/certs/privkey.pem`**` ``&`` `**`/root/certs/fullchain.pem`**



{% hint style="success" %}
**Congratulations. Welcome to v6 beta**
{% endhint %}

We would love to meet you in our Discord chat - join us [here](https://discord.gg/6BGSCJfk4Y).&#x20;
