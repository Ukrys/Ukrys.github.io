---
layout:     post
title:      Blockchain Fundamentals
subtitle:   Solidity - Smart Contract by Patrick Collins
date:       2024-12-21
author:     ukrys
header-img: img/post-bg-bitcoin.jpg
catalog: 	 true
tags:
    - Solidity
    - Blockchain
    - Fintech
---

# BlockChain Fundamentals

> Solidity: Smart Contract by Patrick Collins
>
> Last updated: 24/12/2024

## 1. What is a Blockchain?

### 1.1 Smart Contract

<u>Smart Contracts</u> are a set of instructions executed in a decentralized way without the need for a centralized way without the need for a centralized or third party intermediary.

- one of the main differentiators between the ethereum protocol and the Bitcoin protocol
- Bitcoin is intentionally "turning incomplete"
  - they don't have all the functionalities that a progrmming language would give them 
  - Bitcoin - a store of value VS. Ethereum - both a store of value and a utility to facilitate these decentralized agreements

### 1.2 Oracle Problem

- 'Blockchains are intentionally walled off'
- If we want smart contracts to replace the agreements in out everyday lives, **they need data from the Real World**.
- But blockchains by themselves actually can't interact with the data from the Real World.
  - blockchains are deterministic systems and they're deterministic on purpose

<u>A blockchain oracle</u> is any device or entity that connects a deterministic blockchain with off-chain data.

- We need a decentralized Oracle Network similar to out decentralized blockchain Network.
- The on-chain logic will be decentralized but you also need the off-chain data and computation to be decentralized

### 1.3 Hybrid Smart Conctracts

Combining the on-chain decentralized logic with the off-chain decentralized data and decentralized computation gives rise to <u>Hybrid Smart Conctracts</u>.

- Hybrid Smart Conctracts = On-chain + Off-chain Agreements
- When we say 'smart contracts', we're often using it interchangeably with 'hybrid smart contracts'

### 1.4 Chainlink

- Chainlink: Decentralized Oracle Network

<u>Chainlink</u> is a modular decentralized Oracle Network that can both bring external data and external computation into our smart contracts to make sure they're decentralized end to end while giving them feature richness that we need for our agreements

- customize the smart contracts

### 1.5 Layer 2

- Layer 2 solves the scalability issues
- Two types of true Layer 2:
  - Optimistic Roll-Ups
  - Zero Knowledge Roll-Ups

### 1.6 Web 3

- Web 1: The permissionless open sourced web with static content.
- Web 2: The permissioned web, with dynamic content. Where companies run your agreement: on their servers.
- <u>Web 3</u>: The permissionless web, with dynamic content. Where decentralized censorship resistant networks run your agreement and code. It generally is accompanied by the idea of user owned ecosystems, where the protocols you interact with you also own a portion of, instead of solely being the product.

### 1.7 The value of smart contracts

- **Create Trust Minimized Agreements**
- **Give rise to unbreakable promises**
  - speed, efficiency and transparency  
  - move form a brand-based world to a math-based world
  - build a more fair, more accountable and more transparent financial system

## 2. Other Blockchain Benefits 

### 2.1 Features of Smart Contracts

- Decentralized
  - Many node operators run blockchains
- Transparency & Flexiblity
  - Everybody can see everything that's happening on chain -- No Shady Deals
  - Doesn't mean there's no privacy
    - Blockchain is pseudo Anonymous
- Speed & Efficiency 
- Security & Immutability
- Counterparty Risk Removal
- Trust Minimized Agreements

### 2.2 What have Smart Contracts done so far?

- Defi = Decentralized Finance
- DAOs = Decentralized Autonomous Organizations
- NFTs = Non-Fungible Tokens

### 2.3 Your First Transaction

- Wallet -- MetaMask

- Ethereum Mainnet: the main network of ethereum

- Testnet Faucet: A place to get free testnet ETH

  - sepolia testnet: https://sepolia.etherscan.io/

  > github link: https://github.com/Cyfrin/foundry-full-course-cu?tab=readme-ov-file

