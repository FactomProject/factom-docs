# factom-walletd API

API reference documentation for factom-walletd. factom-walletd serves the wallet api on port :8089.

All these APIs use JSON-RPC, which is a remote procedure call protocol encoded in JSON. It is a very simple protocol (and very similar to XML-RPC), defining only a handful of data types and commands.

They can be invoked as:

`curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "METHOD_NAME", "params":{"PARAM_1":"DATA_1"}}' -H 'content-type:text/plain;' http://localhost:8089/v2`

 The output will also be JSON.

 An example of a request and a response are given in the Right Panel for each of the RPC Methods.

## errors

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "bad"}'  \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "bad"
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "error": {
        "code": -32601,
        "message": "Method not found"
    }
}
```

Example of an invalid method

## address

> Example Request

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "address",
    "params": {
        "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"
    }
}
```

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
"address", "params":{"address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"}}' \ 
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "public": "FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
        "secret": "Fs3E9gV6DXsYzf7Fqx1fVBQPQXV695eP3k5XbmHEZVRLkMdD9qCK"
    }
}
```

Retrieve the public and private parts of a Factoid or Entry Credit address stored in the wallet.

## all-addresses

> Example Request

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "all-addresses"
}
```

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "all-addresses"}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "addresses": [
            {
                "public": "FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
                "secret": "Fs3E9gV6DXsYzf7Fqx1fVBQPQXV695eP3k5XbmHEZVRLkMdD9qCK"
            },
            {
                "public": "EC3MAHiZyfuEb5fZP2fSp2gXMv8WemhQEUFXyQ2f2HjSkYx7xY1S",
                "secret": "Es3ETdf64QnorrJzosZuCbcdSVPTu1NZVezUXTjjTTSzNb12JtES"
            }
        ]
    }
}
```

Retrieve all of the Factoid and Entry Credit addresses stored in the wallet.

## generate-ec-address

> Example Request

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "generate-ec-address"
}

```

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "generate-ec-address"}' \ 
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "public": "EC2LV5w7pMD9fwtoAnv2wiCSGm2WzYpxjCMz84reWmBsxLuCPoBp",
        "secret": "Es3tXbGBVKZDhUWzDKzQtg4rcpmmHPXAY9vxSM2JddwJSD5td3f8"
    }
}
```

Create a new Entry Credit Address and store it in the wallet.

## generate-factoid-address

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "generate-ec-address"}' \ 
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "generate-factoid-address"
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "public": "FA2uGBEmmW5VUy3obcT12DWkW91cVVRV9yppifhkGANBQCzd3pNi",
        "secret": "Fs2G4Hs9YxqBZ8TkfyWwNKmJbwet3Zg1JNXt8MrQReCEph6rGt9v"
    }
}
```

Create a new Entry Credit Address and store it in the wallet.

## get-height

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "get-height"}' \ 
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "get-height"
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "height": 1030
    }
}
```

Get the current hight of blocks that have been cached by the wallet while syncing.

## import-addresses

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "import-addresses", "params":{"addresses":[{"secret":"Fs2G4Hs9YxqBZ8TkfyWwNKmJbwet3Zg1JNXt8MrQReCEph6rGt9v"},{"secret":"Es3tXbGBVKZDhUWzDKzQtg4rcpmmHPXAY9vxSM2JddwJSD5td3f8"}]}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "import-addresses",
    "params": {
        "addresses": [
            {
                "secret": "Fs2G4Hs9YxqBZ8TkfyWwNKmJbwet3Zg1JNXt8MrQReCEph6rGt9v"
            },
            {
                "secret": "Es3tXbGBVKZDhUWzDKzQtg4rcpmmHPXAY9vxSM2JddwJSD5td3f8"
            }
        ]
    }
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "addresses": [
            {
                "public": "FA2uGBEmmW5VUy3obcT12DWkW91cVVRV9yppifhkGANBQCzd3pNi",
                "secret": "Fs2G4Hs9YxqBZ8TkfyWwNKmJbwet3Zg1JNXt8MrQReCEph6rGt9v"
            },
            {
                "public": "EC2LV5w7pMD9fwtoAnv2wiCSGm2WzYpxjCMz84reWmBsxLuCPoBp",
                "secret": "Es3tXbGBVKZDhUWzDKzQtg4rcpmmHPXAY9vxSM2JddwJSD5td3f8"
            }
        ]
    }
}
```

