# chapter 2

## change address (back to owner)

Many bitcoin transactions will include outputs that reference both an address of the new owner and an address of the current owner, called the change address. This is because transaction inputs, like currency notes, cannot be divided. If you purchase a $5 US dollar item in a store but use a $20 US dollar bill to pay for the item, you expect to receive $15 US dollars in change. The same concept applies to bitcoin transaction inputs. If you purchased an item that costs 5 bitcoin but only had a 20 bitcoin input to use, your wallet would create a single transaction that sends two outputs, one output of 5 bitcoin to the store owner and one output of 15 bitcoin back to yourself as change (less any applicable transaction fee). Importantly, the change address does not have to be the same address as that of the input and for privacy reasons is often a new address from the owner’s wallet.

## fact about coinbase tx

Each miner includes a special transaction in their block, one that pays their own Bitcoin address the block reward (currently 6.25 newly created bitcoin) plus the sum of transaction fees from all the transactions included in the block. If they find a solution that makes that block valid, they "win" this reward because their successful block is added to the global blockchain and the reward transaction they included becomes spendable. Jing, who participates in a mining pool, has set up his software to create new blocks that assign the reward to a pool address. From there, a share of the reward is distributed to Jing and other miners in proportion to the amount of work they contributed in the last round.