### 2.4 Gas I: Introduction to Gas 

- Transaction Fee: Amount paid to the block producer for preocessing the transaction
- Gas Price: Cost per unit of gas specified for the transaction, in Ether and Gwei. The higher the gas price the higher chance of getting included in a  block.
  - The more complicated your transaction is, the more gas you have to pay
  - The more people are sending transactions at the same time on the blockchain, the more expensive gas costs are going to be
- Transaction Fee = Gas Price * Gas Used

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231441424.png)![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231444937.png)

## 3. How do Blockchains work?

### 3.1 Blockchain demo

> demo: https://andersbrownworth.com/blockchain/

<u>Hash</u> is a A unique fixed length string, meant to identifya piece of data. They are created by placing said data intoa "hash function"

- Ethereum uses `Keccak256` as its hash function (in SHA family)
- Block: A list of transactions mined together 
- Hash of Block: **Block + Nonce + Data ( + Prev.)**
- Nonce: A "number used once" to find the solution to the blockchain problem
- **Mine**: Find a nonce that when hashed at block number with the data it would start with leading zeros
- Different blockchains have different problems to solve but the concept is going to be the same

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231624669.png)

- Genesis Block: The first block in a blockchain

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231735383.png)

- peers compare the hash of each block to decide which one is acting properly and which one is acting maliciously, the block with hash different from the majority would be out of the chain.
- Decentralized: Having no single point of authority

### 3.2 Signing Transactions

> in the graph above, 'How do we know Darcy who was the one to send $25 to Bingley?'

- **Private Key:** Only known to the key holder, it's used to 'sign' transactions

  ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231650094.png)

  - use Elliptic Curve Digital Signature Algorithm to get the 'Public/ Private Key Pairs'
  - We use private key as a password to quote & unquote digitally sign transactions and then people can verify them with the public key
  - But others cannot derive your private key according to the Message Signature

- Public Key: is derived from your private key. Anyone can "see" it, and use it to verify that a transaction came from you.

  - Your Address is derived from the private key
  - Private Key \|\|\| --> Public Key --> Address

  ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231654634.png)![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231656855.png)

| ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231658981.png) | ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231657183.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

- mnemonic phrase == secret phrase

- Signing a transaction: A "one way" process. Someone with a private
  key signs a transaction by their private key being hashed with their transaction data. Anyone can then verify this new transaction hash with your public key.

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231708525.png)

- Secret Phrase --> Private Key \|\|\| --> Public Key --> Address

### 3.3 Gas II: Block Rewards & EIP 1559

**Main Takeaways:** The more people use a chain, the more expensive it is to send transactions.

- Transaction Fee = `Blcok Base Fee Per Gas` +` MaxPriorityFee Per Gas` * `Gas Used`
- Gas Price = The price offered to the miner to purchase this amount of GAS
- Max Priority Gass Fee = the Max gas price + the tip for the miners
- With your transactions, you can set a limit on how much gas you want to  spend 
- GWEI:  1 Ether = $10^9$ GWei = $10^{18}$ Wei![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231715299.png)

- A part of the Transaction Fee gets burnt, and the other goes to the miners

**EIP 1559 Fee Model:** a transaction type -->  [www.youtube.com/watch?v=MGemhK9t44Q](EIP 1559 Fee Model)

## 4. High-Level Blockchain Fundamentals

- Node: A single instance in a decentralized network
- Anyone can participate in the network
- Blockchains are resilient
- Consensus: is the mechanism used to agree on the state of a blockchain
  - a consensus protocol can be roughly divided into 2 pieces:
    - Chain Selection
    - Sybil Resistance

