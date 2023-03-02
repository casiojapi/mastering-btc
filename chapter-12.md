# chapter 12 - blockchain applications

## building blocks for an application (primitives)

##### Building Blocks (Primitives)
When operating correctly and over the long term, the Bitcoin system offers certain guarantees, which can be used as building blocks to create applications. These include:

#### No Double-Spend
The most fundamental guarantee of bitcoin’s decentralized consensus algorithm ensures that no UTXO can be spent twice.

#### Immutability
Once a transaction is recorded in the blockchain and sufficient work has been added with subsequent blocks, the transaction’s data becomes immutable. Immutability is underwritten by energy, as rewriting the blockchain requires the expenditure of energy to produce Proof-of-Work. The energy required and therefore the degree of immutability increases with the amount of work committed on top of the block containing a transaction.

#### Neutrality
The decentralized Bitcoin network propagates valid transactions regardless of the origin or content of those transactions. This means that anyone can create a valid transaction with sufficient fees and trust they will be able to transmit that transaction and have it included in the blockchain at any time.

#### Secure Timestamping
The consensus rules reject any block whose timestamp is too far in the past or future. This ensures that timestamps on blocks can be trusted. The timestamp on a block implies an unspent-before guarantee for the inputs of all included transactions.

#### Authorization
Digital signatures, validated in a decentralized network, offer authorization guarantees. Scripts that contain a requirement for a digital signature cannot be executed without authorization by the holder of the private key implied in the script.

#### Auditability
All transactions are public and can be audited. All transactions and blocks can be linked back in an unbroken chain to the genesis block.

#### Accounting
In any transaction (except the coinbase transaction) the value of inputs is equal to the value of outputs plus fees. It is not possible to create or destroy bitcoin value in a transaction. The outputs cannot exceed the inputs.

#### Nonexpiration
A valid transaction does not expire. If it is valid today, it will be valid in the near future, as long as the inputs remain unspent and the consensus rules do not change.

#### Integrity
A bitcoin transaction signed with SIGHASH_ALL or parts of a transaction signed by another SIGHASH type cannot be modified without invalidating the signature, thus invalidating the transaction itself.

#### Transaction Atomicity
Bitcoin transactions are atomic. They are either valid and confirmed (mined) or not. Partial transactions cannot be mined and there is no interim state for a transaction. At any point in time a transaction is either mined, or not.

#### Discrete (Indivisible) Units of Value
Transaction outputs are discrete and indivisible units of value. They can either be spent or unspent, in full. They cannot be divided or partially spent.

#### Quorum of Control
Multisignature constraints in scripts impose a quorum of authorization, predefined in the multisignature scheme. The M-of-N requirement is enforced by the consensus rules.

#### Timelock/Aging
Any script clause containing a relative or absolute timelock can only be executed after its age exceeds the time specified.

#### Replication
The decentralized storage of the blockchain ensures that when a transaction is mined, after sufficient confirmations, it is replicated across the network and becomes durable and resilient to power loss, data loss, etc.

#### Forgery Protection
A transaction can only spend existing, validated outputs. It is not possible to create or counterfeit value.

#### Consistency
In the absence of miner partitions, blocks that are recorded in the blockchain are subject to reorganization or disagreement with exponentially decreasing likelihood, based on the depth at which they are recorded. Once deeply recorded, the computation and energy required to change makes change practically infeasible.

#### Recording External State
A transaction can commit a data value, via OP_RETURN, representing a state transition in an external state machine.

#### Predictable Issuance
Less than 21 million bitcoin will be issued, at a predictable rate.
