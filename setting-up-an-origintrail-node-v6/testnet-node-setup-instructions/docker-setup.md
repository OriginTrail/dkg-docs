---
description: Docker setup manual
---

# Docker setup

Below is a step-by-step guide for a docker based DKGv6 setup.

### Prerequisites <a href="#docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b" id="docs-internal-guid-e057adbf-7fff-9a68-2579-1fe11935388b"></a>

* A dedicated **4GB RAM/2CPUs/ 50GB HDD** Instance (minimum hardware requirements)
* Docker Engine and Docker-Compose installed

### Install docker.

For installation on Ubuntu based system, follow the official installation manual below:

{% embed url="https://docs.docker.com/engine/install/ubuntu" %}
Docker installation on for Ubuntu&#x20;
{% endembed %}

For installation on a Debian based system, follow the official installation manual via link below:

{% embed url="https://docs.docker.com/engine/install/debian" %}
Docker installation on Debian
{% endembed %}

For installation on a CentOS based system, follow the official documentation via link below:

{% embed url="https://docs.docker.com/engine/install/centos" %}
Docker installation on CentOS
{% endembed %}

For installation on a Windows based system, follow the official WSL installation documentation via link below:

{% embed url="https://docs.microsoft.com/en-us/windows/wsl/install" %}
WSL installation on Windows OS
{% endembed %}

{% hint style="info" %}
To setup DKGv6 on Windows based system, you need to install your preferred linux subsystem on windows. After installation login into the Linux Subsystem and proceed to install docker-engine & docker-compose.
{% endhint %}

### Setup the firewall

In order for DKGv6 to communicate and send telemetry metrics on the network, you need to open ports below through your firewall system.

\
For Linux based systems run:

```
 sudo ufw allow 8900 && ufw allow 9000
```

### Install Docker-Compose

With docker installed on the system, you can download and install Docker Compose. Follow the official docker-compose installation documentation for your respective OS via link below:

{% embed url="https://docs.docker.com/compose/install" %}
Docker-compose installation
{% endembed %}

### Setup and Clone Code Repo

After installation and configuration of docker with docker-compose, proceed and clone OT-Node Git Repo on to your system.&#x20;

```
cd ~
git clone -b v6/release/testnet https://github.com/OriginTrail/ot-node.git
```

{% hint style="info" %}
**Optional: Create certs folder at home directory**

You need to set up Certificates directory for OT-Node.

```
sudo mkdir ~/certs
```
{% endhint %}

#### Setup configuration file

Create a configuration file in your current directory with the appropriate Public & Private keys.

```
sudo nano ~/ot-node/.origintrail_noderc
```



Dockerized OriginTrail v6 node runs with **BlazeGraph** so please make sure that your configuration file has the correct parameters set under the **"graphDatabase"** section as shown in the example below:

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
    "127.0.0.1"
  ]
}
```

Additional information on the configuration file and the parameters can be found [here](https://docs.origintrail.io/setting-up-an-origintrail-node-v6/v6-configuration).

{% hint style="info" %}
To obtain the IP address of the Linux Subsytem on Windows follow the steps below:

* Obtain the IP address of your host machine by running this command from your Windows Linux distribution: `cat /etc/resolv.conf`
* Copy the IP address following the term: `nameserver`.
* Whitelist the IP address in .origintrail\_noderc
* To obtain the DKGv6 node IP address run command from WSL server (ip -4 addr show eth0) and access the node API with the return IP address.
{% endhint %}

### &#x20;Ubuntu based image build

From your git cloned directory, run the following to build and start Ubuntu based docker container.

```
docker-compose -f docker/docker-compose-ubuntu.yaml up
```

{% hint style="warning" %}
Always run docker-compose command from the cloned "**ot-node**" directory, so that docker-compose can mount .origintrail\_noderc file
{% endhint %}



### Ubuntu based image build

For Ubuntu based docker container **** use**:**

```
docker-compose -f docker/docker-compose-ubuntu-blazegraph.yaml up --detach
```

### Debian based image build

For Debian based docker container **** use**:**

```
docker-compose -f docker/docker-compose-debian-blazegraph.yaml up --detach
```

### Alpine based image build:

For Alpine based docker container **** use**:**

```
docker-compose -f docker/docker-compose-alpine-blazegraph.yaml up --detach
```

{% hint style="info" %}
1. **docker-compose** command will first pull and then start three containers (ot-node, mysql, BlazeGraph).
2. **--detach** will start docker containers as a background process
3. use "**docker logs -f ot-node**" command in order to see the node logs and confirm that your node is successfully started


{% endhint %}

{% hint style="success" %}
**Congratulations. Welcome to v6 beta!**
{% endhint %}
