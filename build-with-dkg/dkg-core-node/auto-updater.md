---
icon: screwdriver-wrench
---

# Auto Updater

### What does the Auto Updater do?

The Auto Updater module ensures your DKG Core Node is always running the **latest stable version** of the DKG, without you having to manually check, pull, or restart anything.

Every **15 minutes**, the updater:

* Checks if a newer version of the code is available.
* If a new version is found, it updates the node and restarts it automatically.

***

### 🔁 How it works

1. **Check for updates** Every 15 minutes, your node contacts the remote GitHub repository to check if there is a newer version than the one it's currently running.
2. **Version comparison**
   * If the **remote version is newer**, it pulls the update and restarts the node.
   * If the **remote version is older or the same**, no changes are made.
3. **Update and restart** After a successful update, a file named `UPDATED` is written to disk, and the node is automatically restarted to load the new version.

***

### 🧩 Mainnet vs Testnet Configuration

Depending on whether you are running a **mainnet** or **testnet** node, the updater checks different branches for updates.

To enable the auto updater, you will need to have this section in the `.origintrail_noderc` configuration file (found in the `ot-node` folder)

#### ✅ Mainnet Node Config:

```json
"modules": {
  "autoUpdater": {
    "enabled": true,
    "implementation": {
      "ot-auto-updater": {
        "package": "./auto-updater/implementation/ot-auto-updater.js",
        "config": {
          "branch": "v6/release/mainnet"
        }
      }
    }
  }
}
```

* The updater will check the `v6/release/mainnet` branch of the GitHub repository for updates.

***

#### 🧪 Testnet Node Config:

```json
"modules": {
  "autoUpdater": {
    "enabled": true,
    "implementation": {
      "ot-auto-updater": {
        "package": "./auto-updater/implementation/ot-auto-updater.js",
        "config": {
          "branch": "v6/release/testnet"
        }
      }
    }
  }
}
```

* The updater will track updates from the `v6/release/testnet` branch.

This allows core developers to push test features to testnet users while keeping mainnet nodes stable and production-ready.

***

### 🛡️ Safety Features

* **No downgrades**: If the remote version is **lower than or equal to your current version**, the update is skipped.
* **Error recovery**: If the updater encounters an error (e.g., network issues), it logs the error and retries again after 15 minutes.
* **Versioning system**: Uses strict semantic versioning to prevent invalid comparisons.
* **Rollback:** If you encounter an error, the auto updater **keeps the previous version available** in the `ot-node` folder, under the version name. In case you need to roll back, change the `current` symlink to point to the location of the previous working version

***

### ✅ Requirements to Use

* You must set `"enabled": true` in the config.
* Restart permissions must be allowed (handled by `process.exit(1)` in code).

***

### 🧭 What to Expect

* Smooth, automatic upgrades.
* Minimal manual intervention.
* Your node always on the latest version.

***

