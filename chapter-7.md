# chapter 7 - advanced transactions and scripting

## multisignature

Multisignature scripts set a condition where N public keys are recorded in the script and at least M of those must provide signatures to unlock the funds. 

M-of-N scheme, where N is the total number of keys and M is the threshold of signatures required for validation. 


## pay-to-script-hash (P2SH)

Pay-to-Script-Hash (P2SH) was introduced in 2012 as a powerful new type of transaction that greatly simplifies the use of complex transaction scripts.

P2SH or Pay-to-Script-Hash addresses are a special type of address in Bitcoin, which allows you to create addresses that can receive or send transactions in which a series of instructions must be followed in order to unlock the balances that contain those addresses.


## useful stuff about P2SH

 + The P2SH feature offers the following benefits compared to the direct use of complex scripts in locking outputs:
 + Complex scripts are replaced by shorter fingerprints in the transaction output, making the transaction smaller.
 + Scripts can be coded as an address, so the sender and the sender’s wallet don’t need complex engineering to implement P2SH.
 + P2SH shifts the burden of constructing the script to the recipient, not the sender.
 + P2SH shifts the burden in data storage for the long script from the output (which additionally to being stored on the blockchain is in the UTXO set) to the input (only stored on the blockchain).
 + P2SH shifts the burden in data storage for the long script from the present time (payment) to a future time (when it is spent).
 + P2SH shifts the higher transaction fee costs of a long script from the sender to the recipient, who has to include the long redeem script to spend it.


## p2sh fun facts

You are not able to put a P2SH inside a P2SH redeem script, because the P2SH specification is not recursive.

warning: P2SH locking scripts contain the hash of a redeem script, which gives no clues as to the content of the redeem script itself. The P2SH transaction will be considered valid and accepted even if the redeem script is invalid. You might accidentally lock bitcoin in such a way that it cannot later be spent.