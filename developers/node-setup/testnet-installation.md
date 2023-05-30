# Testnet Installation

## Obtain test TRAC tokens

In order to receive TRAC tokens on the testnet, please join our discord and post your wallet in the #testnet-discussion channel requesting TRAC from the faucet bot. Discord faucet bot operates on **Rinkeby**, **Kovan** and **Polygon** test networks. You can use the following commands in order to request test TRAC tokens:

**Rinkeby**: !fundme\_rinkeby _<_wallet\_address>

**Polygon**: !fundme\_mumbai _<_wallet\_address>

**Kovan**: !fundme\_kovan _<_wallet\_address>

Bot will provide you with **6000 TRAC** tokens on the network of your choice.&#x20;

**Note:** _In order to see the tokens in your Metamask, you will have to switch it to the desired network and "Import token" by entering the token contract address._&#x20;

### Test TRAC token contracts:

**Rinkeby:** 0x98d9a611ad1b5761bdc1daac42c48e4d54cf5882

**Polygon testnet (Mumbai):** 0x10eD38C374b2F5bBA3E85b9c478B9fc69559355B&#x20;

**Kovan testnet:** 0x3C841844cFe11d3999eD5c0B0d1714cC1eBB23dc

### **Bot help:**

Ask our bot for help by executing the **!help** command and see the list of all networks and available interactions.

## Prepare the wallets

**Create operational wallet** and management wallets

Create a new wallet using Mycrypto or Metamask and export the private key, which we will use for the operational wallet for the node. Deposit the amount of test TRAC you want to have on your node, which is minimum 3000 TRAC to secure the network + additional TRAC to be able to accept jobs. Make sure you also have at least 0.1 test ETH,KOVAN or MATIC in order for your node to be able to pay for the blockchain transactions.&#x20;

## **Configure the server**