Import Factoid and/or Entry Credit address secret keys into the wallet.

## import-koinify

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "import-koinify", "params":
{"words":"yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "import-koinify",
    "params": {
        "words": "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"
    }
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "public": "FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1",
        "secret": "Fs1Nifx4n5BCsS277ozuWpHqX4vRo54eYNvT3cv3wLdFbfSMMjyx"
    }
}
```

Import a Koinify crowd sale address into the wallet. In our examples we used the word "yellow" twelve times, note that in your case the master passphrase will be different.


## wallet-backup

> Example Request

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "wallet-backup"
}
```

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "wallet-backup"}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "wallet-seed": "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow",
        "addresses": [
            {
                "public": "FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
                "secret": "Fs3E9gV6DXsYzf7Fqx1fVBQPQXV695eP3k5XbmHEZVRLkMdD9qCK"
            },
            {
                "public": "FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1",
                "secret": "Fs1Nifx4n5BCsS277ozuWpHqX4vRo54eYNvT3cv3wLdFbfSMMjyx"
            },
            {
                "public": "EC1r4PvxinJgUVXA1j5RhvHZSWuCHtxtH3KsA5jqKAVsxY53F3tU",
                "secret": "Es3XpT2AZaG6vWGWYEjru17mS5rP4rzKUmLfwjEiez9R3fSuy5pB"
            },
            {
                "public": "EC2LV5w7pMD9fwtoAnv2wiCSGm2WzYpxjCMz84reWmBsxLuCPoBp",
                "secret": "Es3tXbGBVKZDhUWzDKzQtg4rcpmmHPXAY9vxSM2JddwJSD5td3f8"
            },
        ]
    }
}
```

Return the wallet seed and all addresses in the wallet for backup and offline storage.

## transactions (Retrieving)

There are a few ways to search for a transaction

### Using a Range

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"transactions",
   "params":{  
      "range":{  
         "start":1,
         "end":2
      }
   }
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method"
:"transactions", "params":{"range":{"start":1,"end":2}}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Reponse 

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "transactions":[  
         {  
            "blockheight":2,
            "feespaid":7999200,
            "signed":true,
            "timestamp":1441138236,
            "totalecoutputs":100000000,
            "totalinputs":107999200,
            "totaloutputs":0,
            "inputs":[  
               {  
                  "address":"FA21zXEUHMPiRtzBgiMY15cGrSpgXCsZqrDPxPv4oUZsR5f2AcjP",
                  "amount":107999200
               }
            ],
            "outputs":null,
            "ecoutputs":[  
               {  
                  "address":"EC2LQ673tP3bRPgzuY6iyNVNvzHxVtzAcG5yw6KyBJpftGWsdS2t",
                  "amount":100000000
               }
            ],
            "txid":"82bd7f0461cfc915b539075faac07488e911ea6dcf1512ca913a876e020ff251"
         },
         {  
            "blockheight":1,
            "feespaid":7999200,
            "signed":true,
            "timestamp":1441138021,
            "totalecoutputs":200000000,
            "totalinputs":207999200,
            "totaloutputs":0,
            "inputs":[  
               {  
                  "address":"FA2vGRwutdPdTHQa7kkpX3LkSgqKQ1MS2nur4UqbxqP5MGHcziWa",
                  "amount":207999200
               }
            ],
            "outputs":null,
            "ecoutputs":[  
               {  
                  "address":"EC1whAxbYYsfQoAFLuzHCsz4Qz29WePBcrrGj5MqMQ1PR43wjiBH",
                  "amount":200000000
               }
            ],
            "txid":"f1d9919829fa71ce18caf1bd8659cce8a06c0026d3f3fffc61054ebb25ebeaa0"
         }
      ]
   }
}
```

