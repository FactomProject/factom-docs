---
title: CLI Reference

language_tabs:
  - shell

toc_footers:
  - <a href='../api'>Factom API Documentation</a>
  - <a href='../cli'>Factom CLI Documentation</a>
  - <a href='../wallet'>Factom Foundation Wallet Documentation</a>
  - <a href='https://docs.factom.com'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/factomproject'>Factom on GitHub</a>
  - <a href='https://factom.com'>Back to FACTOM.COM</a>
  
includes:
  - cli guides
  - before we begin
  - backup wallet
  - install ff
  - run ff
  - generate fa address
  - generate ec address
  - send and receive fct
  - convert fct to ec
  - redeem koinify fct
  - import private key
  - verify balances
  - create chain
  - make entry
  - read entries
  - papermill
  - useful tools

search: true
---

# Introduction

Welcome to the Factom CLI. <i>factom-cli</i> is a command line interface program for interacting with <i>factomd</i>  and <i>factom-walletd</i>.

```shell
factom-cli [OPTIONS] SUBCOMMAND [OPTIONS]
```


# Flags

##-e -x


The addentry subcommands support the -e and -x flags for adding external ids to the Entries they create. Multiple -e and -x flags may be used, and -e and -x may be used in combination. -e string will encode the string as binary and set it as the next external id. -x hexstring will decode the hexstring into binary and set it as the next external id.

```shell
$
```

##-n -h


The get firstentry, get chainhead, and get allentries subcommands support the -n and -h flags for using Chain Names as an alternative for providing a ChainID. The Chain Name is the combination of External IDs on the first Entry in the Chain.

```shell
$ factom-cli get chainhead -n test -h 3031
```

##-r

The r flag tells factom-cli to try and resolve a public Factoid or Entry Credit Address from a DNS name registered through Netki.

```shell
$ factom-cli sendfct -r $my_factoid_address factom.michaeljbeam.me
```

# CLI Commands

##ack

```shell
factom-cli ack TxID|FullTx
```
Example:
```shell
factom-cli ack TxID|FullTx
```
Returns information about a factoid transaction, or an entry / entry credit transaction

##addchain

```shell 
factom-cli addchain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
``` 

Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

##addentry

```shell 
factom-cli addentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
```
Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

##addtxecoutput

```shell
factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
```
Add an Entry Credit output to a transaction in the wallet

##addtxfee

```shell
factom-cli addtxfee TXNAME ADDRESS
```
Add the transaction fee to an input of a transaction in the wallet

##addtxinput

```shell
factom-cli addtxinput TXNAME ADDRESS AMOUNT
```
Add a Factoid input to a transaction in the wallet

##addtxoutput

```shell
factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
```
Add a Factoid output to a transaction in the wallet

##backupwallet

```shell
factom-cli backupwallet
```
Backup the running wallet

##balance

```shell
factom-cli balance [-r] ADDRESS
```
If this is an EC Address, returns number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

##buyec

```shell
factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
```
balance
Buy entry credits

##composechain

```shell
factom-cli composechain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
```
Create API calls to create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

##composeentry

```shell
factom-cli composeentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
```
Create API calls to create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

##composetx

```shell
factom-cli composetx TXNAME
```
Compose a wallet transaction into a json rpc object

##ecrate

```shell
factom-cli ecrate
```
It takes this many Factoids to buy an Entry Credit. Displays the larger between current and future rates. Also used to set Factoid fees.

##exportaddresses

```shell
factom-cli exportaddresses
```
List the private addresses stored in the wallet

##get

```shell
factom-cli get allentries|chainhead|dblock|eblock|entry|firstentry|head|heights
```
Get data about Factom Chains, Entries, and Blocks

##get allentries

```shell
factom-cli get allentries [-n NAME1 -N HEXNAME2 ...] CHAINID
```
Get all of the Entries in a Chain

##get chainhead

```shell
factom-cli get chainhead [-n NAME1 -N HEXNAME2 ...] CHAINID
```
Get ebhead by chainid

##get dblock

```shell
factom-cli get dblock KEYMR
```
Get dblock contents by merkle root

##get eblock

```shell
factom-cli get eblock KEYMR
```
Get eblock by merkle root

##get entry

```shell
factom-cli get entry HASH
```
Get entry by hash

##get firstentry

```shell
factom-cli get firstentry [-n NAME1 -N HEXNAME2 ...] CHAINID
```
Get the first entry from a chain

##get head

```shell
factom-cli get head
```
Get the latest completed directory block

##get heights

```shell
factom-cli get heights
```
Get the current heights of various blocks in factomd

##importaddress

```shell
factom-cli importaddress ADDRESS [ADDRESS...]
```
Import one or more secret keys into the wallet

##importwords

```shell
factom-cli importwords '12WORDS'
```
Import 12 words from Koinify sale into the Wallet

##listaddresses

```shell
factom-cli listaddresses
```
List the addresses stored in the wallet

##listtxs

```shell
factom-cli listtxs [tmp|all|address|id|range]
```
List transactions from the wallet or the Factoid Chain

##listtxs address

```shell
factom-cli listtxs address ECADDRESS|FCTADDRESS
```
List transaction from the Factoid Chain with a specific address

##listtxs [all]

```shell
factom-cli listtxs [all]
```
List all transactions from the Factoid Chain

##listtxs id 

```shell
factom-cli listtxs id TXID
```
List transaction from the Factoid Chain

##listtxs range

```shell
factom-cli listtxs range START END
```
List the transactions from the Factoid Chain within the specified range

##listtxs tmp

```shell
factom-cli listtxs tmp
```
List current working transactions in the wallet

##newecaddress

```shell
factom-cli newecaddress
```
Generate a new Entry Credit Address in the wallet

##newfctaddress

```shell
factom-cli newfctaddress
```
Generate a new Factoid Address in the wallet

##newtx

```shell
factom-cli newtx TXNAME
```
Create a new transaction in the wallet

##properties

```shell
factom-cli properties
```
Get version information about facotmd and the factom wallet

##receipt

```shell
factom-cli receipt ENTRYHASH
```
Returns a Receipt for a given Entry

##rmtx

```shell
factom-cli rmtx TXNAME
```
Remove a transaction in the wallet

##sendfct

```shell
factom-cli sendfct FROMADDRESS TOADDRESS AMOUNT
```
Send Factoids between 2 addresses

##sendtx

```shell
factom-cli sendtx TXNAME
```
Send a Transaction to Factom

##signtx

```shell
factom-cli signtx TXNAME
```
Sign a transaction in the wallet

##subtxfee

```shell
factom-cli subtxfee TXNAME ADDRESS
```
Subtract the transaction fee from an output of a transaction in the wallet
