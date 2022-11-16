# Backing up your node

## 1. Manual backup/migration

In case you wish to manually migrate your OriginTrail V6 node to some other instance or just make a simple back up, make sure that the following files are included:

* Backup the triple store: e.g. in case of blazegraph backup the **blazegraph.jnl** file
* Back up the **ot-node** directory
* Backup the **operationaldb** (via Mysql dump or similar)
* Backup the /lib/system/systemd/**otnode.service** (file)



## 2. Remote network backup (coming soon)