This will retrieve all transactions within a given block height range.

### By TxID

> Example Request

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"transactions",
   "params":{  
      "txid":"f1d9919829fa71ce18caf1bd8659cce8a06c0026d3f3fffc61054ebb25ebeaa0"
   }
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
"transactions", "params":{"txid":
"f1d9919829fa71ce18caf1bd8659cce8a06c0026d3f3fffc61054ebb25ebeaa0"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Reponse

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "transactions":[  
         {  
            "feespaid":7999200,
            "signed":true,
            "timestamp":8,
            "totalecoutputs":200000000,
            "totalinputs":207999200,
            "totaloutputs":0,
            "inputs":[  
               {  
                  "address":"FA2vGRwutdPdTHQa7kkpX3LkSgqKQ1MS2nur4UqbxqP5MGHcziWa",
                  "amount":207999200
               }
            ],
            "outputs":null,
            "ecoutputs":[  
               {  
                  "address":"EC1whAxbYYsfQoAFLuzHCsz4Qz29WePBcrrGj5MqMQ1PR43wjiBH",
                  "amount":200000000
               }
            ],
            "txid":"f1d9919829fa71ce18caf1bd8659cce8a06c0026d3f3fffc61054ebb25ebeaa0"
         }
      ]
   }
}
```

This will retrieve a transaction by the given TxID. This call is the fastest way to retrieve a transaction, but it will not display the height of the transaction. If a height is in the response, it will be 0. To retrieve the height of a transaction, use the 'By Address' method

This call in the backend really pushes the request to factomd. For a more informative reponse, it is advised to use the <a href="#transaction">factomd transaction method</a>

### By Address

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0,
"method":"transactions", "params":
{"address":"FA2vGRwutdPdTHQa7kkpX3LkSgqKQ1MS2nur4UqbxqP5MGHcziWa"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"transactions",
   "params":{  
      "address":"FA2vGRwutdPdTHQa7kkpX3LkSgqKQ1MS2nur4UqbxqP5MGHcziWa"
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "transactions":[  
         {  
            "blockheight":1,
            "feespaid":7999200,
            "signed":true,
            "timestamp":1441138021,
            "totalecoutputs":200000000,
            "totalinputs":207999200,
            "totaloutputs":0,
            "inputs":[  
               {  
                  "address":"FA2vGRwutdPdTHQa7kkpX3LkSgqKQ1MS2nur4UqbxqP5MGHcziWa",
                  "amount":207999200
               }
            ],
            "outputs":null,
            "ecoutputs":[  
               {  
                  "address":"EC1whAxbYYsfQoAFLuzHCsz4Qz29WePBcrrGj5MqMQ1PR43wjiBH",
                  "amount":200000000
               }
            ],
            "txid":"f1d9919829fa71ce18caf1bd8659cce8a06c0026d3f3fffc61054ebb25ebeaa0"
         },
         {  
            "feespaid":1673832600,
            "signed":true,
            "timestamp":1441137600,
            "totalecoutputs":0,
            "totalinputs":178826890364500,
            "totaloutputs":178825216531900,
            "inputs":[  
               {  
                  "address":"FA2L6Vng4jBMbbDZtYLsxKQbAAin4Rxg2CgvnyzXrwENSK1t2QUx",
                  "amount":178826890364500
               }
            ],
            "outputs":[  
               {  
                  "address":"FA2vGRwutdPdTHQa7kkpX3LkSgqKQ1MS2nur4UqbxqP5MGHcziWa",
                  "amount":224108800
               }
            ],
            "ecoutputs":null,
            "txid":"18b13f36b22d6cc23cab2a42fc277ecb0033a0281e646f14e0339e1fbc2ee464"
         }
      ]
   }
}
```

Retrieves all transactions that an address is apart of.

