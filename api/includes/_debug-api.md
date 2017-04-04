# Debug API

These API calls were originally created for Factom internal use to help them develop better tools and quickly monitor processes, nodes and servers. These API calls are primarily for debugging information and purposes.

An example of a request and a response are given in the right panel for each of the RPC Methods.

## holding-queue

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"holding-queue"
}
```

```shell
 curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "holding-queue"}' \
 -H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"Messages":null
	}
}
```

Show current holding messages in queue.

## network-info

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"network-info"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "network-info"}' \ 
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"NetworkNumber":1,
	"NetworkName":"MAIN",
	"NetworkID":4203931043
	}
}
```

Get information on the current network factomd is connected to (TEST, MAIN, etc).

## predictive-fer

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"predictive-fer"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "predictive-fer"}' \ 
-H 'content-type:text/plain;' http://localhost:8088/debug
```

> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"PredictiveFER":666600
	}
}
```

Get the predicted future entry credit rate.

## audit-servers

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"audit-servers"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "audit-servers"}' \ 
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"AuditServers":[]
	}
}
```

Get a list of the current network audit servers along with their information.

## federated-servers

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"federated-servers"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "federated-servers"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"FederatedServers":[
		{
		"ChainID":"0000000000000000000000000000000000000000000000000000000000000000",
		"Name":"",
		"Online":true,
		"Replace":null
		}
	]
	}
}
```

Get a list of the current network federated servers along with their information.

## configuration

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"configuration"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "configuration"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":
	{
	"App":
		{
		"PortNumber":8088,
		"HomeDir":"/home/.factom/m2/",
		"ControlPanelPort":8090,
		"ControlPanelFilesPath":"/home/.factom/m2/",
		"ControlPanelSetting":"readonly",
		"DBType":"LDB",
		"LdbPath":"/home/.factom/m2/test-database/ldb",
		"BoltDBPath":"/home/.factom/m2/test-database/bolt",
		"DataStorePath":"/home/.factom/m2/test-data/export",
		"DirectoryBlockInSeconds":6,
		"ExportData":false,
		"ExportDataSubpath":"/home/.factom/m2/test-database/export/",
		"NodeMode":"FULL","IdentityChainID":"",
		"LocalServerPrivKey":"4c38c72fc5cdad68f13b74674d3ffb1f3d63a112710868c9b08946553448d26d",
		"LocalServerPublicKey":"cc1985cdfae4e32b5a454dfda8ce5e1361558482684f3367649c3ad852c8e31a",
		"ExchangeRate":0,
		"ExchangeRateChainId":"111111118d918a8be684e0dac725493a75862ef96d2d3f43f84b26969329bf03",
		"ExchangeRateAuthorityPublicKey":"daf5815c2de603dbfa3e1e64f88a5cf06083307cf40da4a9b539c41832135b4a",
		"ExchangeRateAuthorityPublicKeyMainNet":"daf5815c2de603dbfa3e1e64f88a5cf06083307cf40da4a9b539c41832135b4a",
		"ExchangeRateAuthorityPublicKeyTestNet":"1d75de249c2fc0384fb6701b30dc86b39dc72e5a47ba4f79ef250d39e21e7a4f",
		"ExchangeRateAuthorityPublicKeyLocalNet":"3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29",
		"Network":"MAIN",
		"MainNetworkPort":"8108",
		"PeersFile":"/home/.factom/m2/test-peers.json",
		"MainSeedURL":"https://raw.githubusercontent.com/FactomProject/factomproject.github.io/master/seed/mainseed.txt",
		"MainSpecialPeers":"",
		"TestNetworkPort":"8109",
		"TestSeedURL":"https://raw.githubusercontent.com/FactomProject/factomproject.github.io/master/seed/testseed.txt",
		"TestSpecialPeers":"",
		"LocalNetworkPort":"8110",
		"LocalSeedURL":"https://raw.githubusercontent.com/FactomProject/factomproject.github.io/master/seed/localseed.txt",
		"LocalSpecialPeers":"",
		"CustomBootstrapIdentity":"38bab1455b7bd7e5efd15c53c777c79d0c988e9210f1da49a99d95b3a6417be9",
		"CustomBootstrapKey":"cc1985cdfae4e32b5a454dfda8ce5e1361558482684f3367649c3ad852c8e31a",
		"FactomdTlsEnabled":false,
		"FactomdTlsPrivateKey":"/full/path/to/factomdAPIpriv.key",
		"FactomdTlsPublicCert":"/full/path/to/factomdAPIpub.cert",
		"FactomdRpcUser":"",
		"FactomdRpcPass":"",
		"ChangeAcksHeight":0
		},
	"Peer":
		{
		"AddPeers":null,
		"ConnectPeers":null,
		"Listeners":null,
		"MaxPeers":0,
		"BanDuration":0,
		"TestNet":false,
		"SimNet":false
		},
	"Log":
		{
		"LogPath":"/home/mjb/.factom/m2/test-database/Log",
		"LogLevel":"error",
		"ConsoleLogLevel":"standard"
		},
	"Wallet":
		{
		"Address":"",
		"Port":0,
		"DataFile":"",
		"RefreshInSeconds":"",
		"BoltDBPath":"",
		"FactomdAddress":"",
		"FactomdPort":0
		},
	"Walletd":
		{
		"WalletRpcUser":"",
		"WalletRpcPass":"",
		"WalletTlsEnabled":false,
		"WalletTlsPrivateKey":"/full/path/to/walletAPIpriv.key",
		"WalletTlsPublicCert":"/full/path/to/walletAPIpub.cert",
		"FactomdLocation":"localhost:8088",
		"WalletdLocation":"localhost:8089"
		}
	}
}
```

Get the current configuration state from factomd.

## process-list

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"process-list"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "process-list"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```

