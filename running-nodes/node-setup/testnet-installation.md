# Testnet Installation

Obtain test TRAC tokens

In order to receive TRAC tokens on the testnet, please join our discord and post your wallet in the \#testnet-discussion channel requesting TRAC on the testnet, or type !Fundme wallet \(update wallet with your public key on the wallet you would like to receive the TRAC on the Rinkeby testnet\), and the discord bot will send those to your wallet.



Prepare the wallets

**Create operational wallet** and management wallets

Create a new wallet using Mycrypto or Metamask and export the private key, which we will use for the operational wallet for the node. Deposit the amount of test TRAC you want to have on your node, which is minimum 3000 TRAC to secure the network + additional TRAC to be able to accept jobs. Make sure you also have at least 0.1 ETH, which you can request through one of the Ethereum faucets \(i.e. [https://faucet.rinkeby.io/](https://faucet.rinkeby.io/)\)



**Configure the server**

Download [Termius ](https://www.termius.com/)\(or any other terminal client like [Kitty](https://www.fosshub.com/KiTTY.html)\) and configure it with the details you received from the VPS hosting \(IP, username, password\). Click on Hosts, Select New host, Choose a Label for the node and add the IP address from the confirmation e-mail from Digital Ocean or Hetzner that the node is created, choose root as username and input the password, and click on Save on the right top corner.

![](https://otnode.com/wp-content/uploads/2020/07/image-3-979x1024.png)

Once you login follow the configuration logic below. Click on the COPY button after each command and **right click** into the terminal window to paste it. Then confirm with Enter

**1. Update the server programs:**

```text
apt update && apt upgrade -y
```

![](https://otnode.com/wp-content/uploads/2020/07/image-4.png)

If you see this notice, choose the first option

![](https://otnode.com/wp-content/uploads/2021/03/image-16.png)

**2. Reboot server with below command, close the window and login again**

```text
reboot
```

**3. Install docker** \(skip this step if you selected the Digital Ocean Server with Docker installation\).

The official installation commands for docker can be found here, should the ones in this section become outdated: [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)

```text
apt-get install apt-transport-https ca-certificates curl software-properties-common
```

```text
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add
```

```text
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"
```

```text
apt-get update
```

```text
apt-get install docker-ce
```

**4. Setup the configuration file**

```text
nano /root/.origintrail_noderc
```

Paste the below in the text editing tool and update the red letters accordingly if you are setting up a node only on x:

```text
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

```text
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

i**nitial\_deposit\_amount** – amount of xTRAC you want to deposit on your node during the installation. \(5000000000000000000000 is equal to 5000 xTRAC\)

**node\_wallet** – Operational wallet public address

**node\_private\_key** – Operational wallet private key. As you will store just 0.1 xDAI there for gas fees, even if server gets compromised, the hacker would have access only to this small amount

**Note**: If your private key start with **0x**, remove these two characters when adding it to the configuration file.

**management\_wallet** – this is your management wallet public address – ideally this should be a wallet on your cold storage \([Ledger Nano S](https://shop.ledger.com/pages/ledger-nano-x?r=c912d8040032), [Trezor](https://shop.trezor.io/?offer_id=10&aff_id=7122), etc.\)

**dh\_price\_factor** – this is the setting of your lambda value – should be less than 1 if you want to accept most of all current jobs. The lower the value, the less paid jobs you are willing to accept.

**Hostname** – this is your server IP, which you can find in the notification e-mail when you setup the VPS

**dh\_max\_holding\_time\_in\_minutes** – the maximum length of jobs you are willing to accept in minutes \(for example 550 000 is to accept one year jobs\).

**5. Install JQ to validate whether the configuration file doesn’t contain any errors**

```text
apt-get install jq
```

```text
jq "." /root/.origintrail_noderc
```

Check the brackets, double quotes and commas. Everything except your data has to be exactly like the example above.

**6. Initiate the node installation**

**Important**: Once you run this command, the TRAC will be deposited to the contract and your first task is to copy and back your ERC725 identity and node identity mentioned on Step 8 below, so you can have control over this deposited amount. Should you get an error at this stage, or if the gas setting you used is too low, do not delete the container or destroy the VPS. Instead join the discord channel or the Official Telegram group to ask for assistance

```text
sudo docker run -i --log-driver json-file --log-opt max-size=1g --name=otnode -p 8900:8900 -p 5278:5278 -p 3000:3000 -v ~/.origintrail_noderc:/ot-node/.origintrail_noderc origintrail/ot-node:release_testnet
```

The first installation runs in interactive mode, and when you click CTRL + C, you both exit the log and stop the node. Thus one additional start command is required.

```text
docker restart otnode
```

**7. Create identities into files on the root directory**

ERC725 identity **on xDAI**

```text
docker cp otnode:/ot-node/data/xdai_erc725_identity.json ~/xdai_erc725_identity.json
```

ERC725 identity **on Ethereum**

```text
docker cp otnode:/ot-node/data/erc725_identity.json ~/erc725_identity.json
```

Node ID

```text
docker cp otnode:/ot-node/data/identity.json ~/identity.json
```

**8. Read erc725 and node id and copy/paste them in secure document**

**XDAI**

```text
more xdai_erc725_identity.json
```

Ethereum

```text
more erc725_identity.json
```

Node Identity

```text
more identity.json
```

Or Login to the server using WINSCP or any other FTP application, go to the root folder and download these two files on your local server and archive them with a password.

\*\*\*\*

**Additional node configurations**

**9. Setup the firewall**

```text
ufw allow 22/tcp && ufw allow 3000 && ufw allow 5278 && ufw allow 8900 && yes | ufw enable
```

**9b. Double check the firewall is properly configured:**

```text
ufw status
```

![](https://otnode.com/wp-content/uploads/2020/07/image-5.png)

\*\*\*\*

**10. Deposit additional xTRAC from your management wallet to the node**

If you want to deposit more than the initial amount, you can deposit the amount of xTRAC which will be available for jobs through the node profile management page at this URL: [https://node-profile.origintrail.io/](https://node-profile.origintrail.io/)

The current recommended amount is 1000 xTRAC in addition to the 3000 xTRAC required to secure the network, and they have to be present on your management wallet.

Login with your XDAI **ERC725 Identit**y which you extracted above and the **operational wallet public address** and follow the instructions on the page. You need metamask to initiate the deposit.

Then on the top left section “Deposit TRAC to Your Node”, enter the amount of TRAC present on your management wallet, to be deposited to the contract for your node, and a set of 2 transactions have to be processed. Metamask popup will show up for you to confirm you want to process the transaction. Once the first transaction is processed, a second popup will show for the second transaction.

Once the deposit is completed, restart your node.

```text
docker restart otnode
```

**11. Enable auto restart and follow the log to monitor the operation of the node**

```text
docker update --restart=always otnode
```

```text
docker logs -f otnode
```

**12. Monitor your node**

You can add your node to the OT Hub and monitor how many jobs has the node won, initiate manual payouts and quickly check if your node is online. The OT Hub can be found on the link below:

[https://othub.origin-trail.network/dashboard](https://othub.origin-trail.network/dashboard)

Also in the **Node Maintenance** section \(menu on the right\) you can find how to setup notifications on your mobile.

**13. Add swap space**

Swap space is dedicated space on your hard drive, which is used as RAM should the hardware RAM is fully utilized. This usually slows down the server as the hard drive is slower than the RAM, however the swap would ensure the node will continue operation. I highly recommend to enable 1 GB Swap space on your server.

```text
fallocate -l 1G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile
```

* confirm it is setup \(SWAP line should show 1\)

```text
free -h
```

![](https://ot.wittymermaid.com/wp-content/uploads/2020/06/image-4.png)

* make it permanent

```text
cp /etc/fstab /etc/fstab.bak
```

```text
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

