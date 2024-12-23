---
layout:     post
title:      Blockchain Fundamentals
subtitle:   Solidity - Smart Contract by Patrick Collins (working in progress...)
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

> Solidity - Smart Contract by Patrick Collins
  Working in progress... Updated on 23/12/2024 :)

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

![image-20241223164055747](/Users/ukrys/Library/Application Support/typora-user-images/image-20241223164055747.png)

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
  - Private Key ||| --> Public Key --> Address

  ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231654634.png)![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231656855.png)

| ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231658981.png) | ![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231657183.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

- mnemonic phrase == secret phrase

- Signing a transaction: A "one way" process. Someone with a private
  key signs a transaction by their private key being hashed with their transaction data. Anyone can then verify this new transaction hash with your public key.

![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231708525.png)

- Secret Phrase --> Private Key ||| --> Public Key --> Address

### 3.3 Gas II: Block Rewards & EIP 1559

**Main Takeaways:** The more people use a chain, the more expensive it is to send transactions.

- Transaction Fee = `Blcok Base Fee Per Gas` +` MaxPriorityFee Per Gas` * `Gas Used`
- Gas Price = The price offered to the miner to purchase this amount of GAS
- Max Priority Gass Fee = the Max gas price + the tip for the miners

- With your transactions, you can set a limit on how much gas you want to  spend 

  <img src="/Users/ukrys/Library/Application Support/typora-user-images/image-20241223171446059.png" alt="image-20241223171446059" style="zoom:50%;" />

- GWEI:  1 Ether = $10^9$ GWei = $10^{18}$ Wei![](https://raw.githubusercontent.com/Ukrys/DFintech_Courses_images/master/202412231715299.png)

- A part of the Transaction Fee gets burnt, and the other goes to the miners

**EIP 1559 Fee Model:** a transaction type -->  www.youtube.com/watch?v=MGemhK9t44Q