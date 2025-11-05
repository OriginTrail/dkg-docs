# Random Sampling rollout

The deployment of the DKG Random Sampling system follows a carefully phased approach to ensure stability, fairness, and backward compatibility with earlier versions of the DKG. This page outlines the rollout timeline, what each release includes, and what node operators and delegators can expect.

### Overview of releases

#### ✅ Phase 1: RFC Confirmation

* **Goal:** Finalize community review of [OT-RFC-24](https://github.com/OriginTrail/OT-RFC-repository/tree/main/RFCs/OT-RFC-24_DKG_V8_Random_sampling_proof_system)
* **Outcome:** Approval of the Random Sampling design by the community and core development team
* **Phase status:&#x20;**<mark style="color:green;">**Completed**</mark>

#### 🚀 Phase 2: V8.1.0 — Initial rollout (Active Proof System)

* **Features introduced:**
  * Live Random Sampling challenge generation and proof submission
  * Score calculation per proof period
  * Epoch-based reward allocation system
  * DKG Sync system goes online
* **Who is affected:**
  * **Core Nodes** begin submitting live proofs
  * **Delegators** start accruing rewards for the active epochs (but do not yet claim rewards for past epochs)
* **Purpose:** Establish live PoK infrastructure and real-time score updates for staking participants
* **Phase status:&#x20;**<mark style="color:yellow;">**Live on Testnet. Mainnet rollout expected in June 2025**</mark>

#### 🔄 Phase 3: V8.1.1 — V6 Compatibility Module goes online

* **Goal:** Allow accumulated rewards from the DKG V6 era to be earned retroactively
* **How it works:**
  * Applies the Random Sampling system retroactively for TRAC fees in the V6 period
  * Nodes that were active during the V6 phase can compete for retroactive rewards, claiming tokens for completed epochs and competing for upcoming epochs.
* **Compatibility duration:** Available for a limited window (12 months from V8.0 launch)
* **Phase status: Testnet & mainnet rollout expected in June 2025**

#### 🛠 Phase 4: V8.1.2 — Tuning Period Module

* **Goal:** Distribute locked fees for the period between V8.0.0 and V8.1.0 releases
* **How it works:**
  * All active nodes during this period are considered to have **100% uptime** for the purpose of reward allocation
  * The same score distribution and reward formula is applied as in the live Random Sampling system
* **Phase status: Testnet & mainnet rollout expected in June 2025**

### Rollout principles

* **Incremental activation** — Each module builds on the previous one, ensuring that no backward compatibility is broken
* **Transparency first** — The DKG Staking Dashboard will be upgraded to reflect:
  * **Node Power**, which will represent the current node power in the network with regard to its stake, service ask, and publishing factor
  * **Node Health,** computed based on proof submissions per epoch
  * Compatibility module reward status
* **Fail-safe participation** — Delegators and node runners are protected from loss of eligibility due to technical transitions, with catch-up mechanisms in place for reward collection

### What you should do

#### Node runners

* Make sure to follow the updates to update your node as soon as the V8.1 release goes live on the mainnet.
* Once your node is updated, make sure to monitor and maintain its proof submission health.
* Optionally enable auto-claiming for delegators via node services to automatically restake all rewards and increase your Node Power.

#### Delegators

* You don’t need to take immediate action.
* Make sure you understand when rewards become claimable based on finalization rules.
* Use the upgraded Staking Dashboard to track your delegator epoch scores and rewards