Download [Termius ](https://www.termius.com/)(or any other terminal client like [Kitty](https://www.fosshub.com/KiTTY.html)) and configure it with the details you received from the VPS hosting (IP, username, password). Click on Hosts, Select New host, Choose a Label for the node and add the IP address from the confirmation e-mail from Digital Ocean or Hetzner that the node is created, choose root as username and input the password, and click on Save on the right top corner.

![](https://otnode.com/wp-content/uploads/2020/07/image-3-979x1024.png)

Once you login follow the configuration logic below. Click on the COPY button after each command and **right click** into the terminal window to paste it. Then confirm with Enter

### **1. Update the server programs:**

```
apt update && apt upgrade -y
```

![](https://otnode.com/wp-content/uploads/2020/07/image-4.png)

If you see this notice, choose the first option

![](https://otnode.com/wp-content/uploads/2021/03/image-16.png)

### **2. Reboot server with below command, close the window and login again**

```
reboot
```

### **3. Install docker** (skip this step if you selected the Digital Ocean Server with Docker installation).

The official installation commands for docker can be found here, should the ones in this section become outdated: [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)

```
apt-get install apt-transport-https ca-certificates curl software-properties-common
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add
```

```
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"
```

```
apt-get update
```

```
apt-get install docker-ce
```

### **4. Setup the configuration file**

```
nano /root/.origintrail_noderc
```

Paste the below in the text editing tool and update the xxxxx entries accordingly if you are setting up a node only on xDAI:

```
{
   "blockchain": {
     "implementations": [
       {
         "blockchain_title": "xDai",
         "network_id": "xdai:testnet",
         "identity_filepath": "xdai_erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx"
       } 
     ]
   },
   "network": {
     "hostname": "xxx.xxx.xxx.xxx"
     },
   "initial_deposit_amount": "5000000000000000000000",
   "dh_max_holding_time_in_minutes": 530000,
   "dh_maximum_dataset_filesize_in_mb": 10
}
```

save the file by **Ctrl-O** and **Enter** and exit by **Ctrl-X**

If you are going to run nodes on Ethereum as well, use the following configuration file:

```
{
   "blockchain": {
     "implementations": [
       {
         "blockchain_title": "Ethereum",
         "network_id": "ethr:rinkeby:1",
         "identity_filepath": "erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx",
         "rpc_server_url": "xxxxxxxxxxx"
       },
       {
         "blockchain_title": "xDai",
         "network_id": "xdai:testnet",
         "identity_filepath": "xdai_erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx"
       } 
     ]
   },
   "network": {
     "hostname": "xxx.xxx.xxx.xxx"
     },
   "initial_deposit_amount": "5000000000000000000000",
   "dh_max_holding_time_in_minutes": 530000,
   "disableAutoPayouts": true,
   "dh_maximum_dataset_filesize_in_mb": 10
}
```

**Explanation:**

i**nitial\_deposit\_amount** – amount of xTRAC you want to deposit on your node during the installation. (5000000000000000000000 is equal to 5000 xTRAC)

**node\_wallet** – Operational wallet public address

**node\_private\_key** – Operational wallet private key. As you will store just 0.1 xDAI there for gas fees, even if server gets compromised, the hacker would have access only to this small amount

**Note**: If your private key start with **0x**, remove these two characters when adding it to the configuration file.

**management\_wallet** – this is your management wallet public address – ideally this should be a wallet on your cold storage

**dh\_price\_factor** – this is the setting of your lambda value – should be less than 1 if you want to accept most of all current jobs. The lower the value, the less paid jobs you are willing to accept.

**Hostname** – this is your server IP, which you can find in the notification e-mail when you setup the VPS

**dh\_max\_holding\_time\_in\_minutes** – the maximum length of jobs you are willing to accept in minutes (for example 550 000 is to accept one year jobs).

### **5. Install JQ to validate whether the configuration file doesn’t contain any errors**

```
apt-get install jq
```

```
jq "." /root/.origintrail_noderc
```

Check the brackets, double quotes and commas. Everything except your data has to be exactly like the example above.

### **6. Initiate the node installation**

**Important**: Once you run this command, the TRAC will be deposited to the contract and your first task is to copy and back your ERC725 identity and node identity mentioned on Step 8 below, so you can have control over this deposited amount. Should you get an error at this stage, or if the gas setting you used is too low, do not delete the container or destroy the VPS. Instead join the discord channel or the Official Telegram group to ask for assistance

```
sudo docker run -i --log-driver json-file --log-opt max-size=1g --name=otnode -p 8900:8900 -p 5278:5278 -p 3000:3000 -v ~/.origintrail_noderc:/ot-node/.origintrail_noderc origintrail/ot-node:release_testnet
```

The first installation runs in interactive mode, and when you click CTRL + C, you both exit the log and stop the node. Thus one additional start command is required.

```
docker restart otnode
```

### **7. Create identities into files on the root directory**

ERC725 identity **on xDAI**

```
docker cp otnode:/ot-node/data/xdai_erc725_identity.json ~/xdai_erc725_identity.json
```

ERC725 identity **on Ethereum**

```
docker cp otnode:/ot-node/data/erc725_identity.json ~/erc725_identity.json
```

Node ID

```
docker cp otnode:/ot-node/data/identity.json ~/identity.json
```

### **8. Read erc725 and node id and copy/paste them in secure document**

**XDAI**

```
more xdai_erc725_identity.json
```

Ethereum

```
more erc725_identity.json
```

Node Identity

```
more identity.json
```

Or Login to the server using WINSCP or any other FTP application, go to the root folder and download these two files on your local server and archive them with a password.



## **Additional node configurations**

### **9. Setup the firewall**

```
ufw allow 22/tcp && ufw allow 3000 && ufw allow 5278 && ufw allow 8900 && yes | ufw enable
```

**Double check the firewall is properly configured:**

```
ufw status
```

![](https://otnode.com/wp-content/uploads/2020/07/image-5.png)



### **10. Enable auto restart and follow the log to monitor the operation of the node**

```
docker update --restart=always otnode
```

```
docker logs -f otnode
```

### **11. Add swap space**

Swap space is dedicated space on your hard drive, which is used as RAM should the hardware RAM is fully utilized. This usually slows down the server as the hard drive is slower than the RAM, however the swap would ensure the node will continue operation. I highly recommend to enable 1 GB Swap space on your server.

```
fallocate -l 1G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile
```

* confirm it is setup (SWAP line should show 1)

```
free -h
```

![](https://ot.wittymermaid.com/wp-content/uploads/2020/06/image-4.png)

* make it permanent

```
cp /etc/fstab /etc/fstab.bak
```

```
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