### All Transactions

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, 
"method":"transactions"}' -H 'content-type:text/plain;' \
http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"transactions"
}
```

`The developers were so preoccupied with whether or not they could, they didn’t stop to think if they should.`

The amount of data returned by this is so large, I couldn't get you a sample output as it froze my terminal window. It is strongly reccomended to use other techniques to retrieve transactions, it is rarely the case to require EVERY transaction in the blockchain. If you are still determined to retrieve EVERY transaction in the blockchain, use other techniques such as using the 'range' method and specifically requesting for transactions between blocks X and Y, then incrementing your X's and Y's until you reach the latest block. This is much more manageable.

## tmp-transactions

> Example Request

```shell
curl  -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, 
"method":"tmp-transactions"}' -H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method":"tmp-transactions"
}
```

> Example Response

```json-doc
{
    "jsonrpc":"2.0",
    "id":0,
    "result":{
        "transactions":[
            {
                "tx-name":"TX_NAME",
                "txid":"e387d89510f16e69ca979bde111caf97d2fc1cf273fe82bf41e241980df76dba",
                "totalinputs":0,
                "totaloutputs":0,
                "totalecoutputs":0
            }
        ]
    }
}
```

Lists all the current working transactions in the wallet. These are transactions that are not yet sent.

## delete-transaction

> Example Request

```json
{
    "jsonrpc":"2.0",
    "id":0,"method":"delete-transaction",
    "params":{
        "tx-name":"a"
    }
}
```

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, 
"method":"delete-transaction", "params":{"tx-name":"TX_NAME"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "signed":false,
      "name":"TX_NAME",
      "timestamp":-62135596800,
      "totalecoutputs":0,
      "totalinputs":0,
      "totaloutputs":0,
      "inputs":null,
      "outputs":null,
      "ecoutputs":null
   }
}

```

Deletes a working transaction in the wallet. The full transaction will be returned, and then deleted.

## new-transaction

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method":"new-transaction", 
"params":{"tx-name":"TX_NAME"}}' -H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc":"2.0",
    "id":0,"method":"new-transaction",
    "params":{
        "tx-name":"TX_NAME"
    }
}
```

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feesrequired":1000,
      "signed":false,
      "name":"TX_NAME",
      "timestamp":1484933437,
      "totalecoutputs":0,
      "totalinputs":0,
      "totaloutputs":0,
      "inputs":null,
      "outputs":null,
      "ecoutputs":null,
      "txid":"4ab170433f9384f3e77a25a5d21a58f794bef19b9a363bcd88048203d73cf3ba"
   }
}
```

This will create a new transaction. The txid is in flux until the final transaction is signed. Until then, it should not be used or recorded.

When dealing with transactions all factoids are represented in factoshis. 1 factoid is 1e8 factoshis, meanining you can never send anything less than 0 to a transaction (0.5).

## add-input

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-input","params":
{"tx-name":"TX_NAME","address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q","amount":2000000000}}' \
 -H 'content-type:text/plain;' http://localhost:8089/v2 
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"add-input",
   "params":{  
      "tx-name":"TX_NAME",
      "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
      "amount":2000000000
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feespaid":2000000000,
      "feesrequired":2000,
      "signed":false,
      "name":"TX_NAME",
      "timestamp":1484934602,
      "totalecoutputs":0,
      "totalinputs":2000000000,
      "totaloutputs":0,
      "inputs":[  
         {  
            "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
            "amount":2000000000
         }
      ],
      "outputs":null,
      "ecoutputs":null,
      "txid":"e713c13c4b3868cc884d1baa68f77cacbe74a2a248f38d4ac5883550fce0c961"
   }
}
```

Adds an input to the transaction from the given address. The public address is given, and the wallet must have the private key associated with the address in order to succusfully sign the transaction.

The input is measured in factoshis, so to send 10 factoids, you must input 1,000,000,000 factoshis (without commas in json)

## add-output

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-output",
"params":{"tx-name":"TX_NAME","address":
"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P","amount":1000000000}}'  \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"add-output",
   "params":{  
      "tx-name":"TX_NAME",
      "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P",
      "amount":1000000000
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feespaid":1000000000,
      "feesrequired":12000,
      "signed":false,
      "name":"TX_NAME",
      "timestamp":1484934602,
      "totalecoutputs":0,
      "totalinputs":2000000000,
      "totaloutputs":1000000000,
      "inputs":[  
         {  
            "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
            "amount":2000000000
         }
      ],
      "outputs":[  
         {  
            "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P",
            "amount":1000000000
         }
      ],
      "ecoutputs":null,
      "txid":"e713d93303077cb87634489c9fd335b394925bf3ae167e5f226b523fa882dd71"
   }
}
```