- Sybil Resistance: the ability of a network to defend against **Sybil attacks**, where a single entity creates multiple fake or malicious identities (nodes, accounts, or addresses) to gain disproportionate influence or control over the system. Sybil resistance mechanisms are critical for maintaining the integrity, fairness, and decentralization of blockchain systems.

  > ### **What is a Sybil Attack?**
  >
  > A Sybil attack occurs when an attacker creates and operates many fake identities (or entities) in a network to manipulate its functioning. In the context of blockchain, this could involve:
  >
  > - Overpowering consensus mechanisms.
  > - Manipulating voting processes.
  > - Flooding the network with spam transactions.
  >
  > For example, if a blockchain uses a voting-based consensus, an attacker could create numerous identities to gain a majority in the voting process and take control of the network.
  >
  > ------
  >
  > ### **Why is Sybil Resistance Important?**
  >
  > Blockchains aim to be **decentralized and trustless**, meaning no single party should have undue influence over the system. Sybil attacks threaten this principle by allowing a malicious actor to:
  >
  > - **Disrupt consensus**: Control a significant portion of nodes to tamper with transaction validation or block creation.
  > - **Launch 51% attacks**: Manipulate the blockchain ledger, double-spend, or censor transactions.
  > - **Undermine fairness**: Skew outcomes in decentralized applications (e.g., in governance or resource allocation).
  >
  > Without Sybil resistance, blockchains and decentralized systems would be inherently vulnerable to manipulation.
  >
  > ------
  >
  > ### **Mechanisms for Sybil Resistance**
  >
  > To prevent Sybil attacks, blockchain networks implement mechanisms that make it expensive or difficult for an attacker to create and control a large number of fake identities. Common Sybil resistance approaches include:
  >
  > #### 1. **Proof-of-Work (PoW)**
  >
  > - PoW requires participants (miners) to solve complex computational puzzles to validate transactions and create new blocks. This makes it expensive and resource-intensive to control a large portion of the network.
  > - Example: Bitcoin and Ethereum (prior to Ethereum 2.0).
  >
  > #### 2. **Proof-of-Stake (PoS)**
  >
  > - PoS requires participants to lock up a certain amount of cryptocurrency as a "stake" to validate transactions. The more cryptocurrency staked, the higher the chance of being selected as a validator.
  > - Creating multiple fake identities would require a significant amount of cryptocurrency, making Sybil attacks costly.
  > - Example: Ethereum (after Ethereum 2.0), Cardano.
  >
  > #### 3. **Proof-of-Authority (PoA)**
  >
  > - In PoA, only a limited number of pre-approved validators are allowed to participate in consensus. The validators are known and trusted entities, reducing the risk of Sybil attacks.
  > - Example: VeChain, some private blockchains.
  >
  > #### 4. **Proof-of-Identity (PoI)**
  >
  > - PoI ties blockchain identities to real-world identities or credentials. This makes it hard for attackers to create numerous fake identities.
  > - Example: Civic (a decentralized identity platform).
  >
  > #### 5. **Social or Reputation-Based Systems**
  >
  > - Some decentralized systems use social graphs or reputation scores to identify and limit malicious actors. A user’s influence depends on their real-world trust or connections.
  > - Example: BrightID (a decentralized identity protocol).
  >
  > #### 6. **Economic Incentives and Penalties**
  >
  > - Networks may require participants to **stake funds** or pay fees to join the system. If malicious behavior is detected, their funds are slashed or forfeited.
  > - Example: Slashing in PoS systems.
  >
  > #### 7. **Resource Constraints**
  >
  > - Limiting the number of identities a single entity can control by tying participation to limited resources like bandwidth, storage, or trusted hardware.
  > - Example: Filecoin (using storage as a resource).
  >
  > ------
  >
  > ### **Real-World Applications of Sybil Resistance**
  >
  > 1. **Decentralized Governance**:
  >    - Voting systems in DAOs (Decentralized Autonomous Organizations) often rely on Sybil-resistant mechanisms to prevent one entity from dominating decisions.
  > 2. **Decentralized Identity (DID)**:
  >    - Sybil resistance is crucial in DID systems to ensure each identity is unique and valid.
  > 3. **Resource Allocation**:
  >    - Systems like airdrops or token distributions use Sybil resistance to prevent abuse by fake accounts.
  > 4. **Reputation Systems**:
  >    - Decentralized marketplaces or platforms use Sybil resistance to prevent fake reviews or reputation manipulation.
  >
  > ------
  >
  > ### **Challenges in Sybil Resistance**
  >
  > While existing mechanisms provide some level of security, there are challenges:
  >
  > - **Cost of decentralization**: Some mechanisms (like PoW) are resource-intensive and environmentally costly.
  > - **Centralization risks**: PoA and identity-based approaches may introduce centralization, undermining blockchain's decentralized nature.
  > - **Scalability**: Some Sybil resistance mechanisms may hinder network scalability.
  > - **Fairness**: Wealth-based systems (like PoS) may favor the rich, leading to inequality.
  >
  > ------
  >
  > ### **Conclusion**
  >
  > Sybil resistance is an essential aspect of blockchain security, ensuring that the network remains decentralized, fair, and robust against attacks. By making it expensive, resource-intensive, or difficult to create fake identities, blockchain systems can uphold their trustless nature and maintain integrity. Different blockchains adopt varying approaches based on their goals, trade-offs, and target use cases.

