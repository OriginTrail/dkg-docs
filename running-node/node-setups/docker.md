# Mainnet Docker Installation

Obtain xDAI and xTRAC

First you need xDAI, which is the gas fee currency on xDAI. Given that the gas fees there are very low, 1-2 xDAI will last you a long time. There are multiple ways to obtain it:

* You can obtain xDAI by following some options described by the xDAI community here: [https://www.xdaichain.com/about-xdai/faqs/xdai-native-coin-token](https://www.xdaichain.com/about-xdai/faqs/xdai-native-coin-token). Then you convert your TRAC through the bridge [https://bridge.xdaichain.com/](https://bridge.xdaichain.com/) – here is a video tutorial how to do it: [https://www.youtube.com/watch?v=oKdh2cOOqUs](https://www.youtube.com/watch?v=oKdh2cOOqUs) This operation would cost one Ethereum smart contract transaction.
* Use the faucet to get 0.01 xdai -&gt; [https://blockscout.com/xdai/mainnet/faucet](https://blockscout.com/xdai/mainnet/faucet)
* If the faucet is not working, join the OriginTrail Community telegram and ask for a cent of xdai -&gt; [https://t.me/OriginTrailCommunity](https://t.me/OriginTrailCommunity)

Second you need xTRAC. If you participated in the SFC boarding, you will obtain back 5% of your TRAC contribution as xTRAC bounty. To claim those, please visit the staking website once announced by the team.

You can also convert TRAC tokens to xTRAC using the Omni Bridge. Go to [https://omni.xdaichain.com/](https://omni.xdaichain.com/) Instructions how to use the bridge can be found here: [https://docs.tokenbridge.net/eth-xdai-amb-bridge/multi-token-extension/ui-to-transfer-tokens/transfer-erc20](https://docs.tokenbridge.net/eth-xdai-amb-bridge/multi-token-extension/ui-to-transfer-tokens/transfer-erc20)

The custom token contract to see xTRAC on your Metamask on xDAI is:

```text
0xEddd81E0792E764501AaE206EB432399a0268DB5Copy
```

Once you have sorted out your xDAI and xTRAC, you need to add the Custom RPC for xDAI, so you can switch your Metamask to the xDAI network. Easiest way to do it is to go to: [https://chainlist.org/](https://chainlist.org/) , click on Connect Wallet in the top right corner and then click “Add me to metamask” button on xDAI section.

![](https://otnode.com/wp-content/uploads/2021/03/image-7.png)

Then you will see on your Metamask xDAI entry when you click on the dropdown on the top where it says Ethereum Mainnet:

![](https://otnode.com/wp-content/uploads/2021/03/image-12.png)

Prepare the wallets

**Create operational wallet** and management wallets

Create a new wallet using Mycrypto or Metamask and export the private key, which we will use for the operational wallet for the node. Deposit the amount of xTRAC you want to have on your node, which is minimum 3000 xTRAC to secure the network + additional xTRAC to be able to accept jobs. Currently around 5-6k total xTRAC is recommended. Also send 0.1 xDAI for gas fees during installation and litigation responses.

If you want to run nodes on Ethereum as well, the process is the same, however each blockchain network requires separate TRAC and ETH for gas fees \(i.e. 4k TRAC on ETH for the Ethereum node + 4k xTRAC for the xDAI node, etc.\). Also deposit 0.1 ETH for gas fees to the operational wallet

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
         "network_id": "ethr:mainnet",
         "identity_filepath": "erc725_identity.json",
         "dh_price_factor" : "1",
         "node_wallet": "xxxxxxxx",
         "node_private_key": "xxxxxxxx",
         "management_wallet": "xxxxxxxx",
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
sudo docker run -i --log-driver json-file --log-opt max-size=1g --name=otnode -p 8900:8900 -p 5278:5278 -p 3000:3000 -v ~/.origintrail_noderc:/ot-node/.origintrail_noderc origintrail/ot-node:release_mainnet
```

Once completed and node has joined the network \(**Make sure you wait and see it**\), exit the log with CTRL +C. If you interrupt the process before the node connecting to the network, you will need to spend some extra time fixing it so please be patient.

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

\*\*\*\*