Adds a factoid address output to the transaction. Keep in mind the output is done in factoshis. 1 factoid is 1,000,000,000 factoshis.

So to send 10 factoids, you must send 1,000,000,000 factoshis (no commas in json)

## add-ec-output

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-ec-output"
,"params":{"tx-name":"TX_NAME","address":
"EC22MrL8CT4iTfRhxPvAStm9v4XEn5cJPvUpY39GLgU9GPnKMffn","amount":10000}}' \
 -H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"add-ec-output",
   "params":{  
      "tx-name":"TX_NAME",
      "address":"EC22MrL8CT4iTfRhxPvAStm9v4XEn5cJPvUpY39GLgU9GPnKMffn",
      "amount":10000
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feesrequired":22000,
      "signed":false,
      "name":"TX_NAME",
      "timestamp":1484934602,
      "totalecoutputs":10,
      "totalinputs":2000000000,
      "totaloutputs":1000000000,
      "inputs":[  
         {  
            "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
            "amount":2000000000
         }
      ],
      "outputs":[  
         {  
            "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P",
            "amount":1000000000
         }
      ],
      "ecoutputs":[  
         {  
            "address":"EC22MrL8CT4iTfRhxPvAStm9v4XEn5cJPvUpY39GLgU9GPnKMffn",
            "amount":10000
         }
      ],
      "txid":"65ec0f3990c49bd18ec4e9c10c6f1d0fa91572dd7cdbf61e5b47b67ab0f011f6"
   }
}
```

When adding entry credit outputs, the amount given is in factoshis, not entry credtis. This means math is required to determine the correct amount of factoshis to pay to get X EC.

`(ECRate * ECTotalOutput)`

In our case the rate is 1000, meaning 1000 entry credits per factoid. We added 10 entry credits, so we need 1,000 * 10 = 10,000 factoshis

To get the ECRate search in the search bar above for "entry-credit-rate"


## add-fee

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-fee","params":
{"tx-name":"TX_NAME","address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"add-fee",
   "params":{  
      "tx-name":"TX_NAME",
      "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feespaid":22000,
      "feesrequired":22000,
      "signed":false,
      "name":"TX_NAME",
      "timestamp":1484934602,
      "totalecoutputs":10000,
      "totalinputs":1000032000,
      "totaloutputs":1000000000,
      "inputs":[  
         {  
            "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
            "amount":1000032000
         }
      ],
      "outputs":[  
         {  
            "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P",
            "amount":1000000000
         }
      ],
      "ecoutputs":[  
         {  
            "address":"EC22MrL8CT4iTfRhxPvAStm9v4XEn5cJPvUpY39GLgU9GPnKMffn",
            "amount":10000
         }
      ],
      "txid":"0afa940a04f2423135fef1c62c6785dc105850079583c2b1881b6b23017266b3"
   }
}
```

Addfee is a shortcut and safeguard for adding the required additonal factoshis to covert the fee. The fee is displayed in the returned transaction after each step, but this be used instead of manually adding the additional input. It is a safeguard as it prevents overpaying.

Addfee will complain if your inputs and outputs do not match up. For example, in the steps above we added the inputs first, this was intentional to show a case of overpaying. Obviously no one wants to overpay for a transaction, so addfee has returned an error and this message: 'Inputs and outputs don't add up' . This is because we have 2,000,000,000 factoshis as input and only 1,000,000,000 + 10,000 as output. Lets correct the input by doing 'add-input', and putting 1000010000 as the amount for the address. It will overwrite the previous input.

