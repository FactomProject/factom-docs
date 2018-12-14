# Factom CLI Commands

```shell
factom-cli [OPTIONS] SUBCOMMAND [OPTIONS]
```
<i>factom-cli</i> is a command line interface program for interacting with <i>factomd</i>  and <i>factom-walletd</i>.

## Flags

### -f

```shell
$ echo hello | factom-cli addchain -f -n moe -n larry \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The f flag, used with the `addchain`, `addentry`, `buyec`, `composechain`, `composeentry`, `sendfct`, `sendtx`, and `signtx` subcommands, tells factom-cli to continue on with processing without waiting for acknowledgment of the success of the subcommand to be generated. This can be useful for scripts where you can execute a long string of subcommands in a fraction of the time it would take if you had to wait for an acknowledgment of each command individually.

### -q

```shell
$ echo goodbye | factom-cli addentry -q -n moe -n larry -e curly \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The q flag specifies "quiet" execution of the `addchain`, `addentry`, `addtxecoutput`, `addtxfee`,
`addtxinput`, `addtxoutput`, `buyec`, `newtx`, `sendfct`, `sendtx`, `signtx`, and `subtxfee` subcommands. This means that no output will be returned back to the user. This again can be useful for scripts where there is no need for feedback from factom-cli.

### -e -x

```shell
$ factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] \
[-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>
```

The `addentry` subcommands support the `-e` and `-x` flags for adding external ids to the Entries they create. Multiple `-e` and `-x` flags may be used, and -e and -x may be used in combination. `-e` string will encode the string as binary and set it as the next external id. `-x` hexstring will decode the hexstring into binary and set it as the next external id.

### -n -h

```shell
$ factom-cli get chainhead -n test -h 3031
```

The `get firstentry`, `get chainhead`, and `get allentries` subcommands support the `-n` and `-h` flags for using Chain Names as an alternative for providing a ChainID. The Chain Name is the combination of External IDs on the first Entry in the Chain.

### -r

```shell
$ factom-cli sendfct -r $my_factoid_address factom.michaeljbeam.me
```

The r flag tells factom-cli to try and resolve a public Factoid or Entry Credit Address from a DNS name registered through Netki.

### -C

```shell
$ echo hello | factom-cli addchain -n moe -n larry -C \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The C flag, used with the `addchain` subcommand, limits the subcommand output to a single field, the ChainID with no headers. This means that a variable can be assigned to the value of the executed command directly.

### -E

```shell
$ echo goodbye | factom-cli addentry -n moe -n larry -e curly -E \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The E flag, used with the `addchain` and `addentry` subcommands, limits the subcommand output to a single field, the Entry Hash with no headers. This means that a variable can be assigned to the value of the executed command directly.

### -T

```shell
$ factom-cli get pendingtransactions -T
```

The T flag, used with the `addchain`, `addentry`, `buyec`, `get pendingtransactions`, `listtxs address`, `listtxs` subcommands, limits the subcommand output to a single field, the Entry Hash with no headers. This means that a variable can be assigned to the value of the executed command directly.

## Commands

### status

```shell
factom-cli status TxID|FullTx
```
Returns information about a factoid transaction, or an entry / entry credit transaction

### addchain

```shell
factom-cli addchain [-fq] [-n NAME1 -n NAME2 -h HEXNAME3 ] [-CET] \
ECADDRESS <STDIN>
```

Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

### addentry

```shell
factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] \
 [-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>
```
Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

### addtxecoutput

```shell
factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
```
Add an Entry Credit output to a transaction in the wallet

### addtxfee

```shell
factom-cli addtxfee TXNAME ADDRESS
```
Add the transaction fee to an input of a transaction in the wallet

### addtxinput

```shell
factom-cli addtxinput TXNAME ADDRESS AMOUNT
```
Add a Factoid input to a transaction in the wallet

### addtxoutput

```shell
factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
```
Add a Factoid output to a transaction in the wallet

### backupwallet

```shell
factom-cli backupwallet
```
Backup the running wallet

### balance

```shell
factom-cli balance [-r] ADDRESS
```
If this is an EC Address, returns the number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

### buyec

```shell
factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
```
balance
Buy entry credits

### composechain

```shell
$ factom-cli composechain [-f] [-n NAME1 -n NAME2 -h HEXNAME3 ] \
ECADDRESS <STDIN>
```
Create API calls to create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

### composeentry

```shell
$ factom-cli composeentry [-f] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] \
[-e EXTID1 -e EXTID2 -x HEXEXTID ...] ECADDRESS <STDIN>
```
Create API calls to create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

### composetx

```shell
$ factom-cli composetx TXNAME
```
Compose a wallet transaction into a JSON RPC object

### ecrate

```shell
factom-cli ecrate
```
It takes this many Factoids to buy an Entry Credit. Displays the larger between current and future rates. Also used to set Factoid fees.

### exportaddresses

