---
layout:     post
title:      Blockchain Foundations
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

# BlockChain Foundation

> Solidity - Smart Contract by Patrick Collins

## 01 Basic Concepts 

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

