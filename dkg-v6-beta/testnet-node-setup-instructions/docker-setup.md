# Docker setup

{% hint style="info" %}
These setup instructions for DKGv6 are "Work in progress" and are subject to change. The development team expects to introduce improvements as well as a more automated process of setting up the DKGv6 node in the future.
{% endhint %}

{% hint style="success" %}
Need any assistance with node setup? Join the DKGv6 Discord chat and find help within the OriginTrail tech community!
{% endhint %}

{% hint style="warning" %}
**IMPORTANT: These instructions are not intended for migrating your current v5 node to v6. Attempting this will most likely break your v5 node at this point. You should only use these instructions in order to setup a fresh OriginTrail v6 testnet node.**
{% endhint %}

Below is a step-by-step guide for a docker based DKGv6 setup.

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
    "127.0.0.1"
  ]
}
```

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
docker-compose -f docker/docker-compose-ubuntu.yaml pull
docker-compose -f docker/docker-compose-ubuntu.yaml up
```

{% hint style="warning" %}
Always run docker-compose command from the cloned directory, so that docker-compose can mount .origintrail\_noderc file.
{% endhint %}

{% hint style="info" %}
Docker-compose will first pull and then start two containers (ot-node & graphdb).
{% endhint %}

### Debian based image build

From your git cloned directory, run the following to build and start Debian based docker container.

```
docker-compose -f docker/docker-compose-debian.yaml pull
docker-compose -f docker/docker-compose-debian.yaml up
```

### Alpine based image build

From your git cloned directory, run the following to build and start Alpine based docker container.

```
docker-compose -f docker/docker-compose-alpine.yaml pull
docker-compose -f docker/docker-compose-alpine.yaml up
```

{% hint style="info" %}
Docker-compose will first pull and then start three containers (ot-node, mysql, graphdb).
{% endhint %}

{% hint style="success" %}
**Congratulations. Welcome to v6 beta!**
{% endhint %}