```shell
factom-cli exportaddresses
```
List the private addresses stored in the wallet

### exportidentitykeys

```shell
factom-cli exportidentitykeys
```
List the identity key pairs (public and private) stored in the wallet

### get

```shell
factom-cli get allentries|chainhead|dblock|eblock|entry|firstentry| \
head|heights
```
Get data about Factom Chains, Entries, and Blocks

### get allentries

```shell
factom-cli get allentries [-n NAME1 -N HEXNAME2 ...] CHAINID
```
Get all of the Entries in a Chain

### get chainhead

```shell
factom-cli get chainhead [-n NAME1 -N HEXNAME2 ...] CHAINID
```
Get ebhead by chainid

### get dblock

```shell
factom-cli get dblock KEYMR
```
Get dblock contents by Merkle root

### get eblock

```shell
factom-cli get eblock KEYMR
```
Get eblock by Merkle root

### get entry

```shell
factom-cli get entry HASH
```
Get entry by hash

### get firstentry

```shell
factom-cli get firstentry [-n NAME1 -N HEXNAME2 ...] CHAINID
```
Get the first entry from a chain

### get head

```shell
factom-cli get head
```
Get the latest completed directory block

### get heights

```shell
$ factom-cli get heights [-DLBE]
DirectoryBlockHeight: 10000
LeaderHeight: 10001
EntryBlockHeight: 10000
EntryHeight: 10000

$ factom-cli get heights -D
10000

```
Get the current heights of various blocks in factomd

Optional output flags will display only specific information used for scripting
**-D** display only the DirectoryBlock height

**-L** display only the Leader height

**-B** display only the EntryBlock height

**-E** display only the Entry height

### identity

```shell
factom-cli identity addchain|addkeyreplacement|addattribute| \
addattributeendorsement|composechain|composekeyreplacement| \
composeattribute|composeattributeendorsement|getactivekeys|getactivekeysatheight
```
Used with subcommands to create/manage Factom Identity Chains, their currently valid keys, attributes, and attribute endorsements

### identity addchain
```shell
factom-cli identity addchain [-fq] [-n NAME1 -n NAME2] \
[-k PUBKEY1 -k PUBKEY2] [-CET] ECADDRESS
```

Create a new Identity Chain. Use the Entry Credits from the specified address.

Using the optional output flags allows you to get back information about the newly created chain and the transaction that created it. Those flags are: `-C` ChainID. `-E` EntryHash. `-T` TxID.

### identity addkeyreplacement
```shell
factom-cli identity addkeyreplacement [-fq] \
 [-c CHAINID | -n NAME1 -n NAME2 ... -n NAMEN] \
 --oldkey PUBKEY --newkey PUBKEY --signerkey PUBKEY ECADDRESS [-CET]
```

Create a new Identity Key Replacement Entry using the Entry Credits from the specified address. The oldkey is replaced by the newkey, and signerkey (same or higher priority as oldkey) authorizes the replacement.

Using the optional output flags allows you to get back information about the newly created entry and the transaction that created it. Those flags are: `-C` ChainID. `-E` EntryHash. `-T` TxID.

### identity addattribute
```shell
factom-cli identity addattribute [-fq] -c CHAINID \
-creceiver CHAINID -csigner CHAINID -signerkey PUBKEY \
-attribute ATTRIBUTE_JSON_ARRAY ECADDRESS [-CET]
```

Create a new Identity Attribute Entry using the Entry Credits from the specified address.

Using the optional output flags allows you to get back information about the newly created entry and the transaction that created it. Those flags are: `-C` ChainID. `-E` EntryHash. `-T` TxID.

The `-attribute` flag must be followed by a JSON array of sub-attributes (key:value mappings) surrounded by backticks like so:

```-attribute `[{"key":KEY1,"value":VALUE1},{"key":KEY2,"value":VALUE2},{"key":KEYN,"value":VALUEN}]` ```

### identity addattributeendorsement
```shell
factom-cli identity addattributeendorsement [-fq] -c CHAINID \
-csigner CHAINID -signerkey PUBKEY -entryhash ENTRYHASH ECADDRESS [-CET]
```

Create a new Endorsement Entry for the Identity Attribute at the given entry hash. Uses the Entry Credits from the specified address.

Using the optional output flags allows you to get back information about the newly created entry and the transaction that created it. Those flags are: `-C` ChainID. `-E` EntryHash. `-T` TxID.

### identity composechain
```shell
factom-cli identity composechain [-f] [-n NAME1 -n NAME2] \
[-k PUBKEY1 -k PUBKEY2] ECADDRESS
```

Create API calls to create a new Factom Identity Chain. Use the Entry Credits from the specified address.

### identity composekeyreplacement
```shell
factom-cli identity composekeyreplacement [-f] \
[-c CHAINID | -n NAME1 -n NAME2 ... -n NAMEN] \
--oldkey PUBKEY --newkey PUBKEY --signerkey PUBKEY ECADDRESS
```