- PoW (Proof of Work): figure out who th block author is and be Sybil resistant
  - Miners
  - a piece of consensus algorithm
- Nakamoto consensus algorithm
  - includes the combination of the longest chain Rule and PoW
- Block Confirmation: the number of additional blocks added on after transactions went through in a block
-  PoS (Proof of Stake): put up collateral as a sybil resistance mechanism
  - Validators
  - uses much less energy --- only one node has to solve the math problem and others only need to validate it.
- Layer 1: Base layer blockchain implementation 
- Layer 2: Any network/application built on top of a layer 1
- Rollups: roll up transactions into a Layer 1
  - solve some scalability issues
  - e.g., arbitrum and optimism 
  - difference from side chains: side chains derive their security from their own protocols



## 5. Layer 1's, Layer 2's and Rollups

### 5.1 Layer 1

Layer 1: base layer of the blockchain ecosystem in which transactions are executed and confirmed

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412241452916.png)

### 5.2 Layer 2

Laer 2: Secondary framework or protocol that is built on top of the layer 1 and then hooks back into it

- Applications
  - Chainlink: a decentralized Oracle Network that brings off-chain data onchain in a decentralized way
- Event Indexing networks:
  - Graph: enables applications to access onchain data
- L2 Chain or Roll-up: Scaling solution that increases the number of transactions on the L1 chain

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412241501647.png)

### 5.3 Roll-ups

**Blockchain Trilema:** a blockchain system can only ever have two out of three properties (decentralization, security and scalability)

- Etheruem has a scalability problem that it can only process approximately 15 transactions per second
- solved by Rollups!!

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412241507401.png)

When a user submits a transaction to a rollup such as ZK sync an operator picks up this transaction, order the transaction with other peoples' transactions and then bundle them together, compress them and then submit them back to the L1 such as Ethereum.

- The gas cost associated with the transaction is split among all of the users, all of the transactions in the transaction batch.

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412241627715.png)

- Rollups helps scale ethereum

### 5.4 Optimistic vs. ZK(zero-knowledge) Rollups

**Optimistic Rollups:** 

- Assume transactions are legitimate by default
- Use fraud proof to verify correctness in the case of a dispute
  - involves the operator playing a call and response game with another operator until they narrow down the dispute to a single computational step, which is then executed on the L1 and if executing this step results in a different outcome, the state of the blockchain is different. The challenging or disputing operator wins the challenge.
  - Slashing: the tokens are taken away if the node isn't acting honestly.

**ZK Rollups:**

- Use validity or zk proof to verify transaction correctness
- Zk proofs: Algorithm that verifies that a 'prover' knows something to a 'verifier' without revealing the information
  - The prover is an operator and the verifier is an L1 contract
  - For each transaction batch that is submitted to the L1, a validity or ZK proof is computed by approver and verified by the verifier or the L1 contract

### 5.5 Sequencer

Sometimes a suquencer is centralized, controlled by a centralized entity.

- Lead to things like censorship, which would block transactions onchain

