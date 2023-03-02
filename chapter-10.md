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


## note on consensus attack

It is important to note that consensus attacks can only affect future consensus, or at best, the most recent past (tens of blocks). Bitcoin’s ledger becomes more and more immutable as time passes. While in theory, a fork can be achieved at any depth, in practice, the computing power needed to force a very deep fork is immense, making old blocks practically immutable. Consensus attacks also do not affect the security of the private keys and signing algorithm (ECDSA). A consensus attack cannot steal bitcoin, spend bitcoin without signatures, redirect bitcoin, or otherwise change past transactions or ownership records. Consensus attacks can only affect the most recent blocks and cause denial-of-service disruptions on the creation of future blocks.


## hard forks

In Blockchain Forks we looked at how the Bitcoin network may briefly diverge, with two parts of the network following two different branches of the blockchain for a short time. We saw how this process occurs naturally, as part of the normal operation of the network and how the network reconverges on a common blockchain after one or more blocks are mined.

There is another scenario in which the network may diverge into following two chains: a change in the consensus rules. This type of fork is called a hard fork, because after the fork the network does not reconverge onto a single chain. Instead, the two chains evolve independently. Hard forks occur when part of the network is operating under a different set of consensus rules than the rest of the network. This may occur because of a bug or because of a deliberate change in the implementation of the consensus rules.


## soft forks

Not all consensus rule changes cause a hard fork. Only consensus changes that are forward-incompatible cause a fork. If the change is implemented in such a way that a non-upgraded client still sees the transaction or block as valid under the previous rules, the change can happen without a fork.

The term soft fork was introduced to distinguish this upgrade method from a "hard fork." In practice, a soft fork is not a fork at all. A soft fork is a forward-compatible change to the consensus rules that allows non-upgraded clients to continue to operate in consensus with the new rules.

One aspect of soft forks that is not immediately obvious is that soft fork upgrades can only be used to constrain the consensus rules, not to expand them. In order to be forward compatible, transactions and blocks created under the new rules must be valid under the old rules too, but not vice versa. The new rules can only limit what is valid; otherwise, they will trigger a hard fork when rejected under the old rules.

Soft forks can be implemented in a number of ways—the term does not specify a particular method, rather a set of methods that all have one thing in common: they don’t require all nodes to upgrade or force non-upgraded nodes out of consensus.

## interesting criticisms of soft forks

#### Technical debt
Because soft forks are more technically complex than a hard fork upgrade, they introduce technical debt, a term that refers to increasing the future cost of code maintenance because of design tradeoffs made in the past. Code complexity in turn increases the likelihood of bugs and security vulnerabilities.

#### Validation relaxation
Non-upgraded clients see transactions as valid, without evaluating the modified consensus rules. In effect, the non-upgraded clients are not validating using the full range of consensus rules, as they are blind to the new rules. This applies to NOP-based upgrades, as well as other soft fork upgrades.

#### Irreversible upgrades
Because soft forks create transactions with additional consensus constraints, they become irreversible upgrades in practice. If a soft fork upgrade were to be reversed after being activated, any transactions created under the new rules could result in a loss of funds under the old rules. For example, if a CLTV transaction is evaluated under the old rules, there is no timelock constraint and it can be spent at any time. Therefore, critics contend that a failed soft fork that had to be reversed because of a bug would almost certainly lead to loss of funds.