# To Do List 

## GoBtc-001: Time limit in mining
Mining a block can not take longer than 1 second due to the epoch time update in the block header.
We should avoid mining a block more than 1 second. 
Either we find a way to limit to 1s without adding too many operations (avoiding 1 check per hash of course), or we do an estimate of the number of hash per goroutine calculated in 1s and we loop up to this value. This will require a few seconds of testing before actually starting mining but this is more efficient and reliable. 

## GoBtc-002: Split a Chunk to be calculated by multiple goroutines at the same time
We do not want to work on 1 chunk per goroutine, we want to split one chunk depending on the number of cores on the machine, staying in the 1s time limit.
We basically have to give each chunk a start value between 0 and MAX_NONCE equally divided by the number of goroutines.

## GoBtc-003: Chunk validation
When a successful chunk is found, we want to give it to a "validation entity" before share it on the network. The validation entity will perform basic testing to make sure the block found is correct and will then submit it on the Bitcoin network. In this ticket, we have to make sure that we can send back a chunk over a chan (which has not be done yet). 

## GotBtc-004: Websocket
We do not want to do ugly bashly curl requests anymore. This is highly inneficient. 
Implement a reliable and efficient websocket for the basic operations that this bitcoin miner needs.

## GotBtc-005: Build coinbasetxn and the Merkle Root
Use Bitcoin documentation to build coinbasetxn which will allow us to build the Merkle Root.

## GoBtc-006: Calculate the Target
Use the difficulty to build the target of the BlockHeader. 