> A **sequencer** in the context of blockchain is a specialized entity or mechanism responsible for determining the order of transactions in a blockchain or a blockchain layer, often in Layer 2 (L2) scaling solutions like optimistic rollups or zk-rollups. The sequencer plays a critical role in ensuring the smooth operation of these systems by organizing transaction data and submitting it to the underlying Layer 1 (L1) blockchain.
>
> ### Key Functions of a Sequencer
>
> 1. **Transaction Ordering**:  
>    The sequencer determines the order in which transactions are processed and included in a block or a batch. This ordering is crucial for ensuring fairness and consistency across the network.
>
> 2. **Fast Confirmation**:  
>    In Layer 2 solutions, a sequencer can provide near-instantaneous confirmation of transactions since it can process them off-chain without waiting for L1 finality. This improves the user experience.
>
> 3. **Batch Submission**:  
>    The sequencer aggregates multiple transactions into a single batch and submits this batch to the L1 blockchain. This reduces the cost of recording transactions on the main blockchain.
>
> 4. **Execution of Smart Contracts**:  
>    In some Layer 2 solutions, the sequencer is responsible for executing smart contracts and managing the state of the rollup.
>
> 5. **Preventing Congestion**:  
>    By aggregating and ordering off-chain transactions, the sequencer helps reduce congestion and transaction fees on the Layer 1 blockchain.
>
> ---
>
> ### Role of Sequencers in Layer 2 Rollups
>
> In Layer 2 systems like **Optimistic Rollups** or **zk-Rollups**, the sequencer plays a pivotal role:
>
> - **Optimistic Rollups**:  
>   The sequencer processes transactions and posts the transaction data or state root to the L1 blockchain. Fraud proofs can be used to challenge incorrect state updates.
>
> - **zk-Rollups**:  
>   The sequencer batches transactions and generates a cryptographic proof (zero-knowledge proof) to verify the validity of the batch. This proof is then submitted to L1.
>
> ---
>
> ### Centralization Concerns
>
> Sequencers in many Layer 2 systems are often centralized entities, which introduces some degree of centralization risk. However, mechanisms are being developed to decentralize sequencers and ensure fairness, such as:
>
> - **Decentralized Sequencers**: Using a network of validators or operators to perform the sequencer's role.
> - **Fallback Mechanisms**: Allowing users to directly submit transactions to L1 if the sequencer behaves maliciously or goes offline.
> - **MEV (Maximal Extractable Value) Mitigation**: Preventing sequencers from exploiting their position to reorder transactions for profit.
>
> ---
>
> ### Summary
>
> A **sequencer** is a critical component of many blockchain scaling solutions, especially Layer 2 rollups, where it determines transaction order, enables faster confirmations, and reduces costs by batching transactions. While many current implementations are centralized, efforts are underway to decentralize sequencers to ensure greater trust and resilience.



### 5.6 Rollup Stages

> refer to: [l2beat.com/scaling/summary]()

The stage of a rollup is a categorization framework based on vitalic proposed milestones. It's an opinionated assessment on the maturity of the rollup by.

- Stage 0: Full training wheels
  - Centralized management
  - Security Council make decisions
  - Open source software for data availability 
- Stage 1: Enhanced Rollup Governance
  - Governed by smart contracts
  - Security Council for bug resolution
  - Decentralized fraud/validity proof system
  - Users have $\gt7$ days to exit in the case of unwanted upgrades

- Stage 2: No Training Wheels
  - Completely decentralized 
  - Smart Contracts manage the rollup
  - Full decentralized & permissionless fraud/validity proof system
  - Ample time to exit system in the case of upgrades
  - Security Council address errors adjudicated on-chain
  - User protection against governance attacks



### 5.7 Transaction demo on ZK Sync

**Bridging Funds:** Taking funds from one chain and getting them on the other chain

> (http://portal.zksync,io/bridge/)[]

- Locking & Unlocking method:

  ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412241554786.png)

- Minting & Burning method:

  ![image-20241224155536152](/Users/ukrys/Library/Application Support/typora-user-images/image-20241224155536152.png)