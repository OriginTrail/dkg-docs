## FAQ - OriginTrail V8 DKG Core Node

### 1. What are the minimum hardware requirements for running a V8 DKG Core Node?

To run the OriginTrail V8 DKG Core Node, you need a server with at least the following hardware specifications:

- **RAM:** 4 GB
- **CPU:** 2 cores
- **Storage:** 50 GB HDD (SSD is recommended)
- **Operating System:** Ubuntu 20.04 LTS or 22.04 LTS


### 2. How can I get ETH and TRAC on the Base Sepolia Testnet?

- **For Base Sepolia ETH:** You can get ETH from Base Sepolia testnet faucets listed in the [official Base documentation](https://docs.base.org/docs/tools/network-faucets/).
- **For Base Sepolia TRAC:** Use the faucet bot in the official OriginTrail Discord. Go to the `faucet-bot` channel and send the following command:

```sh
!fundme_v8_base_sepolia_trac <your_wallet_address>
```

**Example:**

```plaintext
!fundme_v8_base_sepolia_trac 0x0134a3e4...
```

After running the command, you will receive TRAC tokens in your wallet.

### 3. What is the contract address for the Base Sepolia test TRAC?

The contract address for the Base Sepolia **test TRAC** token is:

```sh
0x9b17032749aa066a2DeA40b746AA6aa09CdE67d9
```

You can use this contract address to add the test TRAC token to your wallet.

### 4. What’s the difference between an operational key and an admin key?

- **Operational Key:** This key is used by the node to sign blockchain transactions. The private key **must** be stored on the server and accessible by the node to automatically sign transactions.
- **Admin Key:** This key is used for administrative tasks (e.g., key rotation) by the node operator. You **do not need** to store the private key on the server. It can be kept in a hardware wallet or multisig for better security.

### 5. Do I need to run the installer as `root` or use `sudo`?

**Yes**, you should run the installer as the **root** user, but **do not use `sudo`**. Ensure you are logged in as the `root` user before starting the installer. Running the installer without root privileges could cause issues during installation.

### 6. What does `otnode-logger.service` do?

**`otnode-logger.service`** automatically streams your node logs to the OriginTrail team for support and debugging purposes. This service is required to participate in the incentivized testnet program.

If you wish to disable this service after installation, you can do so with the following commands:

```sh
systemctl disable otnode-logger.service
systemctl stop otnode-logger.service
```

### 7. How can I verify if my node is running correctly after installation?

After a successful installation, you can check if your node is running by using the following command:

```sh
systemctl status otnode
```

You can also view the node logs to confirm everything is working by running:

```sh
journalctl -u otnode --output cat -fn 100
```

### 8. How can I update my node configuration after installation?

To modify your node configuration, open the `.origintrail_noderc` file with the following command:

```sh
nano /root/ot-node/.origintrail_noderc
```

Once you've made changes, restart your node to apply them:

```sh
systemctl restart otnode
```

### 9. What should I do if I encounter issues during installation?

If you face any problems during installation, you can:

- Check for error messages by running:
  
  ```sh
  journalctl -u otnode --output cat -fn 100
  ```

- Join the official [**OriginTrail Discord**](https://discord.gg/W3TgYKpc) in the `v8-discussion` channel and ask for help.
- Send an email to **tech@origin-trail.com** for direct technical assistance.

### 10. How can I check my wallet balance on Base Sepolia?

You can check your ETH and TRAC balances on the Base Sepolia Testnet using a blockchain explorer like:

- **Base Sepolia Explorer:** [https://sepolia.etherscan.io/](https://sepolia.etherscan.io/)

Enter your wallet address to view your balance and transaction history.

### 11. Can I use the same operational key for multiple nodes?

It is **not recommended** to use the same operational key for multiple nodes. Doing so could cause conflicts in signing transactions and managing data. Each node should have a unique operational key.

### 12. What should I do if my node's transactions fail?

If your node experiences failed transactions, it could be due to insufficient funds, an RPC issue, or a network problem. Here's what to check:

- Ensure your wallet has enough ETH and TRAC to cover transaction fees.
- Verify your RPC endpoint is functioning correctly and has a stable connection.
- Check the node logs for specific error messages using:

```sh
journalctl -u otnode --output cat -fn 100
```

For any further questions or assistance, feel free to join our [**Discord community**](https://discord.gg/W3TgYKpc) or reach out to us at [**tech@origin-trail.com**](mailto:tech@origin-trail.com).