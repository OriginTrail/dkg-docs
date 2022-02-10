---
description: How to setup a Windows development environment
---

# Setting up your Windows development environment

{% hint style="info" %} These setup instructions for DKGv6 are "Work in progress" and are subject to change. The development team expects to introduce improvements of setting up the DKGv6 node in local environment in the future. {% endhint %}

{% hint style="success" %} Need any assistance with node setup? Join the DKGv6 Discord chat and find help within the OriginTrail tech community! {% endhint %}

### Prerequisites

- Windows 10 or higher.
- The free GraphDB distribution zip. Please visit their [official website](https://www.ontotext.com/products/graphdb/graphdb-free/) and fill out a form. Installation files will be provided to you via email.

## 1. Development Environment Setup

{% hint style="info" %} The recommended approach for developing on Windows, is to do so using the **Windows Subsystem for Linux (WSL)**.

**WSL** allows you to run a GNU/Linux environment directly on Windows, without the need of a traditional virtual machine or dual-boot steup. {% endhint %}

#### Step 1.1 (Optional recommendation) - Install the latest version of Windows Terminal https://github.com/microsoft/terminal
Use this over something like *PowerShell*, for a more enjoyable command-line experience.

#### Step 1.2 - Install WSL 

Follow the guide https://docs.microsoft.com/en-us/windows/wsl/install to install WSL 2 with the default distribution of **Ubuntu-20.04**.

Useful commands:
- `wsl --list` - get list of installed distributions.
- `wsl --install -d Ubuntu-20.04` - install and set Ubuntu-20.04 as the default distribution.

#### Step 1.3 - Open a session as **root** in your linux environment 
```
wsl -u root
```

#### Step 1.4 - Update and upgrade packages 
```
apt update && apt upgrade
```

#### Step 1.5 - Install nvm, node.js, and npm
Following the installation guide for WSL at https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl.

#### Step 1.6 - Install Git
Install Git on the Ubuntu environment with:
```
apt-get install git
```
{% hint style="info" %} See https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-git for a more detailed installation guide and configuration setup. {% endhint %}

#### Step 1.7 - Install MySQL and create database:
```
apt install tcllib
apt install mysql-server
service mysql start

mysql -u root  -e "CREATE DATABASE operationaldb /*\!40100 DEFAULT CHARACTER SET utf8 */;" 
mysql -u root -e "update mysql.user set plugin = 'mysql_native_password' where User='root';"
mysql -u root -e "flush privileges;"
```

#### Step 1.8 - Start GraphDB:
Copy the GraphDB zip into your Ubuntu root directory, i.e.: `\\wsl$\Ubuntu-20.04\root`.

Run the following commands to unzip and start GraphDB:
```
apt install default-jre
unzip graphdb-free-9.10.1-dist.zip
nohup ~/graphdb-free-9.10.1/bin/graphdb &
```

{% hint style="info" %} `default-jre` is the Java Runtime Environment, required for running GraphDB. {% endhint %}

#### Step 1.9 (Optional recommendation) - Install Visual Studio Code

Install VS Code and the Remote WSL extension: https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode 

This IDE provides seemless integration with WSL, allowing you to develop and debug against code running in WSL from the Windows host.

{% hint style="success" %} You are now ready to clone the OriginTrail repository and start developing. {% endhint %}

## 2. Setting up OT-Node for Development

Making sure you are in your Ubuntu environment as **root**.

#### Step 2.1 - Get the DKG code by cloning the  repo and checking out the development branch:
```
git clone https://github.com/OriginTrail/ot-node
cd ot-node
git checkout v6/develop
```

#### Step 2.2 - Create **.env** file the ot-node root folder and add public and private keys for blockchain:
```
NODE_ENV=development
PUBLIC_KEY=<insert_here>
PRIVATE_KEY=<insert_here>
```

{% hint style="info" %}
OriginTrail v6 development node is running on **Polygon Mumbai (testnet)** network **** and it is currently not requiring any test TRAC tokens. Make sure that the wallet you are using in your configuration file is funded with test MATIC tokens.
{% endhint %}

#### Polygon Mumbai MATIC faucet: [https://faucet.polygon.technology/](https://faucet.polygon.technology)

#### Step 2.3 - Run DB migrations:
```
npx sequelize --config=./config/sequelizeConfig.js db:migrate
```

#### Step 2.4 - Start OriginTrail v6 node
In order to start the node, execute the following command:
```
node index.js
```
![Successfully started](<../.gitbook/assets/Screen Shot 2022-01-19 at 12.32.39.png>)

### API access from the Windows host
If you are wanting to send API requests to your node from outside of WSL (e.g. Using Postman), you will have to configure your node to allow requests from your host IP. This is done using the node configuration **ipWhitelist**.

- Obtain the IP address of your host machine by running this command from your Linux distribution: `cat /etc/resolv.conf`
- Copy the IP address following the term: `nameserver`, and add it to the ipWhitelist in the `/ot-node/.origintrail_nodeerc` file, as shown below:

```json
{
    ...
    "ipWhitelist": [
        "127.0.0.1",
        "::1",
        "172.17.112.1"
    ]
}

```
### Issues and Workarounds
1. #### Localhost API access fails to connect
   In some instances, host access to your node will not work using `localhost` and so the IP address of the Linux Host VM is required. From within your WSL distribution (ie Ubuntu), run the command: 
    ```
    ip addr
    ``` 
    Making note of the IP under the `inet` value of the `eth0` interface.

    You can now use this IP address to access your node APIs.