
## Factom Overview

Before you use the API calls, here is a quick refresher on how Factom is designed. Please get familiar with the elements of Factom and how they interact. 

Each block in the Factom blockchain has data for multiple chains of entries.  

A chain is a section of entries that are related at the application level. 

A directory block is an index of all of the chains and entries that appear in this given block in the factom blockchain.
The header has useful information such as the key of the previous block, the blocks sequence number (eg height) and a timestamp for the blocks creation. In its header you can get the keymr of the previous block, and trace the blockchain back to the genesis block.

The "entryblocklist" is a list of maps, each of which has two key/value pairs.  The keys are "chainid" and "keymr".  The "chainid" is the application level identifier ofr the chian, and the "keymr" is the merkle root used to identify this specific entry.  This is what will be used to retrieve the entry data.


A block contains an array of records of entries.The keymr for these records allows you to look up a specific entry

Each entry consists of a chain ID to which it belongs, a variable length content field, and an array of external IDs.


## API Summaries

### directory-block

Retrieve the full directory block for a block using its key. 

<br>Parameters: "keymr" is the merkle root of the block and is globally unique to this block.
<br>Request:  Simply includes "keymr"
<br>Response: The response will have two elements, a header and an entry block list. 


### directory-block-head

Returns the keymr of the latest directory block. 

<br>Parameters:  none
<br>Request:
<br>Response:

### heights

Returns various heights that allows you to view the state of the blockchain. 

<br>Parameters: none
<br>Request:
<br>Response:


They are:
directory block height:  the sequence number of highest local directory block
leader height: the sequence number of the leaders highest directory block
entry block height DUNNO
entry height DUNNO
missing entry count DUNNO
entry block height processing DUNNO
entry block height complete DUNNO

### raw-data
<br>Parameters: hash
<br>Request:
<br>Response:

Retrieve an entry (DUNNO?) in raw format, as an string encoded binary blob.

### dblock-by-height
<br>Parameters: height
<br>Request:
<br>Response:

find a directory block given only its height.  This is convenient when you know hte block should exist, but you do not know its merkle root (key).

### ablock-by-height
<br>Parameters: height
<br>Request:
<br>Response:

This allows you to retrieve administrative blocks for any given height.
The admin block contains data related to the identities within the factom system and the decisions the system makes as it builds the block chain. 

### ecblock-by-height

This allows you to retrieve the entry credit block for any given height. These blocks contain entry credit transaction information.

<br>Parameters: height
<br>Request:
<br>Response:


### fblock-by-height 

Retrieve the factoid block for any given height. These blocks contain factoid transaction information.

<br>Parameters: height
<br>Request:
<br>Response:


### receipt 

Retrieve a reciept providing cryptographially verfiable proof that information was recorded in the factom blockchain and that this was subsequently anchored in the bitcoin blockchain.

<br>Parameters: hash
<br>Request:
<br>Response:


### entry-block 

Retrieve a specified entry block given its merkle root key. 

<br>Parameters: keymr
<br>Request:
<br>Response:


### entry

Retrieve a specified entry using its key merkle root.  

<br>Parameters: keymr
<br>Request:
<br>Response:

### pending-entries

Returns an array of the entries that have been submitted but have not been recoreded into the blockchain

<br>Parameters: none
<br>Request:
<br>Response:

### transaction

Retrieve details of a factoid transaction using a transactions hash

<br>Parameters: hash
<br>Request:
<br>Response:

### pending-transactions

Returns an array of factoid transactions that have not yet been recorded in the blockchain, but are known to the system.

<br>Parameters: none
<br>Request:
<br>Response:

### chain-head

Return the keymr of the head of the chain for a chain ID ( the unique hash created when the chain was created)

<br>Parameters: chain ID
<br>Request:
<br>Response:


### entry-credit-balance

Return its current balance for a specific entry credit address

<br>Parameters: address
<br>Request:
<br>Response:


### entry-credit-rate

Returns the number of Factoshis (Factoids *10^-8) that purchase a single Entry Credit. The minimum factoid fees are also determined by this rate, along with how complex the factoid transaction is.

<br>Parameters: none
<br>Request:
<br>Response:

### properties

Retrieve current properties of the Factom system, including the software and the API versions.

<br>Parameters: none
<br>Request:
<br>Response:

### factoid-submit
Submit a factoid transaction in the specified format (describe the format)

<br>Parameters: transaction
<br>Request:
<br>Response:

### commit-chain
When you have produced your chain commit message (How? DUNNO) you and submit it.

<br>Parameters: message
<br>Request:
<br>Response:


### reveal-chain
When you have produced your chain reveal message (How? DUNNO) you and submit it.

<br>Parameters: message
<br>Request:
<br>Response:

### commit-entry
When you have produced your entry commit message (How? DUNNO) you and submit it.

<br>Parameters: message
<br>Request:
<br>Response:

### reveal-entry

When you have produced your entry reveal message (How? DUNNO) you and submit it.

<br>Parameters: message
<br>Request:
<br>Response:

### send-raw-message

<br>Parameters:
<br>Request:
<br>Response:

DUNNO






