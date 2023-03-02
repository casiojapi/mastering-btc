# chapter 10 - mining

## mining base 

The purpose of mining is not the creation of new bitcoin. That’s the incentive system. Mining is the mechanism by which bitcoin’s security is decentralized.

Miners receive two types of rewards in return for the security provided by mining: new coins created with each new block, also known as a block reward or coinbase reward, and transaction fees from all the transactions included in the block. To earn this reward, miners compete to solve a difficult mathematical problem based on a cryptographic hash algorithm. The solution to the problem, called the Proof-of-Work, is included in the new block and acts as proof that the miner expended significant computing effort. The competition to solve the Proof-of-Work algorithm to earn the reward and the right to record transactions on the blockchain is the basis for bitcoin’s security model.


## independent verification of txs

Each node verifies every transaction against a long checklist of criteria:

The transaction’s syntax and data structure must be correct.

Neither lists of inputs or outputs are empty.

The transaction size is less than the maximum allowed size for a block excluding witness data, as shown in tx_check.cpp.

Each output value, as well as the total, must be within the allowed range of values (less than 21m coins, more than the dust threshold).

None of the inputs have hash=0, N=–1 (coinbase transactions should not be relayed).

nLocktime is equal to INT_MAX, or nLocktime and nSequence values are satisfied according to MedianTimePast.

The transaction size in bytes is greater than or equal to 82.

The number of signature operations (SIGOPS) contained in the transaction is less than the signature operation limit.

The unlocking script (scriptSig) can only push numbers on the stack, and the locking script (scriptPubkey) must match IsStandard forms (this rejects "nonstandard" transactions).

A matching transaction in the pool, or in a block in the main branch, must exist.

For each input, if the referenced output exists in any other transaction in the pool, the transaction must be rejected.

For each input, look in the main branch and the transaction pool to find its parent transaction. If the parent transaction is missing for any input, this will be an orphan transaction. Add to the orphan transactions pool, if a matching transaction is not already in the pool.

For each input, if its parent transaction is a coinbase transaction, it must have at least COINBASE_MATURITY (100) confirmations.

For each input, the referenced output must exist and cannot already be spent.

Using the parent transactions to get input values, check that each input value, as well as the sum, are in the allowed range of values (less than 21m coins, more than 0).

Reject if the sum of input values is less than sum of output values.

Reject if transaction fee would be too low (minRelayTxFee) to get into an empty block.

The unlocking scripts for each input must validate against the corresponding output locking scripts.


## coinbase tx

The first transaction in any block is a special transaction, called a coinbase transaction. This transaction is constructed by the miner’s node and contains his reward for the mining effort.

tip: If Jing’s mining node writes the coinbase transaction, what stops Jing from "rewarding" himself 100 or 1000 bitcoin? The answer is that an incorrect reward would result in the block being deemed invalid by everyone else, wasting Jing’s electricity used for Proof-of-Work. Jing only gets to spend the reward if the block is accepted by everyone.


## coinbase data

Coinbase transactions do not have an unlocking script (aka, scriptSig) field. Instead, this field is replaced by coinbase data, which must be between 2 and 100 bytes. Except for the first few bytes, the rest of the coinbase data can be used by miners in any way they want; it is arbitrary data.


## about difficulty - target

The Proof-of-Work must produce a hash that is equal to or less than the target. A higher target means it is less difficult to find a hash that is equal to or below the target. A lower target means it is more difficult to find a hash equal to or below the target. The target and difficulty are inversely related.

The difficulty of mining a bitcoin block is approximately '10 minutes of processing' for the entire network, based on the time it took to mine the previous 2,016 blocks, adjusted every 2,016 blocks. This is achieved by lowering or raising the target.




