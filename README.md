flo-mtx
=======

Florincoin Multiple Transaction Protocol

Why?
---
There is a need for a method where applications can reliably write to the blockchain without incurring a fee. There is also the eventual problem of bloating the blockchain with data as well as UTXO bloat. The metacoin-mtx approach solves both problems by requiring an amount of Florin to be held in storage and used for each application.

What?
-----
The Florincoin blockchain allows for metadata to be stored in the blockchain. This unique feature allows a multitude of protocols to be built upon Florincoin. Unfortunately, there are limits on how many fee-less transactions can be sent to the network. The priority equation in particular imposes hard limits on how many fee-less transactions can be sent in a single block. 

The proposed solution is for each application to maintain a balance of coins that can be spent in sequence as requests to write to the blockchain are made. These transactions are sent to the network and maintain a priority high enough such that they do not end up "in limbo" forever. 

The problem:

Let's say the Aterna Love application wishes to write 100 transactions to the blockchain. Using the classical approach, some FLO could be sent from the application's address to the same  address in a "send-to-self" transaction. The problem with this approach is that each of the subsequent transactions after the first has a much lower priority as it isn't confirmed yet in a block. In general, miners will only include one of these transactions in a block, so it could take more than an hour for the last transaction to be placed into a block. Worse, transaction malleability attacks can be used to invalidate any of the transactions in the chain. This attack would essentially amount to a DDOS on the site.

The solution:
A preliminary "multi-genesis" transaction must be made to create a new basis transaction for each coin. Let's say we want to use 100 coins for the mtx protocol:

A "multi-genesis" transaction is created that lists 100 spends of 1 coin to the application's address, creating 100 individual unspent transactions. Each new blockchain write request is sent using the next transaction that has an unspent output. These transactions have higher priority because they are spent from an older transaction, and they do not rely on unconfirmed outputs. 

This requires at least 100 FLO to be "saved" or "held". If the application requires more writes per minute, the amount of FLO required in savings is higher. Therefore, the amount of FLO required in savings is directly proportional to how many writes per minute the application wants to make. 

Each transaction is sent from the application's main address back to that address, so after 1 block, the transaction is spendable again under a new nTxid.

When?
-----
This protocol is currently in development. The latest major update was version 0.01 on 2014-02-21. You can read the changelog here.

Where?
------
In the future, places this protocol is in use will be posted under this section. If you notice your application isn't listed here, please contact us to have that resolved!

