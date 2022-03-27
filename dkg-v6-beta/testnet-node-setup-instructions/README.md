# Testnet node - setup instructions

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

* A dedicated **4GB RAM/2CPUs/50GB HDD** server (minimum hardware requirements)
* A running graph database (see below)

### **Prepare the graph database**

**In the following sections, you can choose between GraphDB or Blazegraph (or other databases to come). If you choose one, you can ignore the instructions for the others.**

**To get GraphDB:**
1. Please visit their [official website](https://www.ontotext.com/products/graphdb/graphdb-free/) and fill out the form. Installation files will sent to you by email. **Use the standalone version of GraphDB**.
2. Upload the **\<graphDB\_file>.zip** file to your server. There are several ways:
* Download any FTP program, such as [FileZilla](https://filezilla-project.org) (works for Mac OS, Windows and Ubuntu), and copy the **\<graphDB\_file>.zip** to the server's /root directory;
* You can also use sftp://user@ip\_address and copy the file over for Ubuntu users. Consult these [instructions](https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server) if needed.

**To get Blazegraph:**
The instructions to get Blazegraph are included in the following dockerless and Arch sections - so skip this part. For Docker setups, you can do the following to download Blazegraph :
1. wget https://github.com/blazegraph/database/releases/latest/download/blazegraph.jar
2. dpkg -i blazegraph.deb
Please consult this [link](https://github.com/OriginTrail/ot-node/issues/1747) for more information.


**Next, we have prepared 3 different ways to start your v6 testnet node:**

1. [Automate setup instructions for Ubuntu server](https://docs.origintrail.io/dkg-v6-upcoming-version/testnet-node-setup-instructions/setup-instructions-dockerless) - Dockerless (recommended)
2. [Setup instructions using Docker](https://docs.origintrail.io/dkg-v6-upcoming-version/testnet-node-setup-instructions/docker-setup)
3. [Setup instructions for Arch Linux server](https://docs.origintrail.io/dkg-v6-upcoming-version/testnet-node-setup-instructions/setup-instructions-arch-linux)
