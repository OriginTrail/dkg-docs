# Feature roadmap

## Release timeline

The V8 deployment is a major update executed as a direct upgrade on the existing OriginTrail V6 network. The update process will, therefore, require several migrations to be executed. To successfully complete all the necessary activities, the V8 launch will be executed through an “**Upgrade Period**”, which will last for approximately 1 week. During the Upgrade Period, all relevant DKG components will be updated (nodes, blockchain contracts, Staking Dashboard, DKG Explorer, and others). The update will be executed on all three connected blockchains - NeuroWeb, Gnosis, and Base.&#x20;



<figure><img src="../../../../.gitbook/assets/V8 Timeline.png" alt=""><figcaption><p>V8 timeline illustration</p></figcaption></figure>

The beginning of the Upgrade Period, marking the start of the V8 deployment, is scheduled for **Thursday, December 19th, 2024**, and the Upgrade Period is expected to end on **Thursday, December 26th, 2024**.

## V8.0 - Launch and Tuning Period

Following the launch of DKG V8.0, which will introduce fundamental updates and batch-minting features, the network will enter the **Tuning Period.** During this period more features and parameter tuning updates are expected on all blockchains of the network.&#x20;

During the Tuning Period, DKG Core Nodes will be accruing rewards, which will be claimable after the expiry of the first epoch in V8, which is expected to be at the end of January (with the shortened epoch).&#x20;

The pending publishing rewards from the V6 period will also be made available through the new proof system through the upgrade, with the V6 tokenomics factor of TRAC stake being the only reward factor (as the distance factor is being deprecated), and available only to nodes online prior to V8 launch. The new Random Sampling System will also tackle the problem of under-submission of proofs by V6 nodes, making the reward collection process more efficient. Due to the migration to the new system of synchronized epochs, the V6 reward pool will be distributed across 1 year.

Features and updates expected for the Tuning period  (V8.0.x)

<table><thead><tr><th width="182">Feature</th><th width="246">Description</th><th width="180">Release</th><th>ETA</th></tr></thead><tbody><tr><td>Paranets support</td><td>Introducing V8 paranets and re-enabling existing ones</td><td>V8.0.1</td><td>mid-January 2025</td></tr><tr><td>Tuning release</td><td>Updates discovered during the Tuning Period, backwards compatibility</td><td>V8.0.2</td><td>January 2025</td></tr><tr><td>Tuning release 2</td><td>Updates discovered during the Tuning Period, updating V8 Knowledge Assets becomes operational</td><td>V8.0.3</td><td>January 2025</td></tr></tbody></table>

### Backward compatibility

Due to changes in Knowledge Assets V2 and protocol updates, the V8.0 network is unfortunately not fully backward compatible with V6 clients. However, backward compatibility will be extended in the coming minor releases as well.  **If you need any assistance with your V6 applications or migrating to V8,** [**contact the core developers in Discord directly**](https://discord.gg/xCaY7hvNwD)**, and we will gladly assist.**&#x20;

We intend to expand the level of backward compatibility over the V8.0 releases.

## Post Tuning period

The Tuning Period ends with **V8.1**, which fully introduces the **Random Sampling** features and completes the scalability updates. From this point on, the Core Nodes will start collecting rewards, and the system will be further tuned for different blockchains. More details on the Random Sampling features will be published in the documentation in due time.

Features and updates expected after the Tuning period

<table><thead><tr><th>Feature</th><th>Description</th><th width="187">Release</th><th>ETA</th></tr></thead><tbody><tr><td>Random sampling proof system (RSPS)</td><td>RSPS will enable the proof system enabling nodes collecting rewards</td><td>V8.1.0</td><td>February 2025</td></tr><tr><td>Collective Programmatic Treasury support</td><td>CPT enablement</td><td>V8.2.0</td><td>March 2025</td></tr></tbody></table>
