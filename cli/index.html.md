---
title: CLI Reference

language_tabs:

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.


# CLI

##ack
```factom-cli ack TxID|FullTx
``` <br><br>
Returns information about a factoid transaction, or an entry / entry credit transaction

##addchain
```factom-cli addchain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
``` <br><br>
Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

##addentry
```factom-cli addentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
``` <br><br>
Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

##addtxecoutput
```factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
```<br><br>
Add an Entry Credit output to a transaction in the wallet

##addtxfee
```factom-cli addtxfee TXNAME ADDRESS
```<br><br>
Add the transaction fee to an input of a transaction in the wallet

##addtxinput
```factom-cli addtxinput TXNAME ADDRESS AMOUNT
```<br><br>
Add a Factoid input to a transaction in the wallet

##addtxoutput
```factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
```<br><br>
Add a Factoid output to a transaction in the wallet

##backupwallet
```factom-cli backupwallet
```<br><br>
Backup the running wallet

##balance
```factom-cli balance [-r] ADDRESS
```<br><br>
If this is an EC Address, returns number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

##buyec
```factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
```balance<br><br>
Buy entry credits

##composechain
```factom-cli composechain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
```<br><br>
Create API calls to create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

##composeentry
```factom-cli composeentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
```<br><br>
Create API calls to create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

##composetx
```factom-cli composetx TXNAME
```<br><br>
Compose a wallet transaction into a json rpc object

##ecrate
```factom-cli ecrate
```<br><br>
It takes this many Factoids to buy an Entry Credit. Displays the larger between current and future rates. Also used to set Factoid fees.

##exportaddresses
```factom-cli exportaddresses
```<br><br>
List the private addresses stored in the wallet

##get
```factom-cli get allentries|chainhead|dblock|eblock|entry|firstentry|head|heights
```<br><br>
Get data about Factom Chains, Entries, and Blocks

##get allentries
```factom-cli get allentries [-n NAME1 -N HEXNAME2 ...] CHAINID
```<br><br>
Get all of the Entries in a Chain

##get chainhead
```factom-cli get chainhead [-n NAME1 -N HEXNAME2 ...] CHAINID
```<br><br>
Get ebhead by chainid

##get dblock
```factom-cli get dblock KEYMR
```<br><br>
Get dblock contents by merkle root

##get eblock
```factom-cli get eblock KEYMR
```<br><br>
Get eblock by merkle root

##get entry
```factom-cli get entry HASH
```<br><br>
Get entry by hash

##get firstentry
```factom-cli get firstentry [-n NAME1 -N HEXNAME2 ...] CHAINID
```<br><br>
Get the first entry from a chain

##get head
```factom-cli get head
```<br><br>
Get the latest completed directory block

##get heights
```factom-cli get heights
```<br><br>
Get the current heights of various blocks in factomd

##importaddress
```factom-cli importaddress ADDRESS [ADDRESS...]
```<br><br>
Import one or more secret keys into the wallet

##importwords
```factom-cli importwords '12WORDS'
```<br><br>
Import 12 words from Koinify sale into the Wallet

##listaddresses
```factom-cli listaddresses
```<br><br>
List the addresses stored in the wallet

##listtxs
```factom-cli listtxs [tmp|all|address|id|range]
```<br><br>
List transactions from the wallet or the Factoid Chain

##listtxs address
```factom-cli listtxs address ECADDRESS|FCTADDRESS
```<br><br>
List transaction from the Factoid Chain with a specific address

##listtxs [all]
```factom-cli listtxs [all]
```<br><br>
List all transactions from the Factoid Chain

##listtxs id 
```factom-cli listtxs id TXID
```<br><br>
List transaction from the Factoid Chain

##listtxs range 
```factom-cli listtxs range START END
```<br><br>
List the transactions from the Factoid Chain within the specified range

##listtxs tmp
```factom-cli listtxs tmp
```<br><br>
List current working transactions in the wallet

##newecaddress
```factom-cli newecaddress
```<br><br>
Generate a new Entry Credit Address in the wallet

##newfctaddress
```factom-cli newfctaddress
```<br><br>
Generate a new Factoid Address in the wallet

##newtx
```factom-cli newtx TXNAME
```<br><br>
Create a new transaction in the wallet

##properties
```factom-cli properties
```<br><br>
Get version information about facotmd and the factom wallet

##receipt
```factom-cli receipt ENTRYHASH
```<br><br>
Returns a Receipt for a given Entry

##rmtx
```factom-cli rmtx TXNAME
```<br><br>
Remove a transaction in the wallet

##sendfct
```factom-cli sendfct FROMADDRESS TOADDRESS AMOUNT
```<br><br>
Send Factoids between 2 addresses

##sendtx
```factom-cli sendtx TXNAME
```<br><br>
Send a Transaction to Factom

##signtx
```factom-cli signtx TXNAME
```<br><br>
Sign a transaction in the wallet

##subtxfee
```factom-cli subtxfee TXNAME ADDRESS
```<br><br>
Subtract the transaction fee from an output of a transaction in the wallet
