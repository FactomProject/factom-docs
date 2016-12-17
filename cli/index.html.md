---
title: CLI Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.


# Authentication

factom-cli ack TxID|FullTx
Returns information about a factoid transaction, or an entry / entry credit transaction

factom-cli addchain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

factom-cli addentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
Add an Entry Credit output to a transaction in the wallet

factom-cli addtxfee TXNAME ADDRESS
Add the transaction fee to an input of a transaction in the wallet

factom-cli addtxinput TXNAME ADDRESS AMOUNT
Add a Factoid input to a transaction in the wallet

factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
Add a Factoid output to a transaction in the wallet

factom-cli backupwallet
Backup the running wallet

factom-cli balance [-r] ADDRESS
If this is an EC Address, returns number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
Buy entry credits

factom-cli composechain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
Create API calls to create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

factom-cli composeentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
Create API calls to create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

factom-cli composetx TXNAME
Compose a wallet transaction into a json rpc object

factom-cli ecrate
It takes this many Factoids to buy an Entry Credit. Displays the larger between current and future rates. Also used to set Factoid fees.

factom-cli exportaddresses
List the private addresses stored in the wallet

factom-cli get allentries|chainhead|dblock|eblock|entry|firstentry|head|heights
Get data about Factom Chains, Entries, and Blocks

factom-cli get allentries [-n NAME1 -N HEXNAME2 ...] CHAINID
Get all of the Entries in a Chain

factom-cli get chainhead [-n NAME1 -N HEXNAME2 ...] CHAINID
Get ebhead by chainid

factom-cli get dblock KEYMR
Get dblock contents by merkle root

factom-cli get eblock KEYMR
Get eblock by merkle root

factom-cli get entry HASH
Get entry by hash

factom-cli get firstentry [-n NAME1 -N HEXNAME2 ...] CHAINID
Get the first entry from a chain

factom-cli get head
Get the latest completed directory block

factom-cli get heights
Get the current heights of various blocks in factomd

factom-cli importaddress ADDRESS [ADDRESS...]
Import one or more secret keys into the wallet

factom-cli importwords '12WORDS'
Import 12 words from Koinify sale into the Wallet

factom-cli listaddresses
List the addresses stored in the wallet

factom-cli listtxs [tmp|all|address|id|range]
List transactions from the wallet or the Factoid Chain

factom-cli listtxs address ECADDRESS|FCTADDRESS
List transaction from the Factoid Chain with a specific address

factom-cli listtxs [all]
List all transactions from the Factoid Chain

factom-cli listtxs id TXID
List transaction from the Factoid Chain

factom-cli listtxs range START END
List the transactions from the Factoid Chain within the specified range

factom-cli listtxs tmp
List current working transactions in the wallet

factom-cli newecaddress
Generate a new Entry Credit Address in the wallet

factom-cli newfctaddress
Generate a new Factoid Address in the wallet

factom-cli newtx TXNAME
Create a new transaction in the wallet

factom-cli properties
Get version information about facotmd and the factom wallet

factom-cli receipt ENTRYHASH
Returns a Receipt for a given Entry

factom-cli rmtx TXNAME
Remove a transaction in the wallet

factom-cli sendfct FROMADDRESS TOADDRESS AMOUNT
Send Factoids between 2 addresses

factom-cli sendtx TXNAME
Send a Transaction to Factom

factom-cli signtx TXNAME
Sign a transaction in the wallet

factom-cli subtxfee TXNAME ADDRESS
Subtract the transaction fee from an output of a transaction in the wallet