## authorities

List of authority servers in the management chain.

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"authorities"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "authorities"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":
	{
	"Authorities"[
		{
		"AuthorityChainID":"0000000000000000000000000000000000000000000000000000000000000000",
		"ManagementChainID":"0000000000000000000000000000000000000000000000000000000000000000",
		"MatryoshkaHash":"0000000000000000000000000000000000000000000000000000000000000000",
		"SigningKey":"49b6edd274e7d07c94d4831eca2f073c207248bde1bf989d2183a8cebca227b7",
		"Status":1,
		"AnchorKeys":null,
		"KeyHistory":null
		}
	]
	}
}
```


Get the process list known to the current factomd instance.

## reload-configuration

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"reload-configuration"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "reload-configuration"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"App":{
		"PortNumber":8088,
		"HomeDir":"/home/.factom/m2/",
		"ControlPanelPort":8090,
		"ControlPanelFilesPath":"/home/.factom/m2/",
		"ControlPanelSetting":"readonly",
		"DBType":"LDB","LdbPath":"/home/.factom/m2/test-database/ldb",
		"BoltDBPath":"/home/.factom/m2/test-database/bolt",
		"DataStorePath":"/home/.factom/m2/test-data/export",
		"DirectoryBlockInSeconds":6,"ExportData":false,
		"ExportDataSubpath":"/home/.factom/m2/test-database/export/",
		"NodeMode":"FULL",
		"IdentityChainID":"",
		"LocalServerPrivKey":"4c38c72fc5cdad68f13b74674d3ffb1f3d63a112710868c9b08946553448d26d",
		"LocalServerPublicKey":"cc1985cdfae4e32b5a454dfda8ce5e1361558482684f3367649c3ad852c8e31a",
		"ExchangeRate":0,
		"ExchangeRateChainId":"111111118d918a8be684e0dac725493a75862ef96d2d3f43f84b26969329bf03",
		"ExchangeRateAuthorityPublicKey":"daf5815c2de603dbfa3e1e64f88a5cf06083307cf40da4a9b539c41832135b4a",
		"ExchangeRateAuthorityPublicKeyMainNet":"daf5815c2de603dbfa3e1e64f88a5cf06083307cf40da4a9b539c41832135b4a",
		"ExchangeRateAuthorityPublicKeyTestNet":"1d75de249c2fc0384fb6701b30dc86b39dc72e5a47ba4f79ef250d39e21e7a4f",
		"ExchangeRateAuthorityPublicKeyLocalNet":"3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29",
		"Network":"MAIN",
		"MainNetworkPort":"8108","PeersFile":"/home/.factom/m2/test-peers.json",
		"MainSeedURL":"https://raw.githubusercontent.com/FactomProject/factomproject.github.io/master/seed/mainseed.txt",
		"MainSpecialPeers":"",
		"TestNetworkPort":"8109",
		"TestSeedURL":"https://raw.githubusercontent.com/FactomProject/factomproject.github.io/master/seed/testseed.txt",
		"TestSpecialPeers":"",
		"LocalNetworkPort":"8110",
		"LocalSeedURL":"https://raw.githubusercontent.com/FactomProject/factomproject.github.io/master/seed/localseed.txt",
		"LocalSpecialPeers":"",
		"CustomBootstrapIdentity":"38bab1455b7bd7e5efd15c53c777c79d0c988e9210f1da49a99d95b3a6417be9",
		"CustomBootstrapKey":"cc1985cdfae4e32b5a454dfda8ce5e1361558482684f3367649c3ad852c8e31a",
		"FactomdTlsEnabled":false,
		"FactomdTlsPrivateKey":"/full/path/to/factomdAPIpriv.key",
		"FactomdTlsPublicCert":"/full/path/to/factomdAPIpub.cert",
		"FactomdRpcUser":"",
		"FactomdRpcPass":"",
		"ChangeAcksHeight":0
	},
	"Peer":{
		"AddPeers":null,
		"ConnectPeers":null,
		"Listeners":null,
		"MaxPeers":0,
		"BanDuration":0,
		"TestNet":false,
		"SimNet":false
	},
	"Log":{
		"LogPath":"/home/.factom/m2/test-database/Log",
		"LogLevel":"error",
		"ConsoleLogLevel":"standard"
	},
	"Wallet":{
		"Address":"",
		"Port":0,
		"DataFile":"",
		"RefreshInSeconds":"",
		"BoltDBPath":"",
		"FactomdAddress":"",
		"FactomdPort":0
	},
	"Walletd":{
		"WalletRpcUser":"",
		"WalletRpcPass":"",
		"WalletTlsEnabled":false,
		"WalletTlsPrivateKey":"/full/path/to/walletAPIpriv.key",
		"WalletTlsPublicCert":"/full/path/to/walletAPIpub.cert",
		"FactomdLocation":"localhost:8088",
		"WalletdLocation":"localhost:8089"
	}
}
}
```

