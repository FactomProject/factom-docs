
## API Summaries

Search for the text DUNNO for things that I'm not clear on that need Michael or Brian to weigh in.

### directory-block
parameters: keymr

Each block in the Factom blockchain has data for multiple chains of entries.  A chain is a section of entries that are related at the application level.  A directory block is an index of all of the chains and entries that appear in this given block in the factom blockchain.

This API will retrieve the directory block for a given block using its key.  The key, a parameter named "keymr" is the merkle root of the block and is globally unique to this block.

The response will have two elements, a header and an entry block list. The header has useful information such as the key of the previous block, the blocks sequence number (eg height) and a timestamp for the blocks creation.

The "entryblocklist" is a list of maps, each of which has two key/value pairs.  The keys are "chainid" and "keymr".  The "chainid" is the application level identifier ofr the chian, and the "keymr" is the merkle root used to identify this specific entry.  This is what will be used to retrieve the entry data.

### directory-block-head
parameters  none

This API returns the keymr of the latest directory block.   Using this keymr you can call the directory-block API to retrieve the full block.  In its header you can get the keymr of the previous block, and in this way walk the blockchain back to the genesis block.

### heights
parameters: none

This API retruns verious heights that tell you details about the state of the block chain. 

They are:
directory block height:  the sequence number of highest local directory block
leader height: the sequence number of the leaders highest directory block
entry block height DUNNO
entry height DUNNO
missing entry count DUNNO
entry block height processing DUNNO
entry block height complete DUNNO

### raw-data
parameters: hash

This API allows you to retrieve an entry (DUNNO?) in raw format, as an string encoded binary blob.

### dblock-by-height
parameters: height

This API allows you to find a directory block given only its height.  This is convenient when you know hte block should exist, but you do not know its merkle root (key).

### ablock-by-height
parameters: height

This allows you to retrieve administrative blocks for any given height.
The admin block contains data related to the identities within the factom system and the decisions the system makes as it builds the block chain. 

### ecblock-by-height
parameters: height

This allows you to retrieve the entry credit block for any given height. These blocks contain entry credit transaction information.

### fblock-by-height 
parameters: height

This allows you to retrieve the factoid block for any given height. These blocks contain factoid transaction information.

### receipt 
parameters: hash

This API allows you to retrieve a reciept providing cryptographially verfiable proof that information was recorded in the factom blockchain and that this was subsequently anchored in the bitcoin blockchain.

### entry-block 
parameters: keymr

This API Allows you to retrieve a specified entry block given its merkle root key.   The block will contain an array of records of entries that have been recorded.  The keymr provided in these records allows you to look up a specific entry using the entry API.

### entry
parameters: keymr

This API allows you to retrieve a specified entry using its key merkle root.  Each entry consists of a chain ID to which it belongs, a variable length content field, and an array of external IDs.

### pending-entries
parameters: none

This API will give you an array of the entries that have been submitted but have not yet been recoreded into the blockchain DUNNO is that right?

### transaction
parameters: hash

An API to retrieve the details of a factoid transaction.  It requires the transactions hash

### pending-transactions
parameters: none

This returns the array of factoid transactions thath ave not yet been recorded in the blockchain, but are known to the system.

### chain-head
parameters: chain ID

This API takes the chain ID (which is hash created when the chain was created) and  gives the keymr of the head of the chain.

### entry-credit-balance
parameters: address

For a given entry credit address, this API will return its current balance.

### entry-credit-rate
parameters: none

This call returns the number of Factoshis (Factoids *10^-8) that purchase a single Entry Credit. The minimum factoid fees are also determined by this rate, along which how complex the factoid transaction is.

### properties
parameters: none

The current properties of the factom system are returned by this call, including the version of the software and the version of the API.

### factoid-submit
parameters: transaction

This API lets you submit a factoid transaction in the specified format (DUNNO the format!)

### commit-chain
parameters: message

When you have produced your chain commit message (How? DUNNO) you and submit it using this API.

### reveal-chain
parameters: message

When you have produced your chain reveal message (How? DUNNO) you and submit it using this API.

### commit-entry
parameters: message

When you have produced your entry commit message (How? DUNNO) you and submit it using this API.

### reveal-entry
parameters: message

When you have produced your entry reveal message (How? DUNNO) you and submit it using this API.

### send-raw-message

DUNNO






