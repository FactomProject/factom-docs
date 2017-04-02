# Debug API

These API calls were originally created for Factom internal use to help them develop better tools and quickly monitor processes, nodes and servers. These API calls are primarily for debugging information and purposes.

An example of a request and a response are given in the right panel for each of the RPC Methods.

## holding-queue

Show current holding messages in queue.

> Example Request

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

## network-info

Get information on the current network factomd is connected to (TEST, MAIN, etc).

> Example Request

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

## predictive-fer

Get the predicted future entry credit rate.

> Example Request

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

## audit-servers

Get a list of the current network audit servers along with their information.

> Example Request

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

## federated-servers

Get a list of the current network federated servers along with their information.

> Example Request

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

## configuration

Get the current configuration state from factomd.

> Example Request

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

## process-list

Get the process list known to the current factomd instance.

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "process-list"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```

## authorities

List of authority servers in the management chain.

> Example Request

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

## reload-configuration

Causes factomd to re-read the configuration from the config file.
Note:This may cause consensus problems and could be impractical even in testing.

> Example Request

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

## drop-rate

Get the current package drop rate for network testing.

> Example Request

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

## set-drop-rate

Change the network drop rate for testing.

> Example Request

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

## current-minute

Get the current minute number for the open entry block.

> Example Request

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

## delay

Get the current msg delay time for network testing.

> Example Request

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

## set-delay

> Example Request

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

Get the nodes summary string.

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "summary"}' \
-H 'content-type:text/plain;' http://localhost:8088/debug
```

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

## messages

Get a list of messages from the message journal (must run factomd with -journaling=true).

