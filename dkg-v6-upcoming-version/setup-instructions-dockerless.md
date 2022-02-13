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

* A dedicated **4GB RAM/2CPUs/50GB HDD** **Ubuntu** server (minimum hardware requirements)
* An installed and running **GraphDB**

**Prepare GraphDB**

1. Please visit their [official website](https://www.ontotext.com/products/graphdb/graphdb-free/) and fill out the form. Installation files will sent to you by email. **Use the standalone version of GraphDB**.
2. Upload the **\<graphDB\_file>.zip** file to your server. There are several ways:

- Download any FTP program, such as [FileZilla](https://filezilla-project.org/) (works for Mac OS, Windows and Ubuntu), and copy the **\<graphDB\_file>.zip** to the server's /root directory;

- You can also use sftp://user@ip_address and copy the file over for Ubuntu users. Consult these [instructions](https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server) if needed;

### Installation&#x20;

#### Step 1

Login to the server as root. You **cannot** use sudo and run this script. The command "npm install" **will** fail.

#### Step 2

Execute **one** of the following commands depending on if you have cloned the ot-node repo:

**If the repo is not cloned yet:**

```
apt install git -y && cd /root && git clone https://github.com/OriginTrail/ot-node && cd ot-node && git checkout v6/release/testnet && installer/installer.sh
```

**If you have already cloned the ot-node repo:**

```
/root/ot-node/installer/installer.sh
```

{% hint style="success" %}
**Congratulations. Welcome to v6 beta**
{% endhint %}


**Checking node logs:**

```
journalctl -u otnode --output cat -fn 100
```

![Successfully started](<../.gitbook/assets/Screenshot 2021-12-27 at 15.49.28.png>)

**Stop / Start / Restarting your node:**

```
systemctl stop otnode
systemctl start otnode
systemctl restart otnode
```

****\

We would love to meet you in our Discord chat - join us [here](https://discord.gg/6BGSCJfk4Y).&#x20;
