# chapter 1

## intro btc

Behind the scenes, Bitcoin is also the name of the protocol, a peer-to-peer network, and a distributed computing innovation. The bitcoin currency is really only the first application of this invention. Bitcoin represents the culmination of decades of research in cryptography and distributed systems and includes four key innovations brought together in a unique and powerful combination. Bitcoin consists of:

A decentralized peer-to-peer network (the Bitcoin protocol)

A public transaction ledger (the blockchain)

A set of rules for independent transaction validation and currency issuance (consensus rules)

A mechanism for reaching global decentralized consensus on the valid blockchain (Proof-of-Work algorithm)


## full-node vs lightweight

Full-node client
A full client, or "full node," is a client that stores the entire history of Bitcoin transactions (every transaction by every user, ever), manages users' wallets, and can initiate transactions directly on the Bitcoin network. A full node handles all aspects of the protocol and can independently validate the entire blockchain and any transaction. A full-node client consumes substantial computer resources (e.g., more than 125 GB of disk, 2 GB of RAM) but offers complete autonomy and independent transaction verification.

Lightweight client
A lightweight client, also known as a simplified-payment-verification (SPV) client, connects to Bitcoin full nodes (mentioned previously) for access to the Bitcoin transaction information, but stores the user wallet locally and independently creates, validates, and transmits transactions. Lightweight clients interact directly with the Bitcoin network, without an intermediary.


## mnemonic phrase, not seed

The correct term for these backup words is "mnemonic phrase". We avoid the use of the term "seed" to refer to a mnemonic phrase, because even though its use is common it is incorrect.


## satoshi explained

Each bitcoin can be subdivided into 100 million units, each called a "satoshi" (singular) or "satoshis" (plural). Named for bitcoin’s creator, the Satoshi is the smallest unit of bitcoin, equivalent to 0.00000001 BTC.