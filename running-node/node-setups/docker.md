# Mainnet Docker Installation

## **Obtain xDAI and xTRAC**

First, you need xDAI**

* xDAI is the gas fee currency on the xDAI chain. Given that the gas fees there are very low, 1-2 xDAI will last you a long time.

* You can obtain xDAI by following some options described by the xDAI community here: [https://www.xdaichain.com/about-xdai/faqs/xdai-native-coin-token](https://www.xdaichain.com/about-xdai/faqs/xdai-native-coin-token). Then you convert your TRAC through the bridge [https://bridge.xdaichain.com/](https://bridge.xdaichain.com/) – here is a video tutorial how to do it: [https://www.youtube.com/watch?v=oKdh2cOOqUs](https://www.youtube.com/watch?v=oKdh2cOOqUs) This operation would cost one Ethereum smart contract transaction.
* Use the faucet to get 0.01 xdai -&gt; [https://blockscout.com/xdai/mainnet/faucet](https://blockscout.com/xdai/mainnet/faucet)
* If the faucet is not working, join the OriginTrail Community telegram and ask for a cent of xDAI : [https://t.me/OriginTrailCommunity](https://t.me/OriginTrailCommunity)

Second, you need xTRAC

* xTRAC is minted from TRAC when you convert TRAC from ETH chain to xDAI chain for use on the xDAI chain. No new TRAC is created as the total maximum supply of all TRAC combined is 500 million. 

* If you participated in the SFC boarding, you would have obtained 5% of your TRAC contribution as xTRAC back.

* In order to obtain xTRAC after the boarding process, you have to use the OmniBridge. Go to [https://omni.xdaichain.com/](https://omni.xdaichain.com/) and instructions on how to use the bridge can be found here: [https://docs.tokenbridge.net/eth-xdai-amb-bridge/multi-token-extension/ui-to-transfer-tokens/transfer-erc20](https://docs.tokenbridge.net/eth-xdai-amb-bridge/multi-token-extension/ui-to-transfer-tokens/transfer-erc20)

## **Prepare your wallets on Metamask**

Once you have sorted out your xDAI and xTRAC, you need to add the Custom RPC for xDAI, so you can switch your Metamask from the Ethereum network to the xDAI network. 

The easiest way to do it is to go to: [https://chainlist.org/](https://chainlist.org/), click on Connect Wallet in the top right corner and then click “Add me to metamask” button on xDAI section.

![](https://otnode.com/wp-content/uploads/2021/03/image-7.png)

Then you will see on your Metamask xDAI entry when you click on the dropdown on the top where it says Ethereum Mainnet:

![](https://otnode.com/wp-content/uploads/2021/03/image-12.png)

On the xDAI chain, the custom token contract to see xTRAC is:

```
0xEddd81E0792E764501AaE206EB432399a0268DB5
```

**Operational wallet**

* Create a new wallet on Metamask and note the public and private keys. We will be using this wallet as the operational wallet for your node. You will require one operational wallet per node.
* Connect your management wallet to Metamask. You can use the same management wallet for all your nodes. We strongly recommend physical wallets such as [Ledger Nano S](https://shop.ledger.com/pages/ledger-nano-x?r=c912d8040032) or [Trezor](https://shop.trezor.io/?offer_id=10&aff_id=7122) to secure your coins. 
* Send approximately 0.1 xDAI from your management wallet to your operational wallet to use as gas fees during node installation process or for litigation responses.
* Send approximately 4000 xTRAC from your management wallet to your operational wallet (node wallet). The minimum stake is 3000 xTRAC to secure the network and any additional xTRAC beyond 3000 will be used to bid for jobs. If a 90-day job will pay out 10 xTRAC at the end of the smart contract, you will need to stake 10 xTRAC on your side for that duration. You can always top up your xTRAC balance as needed.

If you want to run nodes on the Ethereum network as well, the process is the same, however each blockchain network requires separate TRAC and ETH for gas fees (i.e. 4k TRAC for the Ethereum node + 4k xTRAC for the xDAI node, etc.). You will also need about 0.1 ETH for gas fees to the operational wallet.

## **Configure your private server**

* Origintrail nodes need to be available 24/7 for data replications processes when requested. If your node do not respond in time due to local power outtage, Internet problems, you run the risk of being litigated and lose the job as well as your stake on that job. With that in mind, it is recommended 99% of the time to rent a Virtual Private Server (VPS) from many providers online.

* We do not endorse any providers in particular, but current node runners are mainly using services from [Digital Ocean](https://www.digitalocean.com/), [Hetzner](https://www.hetzner.com/), [Alwyzon](https://www.alwyzon.com/en), [Vultr](https://www.vultr.com/), just to name a few. 
  * Create an account with your desired VPS provider and look for at least 1 vCPU 2.2GHz, 2GB of ram, 40GB of SSD space. Dedicated servers are not required for now. 

* You will need a SSH client to access and monitor your node. We suggest [Termius](https://www.termius.com/), [Kitty](https://www.fosshub.com/KiTTY.html) or [MobaXterm](https://mobaxterm.mobatek.net/). All softwares mentionned are free. For the guide below, we will be using Termius.

* Open your Termius session and note the IP address, username and password of your VPS hosting. 

* Click on Hosts >> New host >> Choose a label for the node >> add the IP address of your VPS hosting >> choose root as username >> input your password >> Save.

![](https://otnode.com/wp-content/uploads/2020/07/image-3-979x1024.png)

Once you log in, follow the configuration logic below. 

Click on the **COPY** button on the right of each command and **right click** into the terminal window to paste it, then confirm with [Enter].

### **1. Update the server programs:**

```text
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

Paste the below in the text editing tool and update the variables accordingly if you are setting up a node only on xDai:

```
{
   "blockchain": {
     "implementations": [
       {
         "blockchain_title": "xDai",
         "network_id": "xdai:mainnet",
         "identity_filepath": "xdai_erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx"
       } 
     ]
   },
   "network": {
     "hostname": "xxx.xxx.xxx.xxx",
     "remoteWhitelist": "127.0.0.1"
     },
   "initial_deposit_amount": "4000000000000000000000",
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
         "network_id": "ethr:mainnet",
         "identity_filepath": "erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx",
         "disableAutoPayouts": true,
         "rpc_server_url": "xxxxxxxxxxx"
       },
       {
         "blockchain_title": "xDai",
         "network_id": "xdai:mainnet",
         "identity_filepath": "xdai_erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx"
       } 
     ]
   },
   "network": {
     "hostname": "xxx.xxx.xxx.xxx",
     "remoteWhitelist": "127.0.0.1"
     },
   "initial_deposit_amount": "4000000000000000000000",
   "dh_max_holding_time_in_minutes": 530000,
   "dh_maximum_dataset_filesize_in_mb": 10
}
```

**Variables explanation:**

**initial_deposit_amount** – Amount of xTRAC you want to deposit on your node during the installation (4000000000000000000000 is equal to 4000 xTRAC).

**node_wallet** – This is your operational wallet public address.

**node_private_key** – This is your operational wallet private key. Since you will only be storing 0.1 xDAI (equivalent to 0.10$ USD) there for gas fees and litigation processes, even if server gets compromised, the hacker would only have access to that amount. 

**Note**: If your private key start with **0x**, remove these two characters when adding it to the configuration file.

**management_wallet** – This is your management wallet public address – ideally this should be your physical wallet such as Trezor or Ledger Nano S. 

**dh_price_factor** – This is the setting of your lambda value – should be 1 if you want to accept all current jobs. The lower the value, the less paid jobs you are willing to accept.

**Hostname** – This is your server IP, which you can find in the notification e-mail when you setup your VPS.

**dh_max_holding_time_in_minutes** – the maximum length of jobs you are willing to accept in minutes (input 525600 for maximum one year jobs).

### **5. Install jq to make sure the configuration file doesn’t contain any errors**

```
apt-get install jq
```

```
jq "." /root/.origintrail_noderc
```

Check the brackets, double quotes and commas. Everything except your data has to be exactly like the example above.

### **6. Initiate the node installation**

**Important**: Once you run this command, the xTRAC on your operational wallet will be deposited to the contract address. To keep control of your deposited amount, you must copy and protect your ERC725 identity as well as your node identity (step 8 below). Should you get an error at this stage, do not delete the container or destroy the VPS - join the discord channel or the Official Telegram group for assistance.

```
sudo docker run -i --log-driver json-file --log-opt max-size=50m --name=otnode -p 8900:8900 -p 5278:5278 -p 3000:3000 -v ~/.origintrail_noderc:/ot-node/.origintrail_noderc origintrail/ot-node:release_mainnet
```

Once completed and node has joined the network, exit the log with CTRL+C. If you interrupt the process before the node connects to the network, you will need to spend some extra time fixing it so please be patient. **Make sure you wait and see that the node is connected**.

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

xDAI

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

When you are done, delete these files from your root folder
```
rm xdai_erc725_identity.json erc725_identity.json identity.json
```
Clear the history of your current shell
```
history -c
```
****

### **9. Setup the firewall**

```
ufw allow 22/tcp && ufw allow 3000 && ufw allow 5278 && ufw allow 8900 && yes | ufw enable
```

Double check the firewall is properly configured

```
ufw status
```

![](https://otnode.com/wp-content/uploads/2020/07/image-5.png)

### **10. Deposit additional TRAC**

If you want to deposit more than the initial amount, you can deposit the amount of xTRAC which will be available for jobs through the node profile management page at this URL: [https://node-profile.origintrail.io/](https://node-profile.origintrail.io/)

The current recommended amount is 1000 xTRAC in addition to the 3000 xTRAC required to secure the network. Any further deposits to your node have to be done via your management wallet on the node profile management console. 

Log in with your xDAI **ERC725 Identity** which you extracted above and the **operational wallet public address** and follow the instructions on the page. You need metamask to initiate the deposit.

Then on the top left section “Deposit TRAC to Your Node”, enter the amount of TRAC present on your management wallet, to be deposited to the contract for your node, and a set of 2 transactions have to be processed. Metamask popup will show up for you to confirm you want to process the transaction. Once the first transaction is processed, a second popup will show for the second transaction.

Once the deposit is completed, restart your node.

```
docker restart otnode
```

**11. Enable auto restart and follow the operation of your node**

```
docker update --restart=always otnode
```

```
docker logs -f otnode
```
You can adjust the command above to show logs in the past 15 minutes only
```
docker logs -f --since 15m otnode
```

**12. Monitor your node in a web interface**

You can add your node to the OT Hub and monitor how many jobs your node have won and initiate manual payouts. The OT Hub can be found on the link below:

[https://othub.origin-trail.network/dashboard](https://othub.origin-trail.network/dashboard)

**13. Add swap space**

Swap space is dedicated space on your hard drive, which is used as RAM should the hardware RAM is fully utilized. This usually slows down the server as the hard drive is slower than the RAM, however the swap would ensure the node will continue operation. I highly recommend to enable 1 GB Swap space on your server.

```
fallocate -l 1G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile
```

confirm it is setup (SWAP line should show 1)

```
free -h
```

![](https://ot.wittymermaid.com/wp-content/uploads/2020/06/image-4.png)

make it permanent

```
cp /etc/fstab /etc/fstab.bak
```

```
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
Because server ram is much faster, you want your server to prioritize server ram rather than swap space ram. 

In order to do this, you want to reduce the default swappiness value of 60 (on a scale from 0 to 100, 0 being ignore swap space completely and 100 being prioritize swap space)
```
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"
```
```
sudo sysctl -p
```

**14. Reduce journal log size**

Reduce the size of logs saved on your system. Since node storage space is a problem right now, you don't want your logs to go out of control. you can change "50M" to the amount you want.
```
sed -i 's/SystemMaxUse=.*/SystemMaxUse=50M/g' /etc/systemd/journald.conf
```

**15. Additional setups**

If you want to automate daily backups efficiently, get Telegram notifications on jobs won, notifications when your docker is down, disk usage above a certain threshold, run nodes without docker, please visit this link https://github.com/calr0x created by Calvin, one of our best tech guy in the Origintrail community.

If you want to know when your server isn't responding, monitor CPU, Memory, storage usage and so on, we strongly suggest installing NetData on your server by following instructions here : https://learn.netdata.cloud/docs/agent/packaging/installer/methods/kickstart.

If you need any assistance while installing the steps above, please join the [Community Node Support Group](https://t.me/otnodegroup) !

### **Congratulations and welcome to the Origintrail Decentralized Network !**