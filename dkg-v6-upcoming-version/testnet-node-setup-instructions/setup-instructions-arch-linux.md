# Setup instructions Arch Linux

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

* A dedicated **4GB RAM/2CPUs/50GB HDD** **Arch Linux** server (minimum hardware requirements)

## **Manual installation steps**

First, log in as root and update your system
```
pacman -Syu
```

#### **Prepare Databases**

**In this section and the one below, you can choose between using GraphDB or Blazegraph. If you choose one, you can ignore the instructions for the other.**

In order to download GraphDB, please visit their [official website](https://www.ontotext.com/products/graphdb/graphdb-free/) and fill out the form. Installation files will be provided to you via email. Use the standalone version of GraphDB.\
Save the **\<graphDB\_file>.zip** on your root folder.

In order to download blazegraph, run
```
wget https://github.com/blazegraph/database/releases/download/BLAZEGRAPH_2_1_6_RC/blazegraph.jar
```

#### **Step 0: Setup GraphDB or Blazegraph**
If you chose to use **GraphDB**, below are the steps to follow:
```
pacman -S jre-openjdk
unzip graphdb-free-9.10.1-dist.zip
```

We will create a system service to allow graphDB to keep running in the background.
```
nano /lib/systemd/system/graphdb.service
```
Paste the following content and save
```
#/lib/systemd/system/graphdb.service

[Unit]
Description=GraphDB - OriginTrail V6 Stage 1 Beta Node
Documentation=https://github.com/OriginTrail/ot-node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/graphdb-free-9.10.1/bin/
ExecStart=/root/graphdb-free-9.10.1/bin/graphdb
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Now let's start the service:
```
systemctl daemon-reload
systemctl start graphdb
```
If you chose to use **Blazegraph**, please follow the steps below:

We will create a system service to allow Blazegraph to keep running in the background.
```
nano /lib/systemd/system/blazegraph.service
```
Paste the following content and save
```
#/lib/systemd/system/blazegraph.service

[Unit]
Description=blazegraph - OriginTrail V6 Stage 1 Beta Node
Documentation=https://github.com/OriginTrail/ot-node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/
ExecStart=/bin/java -jar /root/blazegraph.jar
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Now let's start the service:
```
systemctl daemon-reload
systemctl start blazegraph
```
When graphDB or blazegraph are started, please check the status in order to confirm that it is running in the background. 
```
systemctl status graphdb
```
```
systemctl status blazegraph
```

#### **Step 1: Installing other requirements**

OriginTrail v6 node requires **npm** and **Node.js v14**. In order to install them, please execute the following set of commands:

```
pacman -S npm nodejs-lts-fermium
```

#### **Step 2 - Install **mysql** and create a local operational database**

For Arch Linux, MariaDB is a community-developed, commercially supported fork of the MySQL, intended to remain free and open-source software. It meets the same standard enterprise requirements as MySQL, often with additional features, capabilities and options, and shows an improved speed when compared. 

```
pacman -S tcl mariadb
mariadb-install-db --user=mysql --basedir=/usr --datadir=/var
systemctl start mariadb
mysql -u root -e "CREATE DATABASE operationaldb /*\!40100 DEFAULT CHARACTER SET utf8 */;" 
mysql -u root -e "ALTER USER root@localhost IDENTIFIED VIA mysql_native_password;"
mysql -u root -e "flush privileges;"
```

Disable binary logging in the mysql config file:

```
nano /etc/my.cnf.d/mysql-clients.cnf
```

Under the line that reads [mysqlbinlog], add the following line:

```
skip-log-bin
```

Close and save the file. Restart the service:&#x20;

```
systemctl restart mariadb
```

#### **Step 3 - Get the DKG code by cloning the  repo and checking out the proper branch**

```
git clone https://github.com/OriginTrail/ot-node
cd ot-node
git checkout v6/release/testnet
```

#### **Step 4 - Install dependencies**

```
npm install
```

#### **Step 5 - Ports**

Allow traffic on ports 8900 (RPC) and 9000 (libp2p) on your router. Note that all ports are open by default on Arch Linux.


#### **Step 6 - Create .env file:**

```
nano .env
```

Paste the following variable into the .**env** file, save and close:

```
NODE_ENV=testnet
```

**Step 7 -** Create **.origintrail\_noderc** file

Paste the content below if you are using **GraphDB**, then add your operational wallet public and private keys :
```
{
  "blockchain":[
    {
      "blockchainTitle": "Polygon",
      "networkId": "polygon::testnet",
      "rpcEndpoints": ["https://rpc-mumbai.maticvigil.com/"],
      "publicKey": "...",
      "privateKey": "..."
    }
  ],
  "graphDatabase": {
    "username": "admin",
    "password": ""
  },
  "logLevel": "trace",
  "rpcPort": 8900,
  "network": {
  },
  "ipWhitelist": [
  "::1",
    "127.0.0.1"
  ]
}
```
Paste the content below if you are using **Blazegraph**, then add your operational wallet public and private keys :
```
{
  "blockchain":[
    {
      "blockchainTitle": "Polygon",
      "networkId": "polygon::testnet",
      "rpcEndpoints": ["https://rpc-mumbai.maticvigil.com/"],
      "publicKey": "...",
      "privateKey": "..."
    }
  ],
  "graphDatabase": {
    "implementation": "Blazegraph",
    "url": "http://localhost:9999/blazegraph",
    "username": "admin",
    "password": ""
  },
  "logLevel": "trace",
  "rpcPort": 8900,
  "network": {
  },
  "ipWhitelist": [
  "::1",
    "127.0.0.1"
  ]
}
```
.**origintrail\_noderc** example can also be found on our [GitHub](https://github.com/OriginTrail/ot-node/blob/v6/develop/.origintrail\_noderc\_example).


{% hint style="info" %}
OriginTrail v6 testnet node is running on **Polygon Mumbai (testnet)** network **** and it is currently not requiring any test TRAC tokens. Make sure that the wallet you are using in your configuration file is funded with test MATIC tokens.
{% endhint %}

#### Polygon Mumbai MATIC faucet: [https://faucet.polygon.technology/](https://faucet.polygon.technology)

#### Step **8 -** Run DB migrations:

```
npx sequelize --config=./config/sequelizeConfig.js db:migrate
```

****\
**Step 9 - Start OriginTrail v6 node**\
****We will create a service to start the node:

```
nano /lib/systemd/system/otnode.service
```
Paste the following content and save
```
#/lib/systemd/system/otnode.service

[Unit]
Description=OriginTrail V6 Stage 1 Beta Node
Documentation=https://github.com/OriginTrail/ot-node/
After=network.target graphdb.service

[Service]
Type=simple
User=root
WorkingDirectory=/root/ot-node
ExecStart=/usr/bin/node /root/ot-node/index.js
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
```
systemctl daemon-reload
systemctl start otnode
```
Verify that the service is up and running:
```
systemctl status otnode
```

**Checking node logs:**\
****Use the following command to check the logs:

```
journalctl -f -u otnode --all
```

![Successfully started](<../.gitbook/assets/Screenshot 2021-12-27 at 15.49.28.png>)

In order to stop your node, use the following command:

```
systemctl stop otnode
```

### OPTIONAL: 
You can enable all previous services to allow them to start on reboot. Enable GraphDB or Blazegraph depending on your choice above.
```
systemctl enable graphdb
systemctl enable blazegraph
systemctl enable mariadb
systemctl enable otnode
```
To control your journal size over time, I strongly suggest running the following:
```
journalctl --vacuum-size=200M
```

{% hint style="success" %}
**Congratulations. Welcome to v6 beta**
{% endhint %}

We would love to meet you in our Discord chat - join us [here](https://discord.gg/6BGSCJfk4Y).&#x20;