Curl to do that:

`curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-input","params":
{"tx-name":"TX_NAME","address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q","amount":1000010000}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2 `

Run the addfee again and the feepaid and feerequired will match up

## sub-fee

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"sub-fee","params":{"tx-name":"TX_NAME","address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P"}}' -H 'content-type:text/plain;' http://localhost:8089/v2
```

```json

```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feespaid":22000,
      "feesrequired":22000,
      "signed":false,
      "name":"TX_NAME",
      "timestamp":1484934602,
      "totalecoutputs":10000,
      "totalinputs":1000010000,
      "totaloutputs":999978000,
      "inputs":[  
         {  
            "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
            "amount":1000010000
         }
      ],
      "outputs":[  
         {  
            "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P",
            "amount":999978000
         }
      ],
      "ecoutputs":[  
         {  
            "address":"EC22MrL8CT4iTfRhxPvAStm9v4XEn5cJPvUpY39GLgU9GPnKMffn",
            "amount":10000
         }
      ],
      "txid":"32fbdc624fb31927f60a1cd52a836b1c65cc49ddc98b41d4d7adb50780ebf305"
   }
}
```

When paying from a transaction, you can also make the recieving transaction pay for it. Using sub fee, you can use the recieiving address in the parameters, and the fee will be deducted from their output amount.

This allows a wallet to send all it's factoids, by making the input and output the remaining balance, then using sub fee on the output address.

## sign-transaction

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"sign-transaction","params":{"tx-name":"TX_NAME"}}' \
 -H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"sign-transaction",
   "params":{  
      "tx-name":"TX_NAME"
   }
}
```

> Example Reponse

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "feespaid":22000,
      "feesrequired":22000,
      "signed":true,
      "name":"TX_NAME",
      "timestamp":1484934602,
      "totalecoutputs":10000,
      "totalinputs":1000010000,
      "totaloutputs":999978000,
      "inputs":[  
         {  
            "address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q",
            "amount":1000010000
         }
      ],
      "outputs":[  
         {  
            "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P",
            "amount":999978000
         }
      ],
      "ecoutputs":[  
         {  
            "address":"EC22MrL8CT4iTfRhxPvAStm9v4XEn5cJPvUpY39GLgU9GPnKMffn",
            "amount":10000
         }
      ],
      "txid":"32fbdc624fb31927f60a1cd52a836b1c65cc49ddc98b41d4d7adb50780ebf305"
   }
}
```

Signs the transaction. It is now ready to be signed

## compose-transaction

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"compose-transaction",
"params":{"tx-name":"TX_NAME"}}' -H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"compose-transaction",
   "params":{  
      "tx-name":"TX_NAME"
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "jsonrpc":"2.0",
      "id":3,
      "params":{  
         "transaction":"020159bcffde4d01010183dcebe210646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc42883dce9e81028f458993c24c1cee28b34f77fc633c92603f36e1c1cd1f21350753f00eccdefce1022883c5223b3344e0a0e0a9a5a23856890507d4451a5ee2de0ca6c6d699d4cdf01718b5edd2914acc2e4677f336c1a32736e5e9bde13663e6413894f57ec272e28a30347ad7a0b4d449a0e644e5b4bd53eda240677a450b6f19482b63558031c027ae7ca84d713a4eac48a3e9f57603fe270318fc8144eb107fa10c6cf349c9006"
      },
      "method":"factoid-submit"
   }
}
```

Compose transaction marshals the transaction into a hex encoded string. The string can be inputted into the factomd API 'factoid-submit' to be sent to the network.

## properties

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "properties"}'  \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "properties"
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "walletversion": "0.2.0.0",
        "walletapiversion": "2.0"
    }
}
```

Retrieve current properties of factom-walletd, including the wallet and wallet API versions.