Create API calls to create a new Identity key replacement entry using the Entry Credits from the specified address. The oldkey is replaced by the newkey, and signerkey (same or higher priority as oldkey) authorizes the replacement.

### identity composeattribute
```shell
factom-cli identity composeattribute [-f] -c CHAINID \
-creceiver CHAINID -csigner CHAINID -signerkey PUBKEY \
-attribute ATTRIBUTE_JSON_ARRAY ECADDRESS
```

Create API calls to create a new Identity Attribute Entry using the Entry Credits from the specified address.

The `-attribute` flag must be followed by a JSON array of sub-attributes (key:value mappings) surrounded by backticks like so:

```-attribute `[{"key":KEY1,"value":VALUE1},{"key":KEY2,"value":VALUE2},{"key":KEYN,"value":VALUEN}]` ```

### identity composeattributeendorsement
```shell
factom-cli identity composeattributeendorsement [-f] \
-c CHAINID -csigner CHAINID -signerkey PUBKEY -entryhash ENTRYHASH ECADDRESS
```

Compose API calls to create a new Endorsement Entry for the Identity Attribute at the given entry hash. Uses the Entry Credits from the specified address.

### identity getactivekeys
```shell
factom-cli identity getactivekeys [-c CHAINID | -n NAME1 -n NAME2 ... -n NAMEN]
```

Gets the set of identity public keys that are active for the given identity chain at the highest known block height.

### identity getactivekeysatheight
```shell
factom-cli identity getactivekeysatheight [-c CHAINID | -n NAME1 -n NAME2 ... -n NAMEN] HEIGHT
```

Gets the set of identity public keys that were active for the given identity chain at the specified block height.

### importaddress

```shell
factom-cli importaddress ADDRESS [ADDRESS...]
```
Import one or more secret keys into the wallet

### importidentitykeys

```shell
factom-cli importidentitykeys SECKEY [SECKEY...]
```
Import one or more identity keys into the wallet from the specified idsec keys

### importwords

```shell
factom-cli importwords '12WORDS'
```
Import 12 words from Koinify sale into the Wallet

### listaddresses

```shell
factom-cli listaddresses
```
List the addresses stored in the wallet

### listidentitykeys

```shell
factom-cli listidentitykeys
```
List the public identity keys stored in the wallet

### listtxs

```shell
factom-cli listtxs [tmp|all|address|id|range]
```
List transactions from the wallet or the Factoid Chain

### listtxs address

```shell
factom-cli listtxs address ECADDRESS|FCTADDRESS
```
List the transaction from the Factoid Chain with a specific address. This command will only list confirmed transactions.

### listtxs [all]

```shell
factom-cli listtxs [all]
```
List all transactions from the Factoid Chain. This command will only list confirmed transactions.

### listtxs id

```shell
factom-cli listtxs id TXID
```
List transaction from the Factoid Chain. This command will only list confirmed transactions.

### listtxs range

```shell
factom-cli listtxs range START END
```
List the transactions from the Factoid Chain within the specified range. This command will only list confirmed transactions.

### listtxs tmp

```shell
factom-cli listtxs tmp
```
List current working transactions in the wallet

### newecaddress

```shell
factom-cli newecaddress
```
Generate a new Entry Credit Address in the wallet

### newfctaddress

```shell
factom-cli newfctaddress
```
Generate a new Factoid Address in the wallet

### newidentitykey

```shell
factom-cli newidentitykey
```
Generates a new identity key in the wallet

### newtx

```shell
factom-cli newtx TXNAME
```
Create a new transaction in the wallet

### properties

```shell
factom-cli properties
```
Get version information about facotmd and the factom wallet

### receipt

```shell
factom-cli receipt ENTRYHASH
```
Returns a Receipt for a given Entry

### rmaddress

```shell
factom-cli rmaddress ADDRESS
```
Removes the public and private key from the wallet for the address specified.

### rmidentitykey

```shell
factom-cli rmidentitykey PUBKEY
```
Removes the identity key pair from the wallet for the specified idpub key.

### rmtx

```shell
factom-cli rmtx TXNAME
```
Remove a transaction in the wallet

### sendfct

```shell
factom-cli sendfct FROMADDRESS TOADDRESS AMOUNT
```
Send Factoids between 2 addresses

### sendtx

```shell
factom-cli sendtx TXNAME
```
Send a Transaction to Factom

### signtx

```shell
factom-cli signtx TXNAME
```
Sign a transaction in the wallet

### subtxfee

```shell
factom-cli subtxfee TXNAME ADDRESS
```
Subtract the transaction fee from an output of a transaction in the wallet

### unlockwallet

```shell
 factom-cli unlockwallet [-v] "passphrase" <seconds-to-unlock>
```
Unlock the wallet for some number of seconds; must be an encrypted wallet. -v verbose. (Note: it is recommended that you run the command with a leading space to prevent writing the password to the command line history.)
