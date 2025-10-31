[aryachain_node_architecture_en.md](https://github.com/user-attachments/files/23257564/aryachain_node_architecture_en.md)
# **AryaChain Node Architecture — Technical Overview (v1.0)**

### **1. Introduction**

AryaChain’s network is built upon a layered architecture where each node type has a specific purpose, storage responsibility, and reward mechanism.  
This modular structure enables scalability, transparency, and decentralization, ensuring that every participant — from high-capacity validators to casual mobile users — can contribute to the network based on their available resources.

The system defines three functional layers:

1. **Consensus & Execution Layer** – responsible for validating and producing blocks.  
2. **Service & Data Layer** – focused on providing APIs, off-chain storage, and accessibility.  
3. **Access Layer** – connecting end users to the blockchain through lightweight or mobile clients.

---

### **2. Consensus & Execution Layer**

#### **Core Full Node**
**Role:** Executes the Rules Configuration File, maintains the full blockchain state, validates transactions and blocks, and participates directly in consensus.  
**Stored Data:**  
- Complete on-chain data (blocks, transactions, headers, and account state)  
- No off-chain data  
**Deletion Policy:** May prune old cached blocks (safe pruning only)  
**Consensus Participation:** ✅ Yes (miner or validator)  
**Reward:** Block reward + transaction fees  

**Description:**  
Core Full Nodes form the backbone of the network. They enforce protocol rules, maintain global state integrity, and serve as reference nodes for all other participants.

---

#### **Miner Node**
**Role:** Performs Proof-of-Work calculations and submits valid blocks to a connected Core Full Node.  
**Stored Data:**  
- Partial block templates and headers only  
- No full state  
**Consensus Participation:** ⚙️ Indirect, via a connected Full Node  
**Reward:** Share of block reward  

**Description:**  
A miner node operates as a lightweight worker. It does not validate the full chain but depends on a Full Node for transaction templates and verification. Once a valid block is found, it is broadcast through the Full Node to the network.

---

#### **Validator Node**
**Role:** Signs or votes on block proposals in the Proof-of-Stake process.  
**Stored Data:**  
- Partial information (candidate block headers, validator list)  
- No full state (relies on its paired Full Node)  
**Consensus Participation:** ⚙️ Indirect, via Execution Node  
**Reward:** Staking rewards + transaction fees  

**Description:**  
Validators focus solely on signing and attesting block proposals. Their separation from state execution improves security (private keys are isolated) and allows lighter hardware requirements.

---

### **3. Service & Data Layer**

#### **Service Node**
**Role:** Acts as an API and data gateway, storing and distributing off-chain metadata (DAO votes, NFT attributes, messages, etc.) and relaying transactions to the network.  
**Stored Data:**  
- Full on-chain data  
- Partial off-chain metadata  
**Deletion Policy:** Can delete old or expired off-chain data only  
**Consensus Participation:** ❌ No  
**Reward:** Relay reward + storage reward  

**Description:**  
Service Nodes form AryaChain’s communication and scalability layer. They connect dApps, wallets, and users to the blockchain through gRPC or REST interfaces, without needing consensus participation.  

---

#### **Archive Node**
**Role:** Maintains a complete, immutable record of all on-chain and off-chain data for analytics, historical queries, or AI models.  
**Stored Data:**  
- Complete on-chain and off-chain datasets  
**Deletion Policy:** None  
**Consensus Participation:** ❌ No  
**Reward:** Snapshot or historical query reward  

**Description:**  
Archive Nodes serve as the long-term memory of AryaChain. They never prune data and are essential for explorers, governance audits, and historical analysis.

---

### **4. Access Layer**

#### **Light Node**
**Role:** Simplified Payment Verification (SPV) or lightweight mobile client. Verifies transactions or account proofs using Merkle proofs from Full or Service Nodes.  
**Stored Data:**  
- Block headers only  
- No transaction body, state, or metadata  
**Consensus Participation:** ❌ No  
**Reward:** Optional micro-rewards for relaying transactions or verifying proofs  

**Description:**  
Light Nodes enable everyday users to interact with AryaChain securely without downloading the full blockchain. They maintain independence from centralized APIs by validating cryptographic proofs directly on-device.

---

### **5. Reward Domains and Incentive Model**

AryaChain divides its reward structure into several economic domains:

| Domain | Participants | Reward Source | Description |
|--------|----------------|----------------|-------------|
| **Consensus Reward** | Full Nodes, Miners, Validators | Block creation + transaction fees | Incentivizes securing the network and validating blocks |
| **Relay Reward** | Service Nodes, Light Clients | Micro-fees per relayed transaction | Encourages decentralization of transaction propagation |
| **Storage Reward** | Service Nodes | Off-chain data storage | Rewards reliable metadata hosting (e.g., NFTs, DAO logs) |
| **Snapshot Reward** | Archive Nodes | DAO treasury allocation | Supports long-term data availability and analytics |

---

### **6. Layered Architecture (Overview Diagram)**

```
          +--------------------------------+
          |        Access Layer             |
          |  (Light Nodes / Mobile Wallets) |
          +---------------+----------------+
                          |
                          v
          +--------------------------------+
          |     Service & Data Layer        |
          | (Service / Archive Nodes)       |
          +---------------+----------------+
                          |
                          v
          +--------------------------------+
          |  Consensus & Execution Layer    |
          | (Full Nodes / Miners / Validators) |
          +--------------------------------+
```

---

### **7. Summary Table**

| Node Type | On-chain Data | Off-chain Data | Deletion | Consensus Role | Typical Rewards | Main Function |
|------------|---------------|----------------|-----------|----------------|-----------------|----------------|
| Core Full Node | ✅ Full | ❌ None | Prune only | Direct | Block reward + fees | Executes rules, validates blocks |
| Miner Node | Partial | None | No | Indirect | Share of block reward | Performs PoW computations |
| Validator Node | Partial | None | No | Indirect | Staking reward | Signs and votes on blocks |
| Service Node | Full | Partial | Off-chain only | No | Relay + storage reward | API gateway, metadata store |
| Archive Node | Full | Full | No | No | Snapshot reward | Historical storage and analytics |
| Light Node | Headers only | None | No | No | Optional micro-reward | Lightweight verification for users |

---

### **8. Conclusion**

The multi-layered node architecture of AryaChain enables a balanced ecosystem that combines decentralization, scalability, and performance.  
By separating consensus, data management, and user access, AryaChain ensures that:

- **Full Nodes** remain secure and authoritative,  
- **Service Nodes** scale the network efficiently,  
- **Archive Nodes** preserve transparency and history, and  
- **Light Nodes** bring blockchain participation to everyone.

This structure lays the foundation for future integrations with distributed storage networks (e.g., IPFS or Arweave) and AI-driven analysis modules.