Causes factomd to re-read the configuration from the config file.
Note:This may cause consensus problems and could be impractical even in testing.

## drop-rate

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"drop-rate"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "drop-rate"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
	"jsonrpc":"2.0",
	"id":0,
	"result":{
		"DropRate":0
	}
}
```

Get the current package drop rate for network testing.

## set-drop-rate

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"set-drop-rate",
   "params":{  
      "DropRate":10
   }
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "set-drop-rate", "params":{"DropRate":10}}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
	"jsonrpc":"2.0",
	"id":0,
	"result":{
		"DropRate":10
	}
}
```

Change the network drop rate for testing.

## current-minute

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"current-minute"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "current-minute"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
	"jsonrpc":"2.0",
	"id":0,
	"result":{
		"Minute":0
	}
}
```


Get the current minute number for the open entry block.

## delay

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"delay"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "delay"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
	"jsonrpc":"2.0",
	"id":0,"result":{
		"Delay":0
	}
}
```

Get the current msg delay time for network testing.

## set-delay

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"set-delay",
   "params":{  
      "Delay":10
   }
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "set-delay", "params":{"Delay":10}}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
	"jsonrpc":"2.0",
	"id":0,
	"result":{
		"Delay":10
	}
}
```

## summary

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"summary"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "summary"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```

> Example Response

```json-doc
{
	"jsonrpc":"2.0",
	"id":0,
	"result":{
		"Summary":"    FNode0[b1455b]
		L___vm00  0/ 0  0.0%  0.000  2832[1aac21] 2830/2833/2834   1/ 1        
		0/0/0/0                    0/0/0/0      0     0        0/0/0          
		0/0/0   0.00/0.00 0/0 -"
	}
}
```

Get the nodes summary string.

## messages

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"messages"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "messages"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```
> Example Response

```json-doc
{
"jsonrpc":"2.0",
"id":0,
"result":{
	"Messages":[
		"... Messages ..."
	]}
}
```

Get a list of messages from the message journal (must run factomd with -journaling=true).