> Example Request

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
		{
		"Type":20,
		"Message":{
			"FullMsgHash":null,
			"Origin":0,
			"NetworkOrigin":"",
			"Peer2Peer":true,
			"LocalOnly":true,
			"NoResend":true,
			"ResendCnt":0,
			"LeaderChainID":null,
			"MsgHash":null,
			"VMIndex":0,
			"VMHash":null,
			"Minute":0,
			"Stalled":false,
			"MarkInvalid":false,
			"Sigvalid":false,
			"Timestamp":1490901994036,
			"DirectoryBlock":{
				"DBHash":"67064c4c80bbf8da3a9829a3bc6c5acd0b8f71f34d7a1d3d80d9e436507eb1fd",
				"KeyMR":"f6c823b784bb685419af9f71198ec6809f9d9a9db721c08a28b5d165f6449d92",
				"Header":{
					"Version":0,
					"NetworkID":4164959280,
					"BodyMR":"c61aafca406f0dfe5e9825bd54e48f04320d97024281fbd0d5077ff3bbf6ce6b",
					"PrevKeyMR":"0000000000000000000000000000000000000000000000000000000000000000",
					"PrevFullHash":"0000000000000000000000000000000000000000000000000000000000000000",
					"Timestamp":24018960,
					"DBHeight":0,
					"BlockCount":3,"ChainID":"000000000000000000000000000000000000000000000000000000000000000d"
				},
			"DBEntries"[
				{
				"ChainID":"000000000000000000000000000000000000000000000000000000000000000a",
				"KeyMR":"3a4014a3ea9ccbe3f64b6178972e4a8828317cc3ffb491accf1ee4f8fcce747f"
				},						
				{
				"ChainID":"000000000000000000000000000000000000000000000000000000000000000c",
				"KeyMR":"a566023a9d7b824e4a12121ee38bc4d3c4987988f04eb8cfecc63570936d7c56"
				},
				{
				"ChainID":"000000000000000000000000000000000000000000000000000000000000000f",
				"KeyMR":"0f426b2433103e606fb16b9340c14d88da8a02268af3c58b9a7896fa86e2904f"
				}
			]
		},
		"AdminBlock":{
			"Header":{
				"PrevBackRefHash":"0000000000000000000000000000000000000000000000000000000000000000",
				"DBHeight":0,
				"HeaderExpansionSize":0,
				"HeaderExpansionArea":"",
				"MessageCount":1,
				"BodySize":37,
				"AdminChainID":"000000000000000000000000000000000000000000000000000000000000000a",
				"ChainID":"000000000000000000000000000000000000000000000000000000000000000a"
			},
			"ABEntries":[
				{
				"IdentityChainID":"38bab1455b7bd7e5efd15c53c777c79d0c988e9210f1da49a99d95b3a6417be9",
				"DBHeight":1
				}
			],
			"BackReferenceHash":"61957dd1579df70286ebeb07862f23ea64a3657c9dce6e22833c45ea955212ed",
			"LookupHash":"3a4014a3ea9ccbe3f64b6178972e4a8828317cc3ffb491accf1ee4f8fcce747f"
		},
		"FactoidBlock":{
			"bodymr":"3f18eb3ef578f76c74da414fed348805d079dc2402bdf0a17c5967c552092c6c",
			"prevkeymr":"0000000000000000000000000000000000000000000000000000000000000000",
			"prevledgerkeymr":"0000000000000000000000000000000000000000000000000000000000000000",
			"exchrate":1000,
			"dbheight":0,
			"transactions":[
				{
				"millitimestamp":1441108800000,
				"inputs":[],
				"outputs":[
					{
					"amount":50000000253000,
					"address":"6c464662cb2b43ae2159e76afa733eb5c37be13f71141f3dc586191f57d2a548",
					"useraddress":""
					}
				],
				"outecs":[],
				"rcds":[],
				"sigblocks":[],
				"blockheight":0
				},
				{
				"millitimestamp":1441108800000,
				"inputs":[
					{
					"amount":50000000253000,
					"address":"6c464662cb2b43ae2159e76afa733eb5c37be13f71141f3dc586191f57d2a548",
					"useraddress":""
					}
				],
				"outputs":[
					{
					"amount":2000000000000,
					"address":"4311a01e2140f9c41afa18e1bf134333f5cf056f1afa78b717a540e030cbf0ef",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"211b255e3801cca0a7ea538c7ce36592275f424105f21411a6634d00c5a4caec",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"08115f96ebb5e35a9c806de9cffe4c99455a0c5a1c448a1d2eb6d46abb7ea8e6",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"0a5b5a404fc54a1b9eadb45dfa7dc9e65ee13196869c9d00689ae48ef97dd23f",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"b6738c6be1b76d94b1a7fee21f1d6efc35193d77c73d724417deb90e27ac85bf",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"36d3fc555c342169e3a6343b2b614493f3a26904c4e691842e9395205dad0f3d",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"46489723fe6d51019fdbd2539dd79b4a3e0fd6842f8e4c914327d426457df85c",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc428",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"be92612b43078eb5338118b701a043a8b74df2f9bbb1727bc4a2ac864b80a4d6",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"44f417858ea07b80a6c275d73a9eba8fc5c9231c3184c3b59f2fcd4c2eeafb85",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"c8f0cbe13111626c58797fb056c97b0117b3f1b12ab61069b6ba5ebcbc2aa81e",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"59eb0c63b4a8293de6bbd543cf3f83910a72922a84d80ee83666528c0f1b802f",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"11532bc06a9b51784e9e83209b51b7e3a8e715d9295a534660e3070961b3ae93",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"ce7b98bfdae90f942bc1fe88c3dd44d8f4c81f4eeb88a5602da05abc82ffdb53",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"872678c0ed7bbc55b7d3f378e049591b8e5771b7a4b509bedb76f24c8a58a5fc",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"e5df4353f66065227dd8721ff5d29f144cc6e8790843395cab5dd8df0a260dbb",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"17e5dc5999de0116483d64982e9a821e00b45f5f31e3f414e54547e78b1bde90",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"bb6d682adc8edab9a9cdc83b83723fa3fd279d2e4745ace86423abe400ea044e",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"27e0df223b9f6ff3fa1f0b1f095db920d22f61c8a6a94827dc88b92bb440ca8a",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"e44aae4ba2c54022f39606abfb6f5975e0769738b5cc35320e5ec1ca6ddc9b79",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"d929b10b488382de5cccaa2a47b2a77ac04fd78926c67eb264615fc388063ab9",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"e4571e13d3af400ad41a7e70134387d0f9b0bd5afc646213c0144043235bd361",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"a675d5ad742ccc4f33f5769724e1522be33cc8b09e57e0e73a25c2227847811b",
					"useraddress":""
					},
					{
					"amount":2000000000000,
					"address":"0b17cd56783c900c7618601fe3ac3f7986306e3d23fe494c22bfbf31b869ece8",
					"useraddress":""
					}
				],
				"outecs":[],
				"rcds":[
					"941d317e41d4fb6f2f464a842897fe3046d2b446d01787d8801dcdb856fecb27"
				],
				"sigblocks":[
					{
					"Signatures":[
						"ad344954a2fc39765bc235ceb5cc5fe89fe643d7125d0d93e00d18a848f4518e07c8ee89d814fe18eedbc78bf146de2a83729755536c32b9396ae062a395f001"
					]
					}
				],
				"blockheight":0
			}
			],
			"chainid":"000000000000000000000000000000000000000000000000000000000000000f",
			"keymr":"0f426b2433103e606fb16b9340c14d88da8a02268af3c58b9a7896fa86e2904f",
			"ledgerkeymr":"9264d9df82a1912d156669cd9d914d421fa14eb90136d8bcab98820592995535"
		},
		"EntryCreditBlock":{
			"Header":{
				"BodyHash":"e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
				"PrevHeaderHash":"0000000000000000000000000000000000000000000000000000000000000000",
				"PrevFullHash":"0000000000000000000000000000000000000000000000000000000000000000",
				"DBHeight":0,
				"HeaderExpansionArea":"",
				"ObjectCount":0,
				"BodySize":0,
				"ChainID":"000000000000000000000000000000000000000000000000000000000000000c",
				"ECChainID":"000000000000000000000000000000000000000000000000000000000000000c"
			},
			"Body":{
				"Entries":[]
			}
		},
		"EBlocks":null,
		"Entries":null,
		"SignatureList":{
			"Length":1,
			"List":[
				{
				"Pub":"cc1985cdfae4e32b5a454dfda8ce5e1361558482684f3367649c3ad852c8e31a",
				"Sig":"02511cf522d19cdd91b0d893bdd53ac89ea58154016f7f4d41c174eeb6522955683f46d52a685637f55e7c49ff92ff824fa10c18f846e4cd09e618dfbcf7ab09"
				}
			]
		},
		"Sent":null,
		"IsInDB":true
	}
},
........
```