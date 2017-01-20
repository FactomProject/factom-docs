# factomd API

This is the API reference for the factomd process. The API is designed for outside application to process transactions and interact with the Factom federated servers. It’s listening port can be configured and runs on 8088 by default.

All these APIs use JSON-RPC, which is a remote procedure call protocol encoded in JSON. It is a very simple protocol (and very similar to XML-RPC), defining only a handful of data types and commands.

They can be invoked in your terminal as

`curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "METHOD_HERE", "params": {"PARAM_1":"PARAM_DATA_1"}}' -H 'content-type:text/plain;' http://localhost:8088/v2`

 The output will also be JSON.

 The right panel will contain the curl commands to be run in your terminal, as well as the json structures of the request and reponse. The json structs detail the required parameters for each call.


## directory-block

> Example Request

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "directory-block",
  "params": {
    "keymr": "36c360817761e0d92af464f7c2e94a7495104d6b0a6051218cc53e52d3d519b6"
  }
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": 
"directory-block", "params": {"KeyMR":"7ed5d5b240973676c4a8a71c08c0cedb9e0ea335eaef22995911bcdc0fe9b26b"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "header":{  
         "prevblockkeymr":"7d15d82e70201e960655ce3e7cf475c9da593dfb82c6dca6377349bd148bf001",
         "sequencenumber":72497,
         "timestamp":1484858820
      },
      "entryblocklist":[  
         {  
            "chainid":"000000000000000000000000000000000000000000000000000000000000000a",
            "keymr":"3faa880a97ef6ce1feca643cffa015dd6be6a597b3f9260e408c5ac9351d1f8d"
         },
         {  
            "chainid":"000000000000000000000000000000000000000000000000000000000000000c",
            "keymr":"5f8c98930a1874a46b47b65b9376a02fbff65b760f6866519799d69e2bc019ee"
         },
         {  
            "chainid":"000000000000000000000000000000000000000000000000000000000000000f",
            "keymr":"8c6fed0f41317cc45201b5b170a9ac5bc045029e39a90b6061211be2c0678718"
         }
      ]
   }
}
```

Every directory block has a KeyMR (Key Merkle Root), which can be used to retrieve it. The reponse will contain information that can be used to naviagate through all transactions (entry and factoid) within that block. The header of the directory block will contain information regarding the previous directory block's keyMR, directory block height, and the timestamp. 

## directory-block-head
> Example Request

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "directory-block-head"
}
```

```shell
curl -X POST --data-binary \
'{"jsonrpc": "2.0", "id": 0, "method": "directory-block-head"}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "keymr":"7ed5d5b240973676c4a8a71c08c0cedb9e0ea335eaef22995911bcdc0fe9b26b"
   }
}
```
The directory block head is the last known directory block by factom, or in other words, the most recently recorded block. This can be used to grab the latest block and the information required to traverse the entire blockchain. 

## heights

> Example Request

```shell
curl -X POST --data-binary \
'{"jsonrpc": "2.0", "id": 0, "method": "heights"}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "heights"
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "directoryblockheight":72498,
      "leaderheight":72498,
      "entryblockheight":72498,
      "entryheight":72498,
      "missingentrycount":0,
      "entryblockdbheightprocessing":72498,
      "entryblockdbheightcomplete":72498
   }
}
```

Returns various heights that allows you to view the state of the blockchain. The heights returned provide a lot of information regarding the state of factomd, but not all are neede by most applications. The heights also indicate the most recent block, which could not be complete, and still being built. The heights mean as follows:

* directoryblockheight : The current directory block height of the local factomd node.
* leaderheight : The current block being worked on by the leaders in the network. This block is not yet complete, but all transactions submitted will go into this block (depending on network conditions, the transaction may be delayed into the next block)
* entryblockheight : The height at which the factomd node has all the entry blocks. Directory blocks are obtained first, entry blocks could be lagging behind the directory block when sycning.
* entryheight : The height at which the local factomd node has all the entries. If you added entries at a block height above this, they will be not be able to be retrieved by the local factomd until it syncs further.
* missingentrycount : More insight to the system, this should mostly be ignored
* entryblockdbheightprocessing : More insight to the system, this should mostly be ignored
* entryblockdbheightcomplete : More insight to the system, this should mostly be ignored

A fully synced node should show the same number for all but 'missingentrycount'

## raw-data

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": 
"raw-data", "params":{"hash":"0ae2ab2cf543eed52a13a5a405bded712444cc8f8b6724a00602e1c8550a4ec2"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "raw-data",
  "params": {
    "hash": "1f2931558c0ef6ef9d40450fa3a49dc3a29d18c30ced91c791bbe6060d405e39"
  }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "data":"00f9164cd66af9d5773b4523a510b5eefb9a5e626480feeb6671ef2d17510ca30000900040e5a5fa49cf19015475fb1b5c8e4269b4586f04ec98e0bb60dd32c214e201c9cf97febe09afca45549db35a9f61ca930855ce6d753853fb270490bcafb65e43020015466163746f6d20496e63204261736520436861696e0014466163746f6d697a652045766572797468696e67000c42656c6c2041766572616765001142656c6c204176657261676520446174617b22736f75726365223a227777772e62656c6c617665726167652e636f6d222c2271756f74655f64617465223a22323031372d30312d31392031373a33333a3031222c2264617461223a5b7b22474f4c44223a22313231332e3134227d2c7b2253494c564552223a2231372e3139227d5d7d"
   }
}
```

Retrieve an entry or transaction in raw format, the data is a hex encoded string. 

## dblock-by-height

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": 
"dblock-by-height", "params":{"height":14460}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "dblock-by-height",
  "params": {
    "height": 1
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "dblock": {
      "header": {
        "version": 0,
        "networkid": 4203931043,
        "bodymr": "7716df6083612597d4ef18a8076c40676cd8e0df8110825c07942ca5d30073b4",
        "prevkeymr": "fa7e6e2d37b012d71111bc4e649f1cb9d6f0321964717d35636e4637699d8da2",
        "prevfullhash": "469c7fdce467d222363d55ac234901d8acc61fd4045ae26dd54dac17c556ef86",
        "timestamp": 24671414,
        "dbheight": 14460,
        "blockcount": 3,
        "chainid": "000000000000000000000000000000000000000000000000000000000000000d"
      },
      "dbentries": [
        {
          "chainid": "000000000000000000000000000000000000000000000000000000000000000a",
          "keymr": "574e7d6178e04c92879601f0cb84a619f984eb2617ff9e76ee830a9f614cc9a0"
        },
        {
          "chainid": "000000000000000000000000000000000000000000000000000000000000000c",
          "keymr": "2a10f1678b9736f213ef3ac76e4f8aa910e5fed66733aa30dafdc91245157b3b"
        },
        {
          "chainid": "000000000000000000000000000000000000000000000000000000000000000f",
          "keymr": "cbadd7e280377ad8360a4b309df9d14f56552582c05100145ca3367e50adc497"
        }
      ],
      "dbhash": "aa7d881d23aad83425c3f10996999d31c76b51b14946f7aca204c150e81bc6d6",
      "keymr": "18509c431ee852edbe1029d676217a0d9cb4fcc11ef8e9aef27fd6075167120c"
    },
    "rawdata": "00fa92e5a37716df6083612597d4ef18a8076c40676cd8e0df8110825c07942ca5d30073b4fa7e6e2d37b012d71111bc4e649f1cb9d6f0321964717d35636e4637699d8da2469c7fdce467d222363d55ac234901d8acc61fd4045ae26dd54dac17c556ef86017874b60000387c00000003000000000000000000000000000000000000000000000000000000000000000a574e7d6178e04c92879601f0cb84a619f984eb2617ff9e76ee830a9f614cc9a0000000000000000000000000000000000000000000000000000000000000000c2a10f1678b9736f213ef3ac76e4f8aa910e5fed66733aa30dafdc91245157b3b000000000000000000000000000000000000000000000000000000000000000fcbadd7e280377ad8360a4b309df9d14f56552582c05100145ca3367e50adc497"
  }
}
```

Retrieve a directory block given only its height.

## ablock-by-height

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
"ablock-by-height", "params": {"height":1}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "ablock-by-height",
  "params": {
    "height": 14460
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "ablock": {
      "header": {
        "prevbackrefhash": "77e4fb398e228ec9710c20988647a01e2259a40ab77e27c005baf7f2deae3415",
        "dbheight": 14460,
        "headerexpansionsize": 0,
        "headerexpansionarea": "",
        "messagecount": 4,
        "bodysize": 516,
        "adminchainid": "000000000000000000000000000000000000000000000000000000000000000a",
        "chainid": "000000000000000000000000000000000000000000000000000000000000000a"
      },
      "abentries": [
        {
          "identityadminchainid": "888888e238492b2d723d81f7122d4304e5405b18bd9c7cb22ca6bcbc1aab8493",
          "prevdbsig": {
            "pub": "0186ad82617edf3565d944aa104590eb6adb338e92ee6fcd750c2ab2b2707e25",
            "sig": "5796cd49835088ea0d6b8e4a75611ebc674fb791d6e9ebc7f6e5bb1a5e86fc25a8a7742e8f60870e2cb8523fd122ef54bb95ac94b3676b81e07c921ed2196508"
          }
        },
        {
          "identityadminchainid": "888888fc37fa418395eeccb95ab0a4c64d528b2aeefa0d1632c8a116a0e4f5b1",
          "prevdbsig": {
            "pub": "c845f47df202a649e2262d3da0e35556aab62e361425ad7d2e7813a215c8f277",
            "sig": "a5c976c4d18814916fc893f7b4dee78120d20e0deab2b04df2e3b67c2ea1123224db28559ca6d022822388a5ce41128bf5a09ccbbd02b1c5b17a4152183a3d06"
          }
        },
        {
          "identityadminchainid": "88888815ac8a1ab6b8f57cee67ba15aad23ab7d8e70ffdca064200738c201f74",
          "prevdbsig": {
            "pub": "f18512813300d8c1d11e78216d0640ddcc35156a20b53d5ced351a7d5ad90010",
            "sig": "1051c165d7ad33e1f764bb96e5e661053da381ebd708c8ac137da2a1b6847eac07e83472d4fa6096768c7904760c821e45b5ebe23a691cc5bad1b61937f9e303"
          }
        },
        {
          "identityadminchainid": "888888271203752870ae5e6fa0cf96f93cf14bd052455ad476ab26de1ad2c077",
          "prevdbsig": {
            "pub": "4f2d34f0417297e2e985e0cc6e4cf3d0814416d09f37af7375517ea236786ed3",
            "sig": "01206ff2963af7df29bb6749a4c29bc1eb65a48bd7b3ec6590c723e11c3a3c5342e72f9b079a58d77a2562c25289d799fadfc5205f1e99c4f1d5c3ce85432906"
          }
        }
      ],
      "backreferencehash": "1786de6a72311dd4b60c6608d60c2b9367642fb1ee6b867b2c9f4c57c87b8cba",
      "lookuphash": "574e7d6178e04c92879601f0cb84a619f984eb2617ff9e76ee830a9f614cc9a0"
    },
    "rawdata": "000000000000000000000000000000000000000000000000000000000000000a77e4fb398e228ec9710c20988647a01e2259a40ab77e27c005baf7f2deae34150000387c00000000040000020401888888e238492b2d723d81f7122d4304e5405b18bd9c7cb22ca6bcbc1aab84930186ad82617edf3565d944aa104590eb6adb338e92ee6fcd750c2ab2b2707e255796cd49835088ea0d6b8e4a75611ebc674fb791d6e9ebc7f6e5bb1a5e86fc25a8a7742e8f60870e2cb8523fd122ef54bb95ac94b3676b81e07c921ed219650801888888fc37fa418395eeccb95ab0a4c64d528b2aeefa0d1632c8a116a0e4f5b1c845f47df202a649e2262d3da0e35556aab62e361425ad7d2e7813a215c8f277a5c976c4d18814916fc893f7b4dee78120d20e0deab2b04df2e3b67c2ea1123224db28559ca6d022822388a5ce41128bf5a09ccbbd02b1c5b17a4152183a3d060188888815ac8a1ab6b8f57cee67ba15aad23ab7d8e70ffdca064200738c201f74f18512813300d8c1d11e78216d0640ddcc35156a20b53d5ced351a7d5ad900101051c165d7ad33e1f764bb96e5e661053da381ebd708c8ac137da2a1b6847eac07e83472d4fa6096768c7904760c821e45b5ebe23a691cc5bad1b61937f9e30301888888271203752870ae5e6fa0cf96f93cf14bd052455ad476ab26de1ad2c0774f2d34f0417297e2e985e0cc6e4cf3d0814416d09f37af7375517ea236786ed301206ff2963af7df29bb6749a4c29bc1eb65a48bd7b3ec6590c723e11c3a3c5342e72f9b079a58d77a2562c25289d799fadfc5205f1e99c4f1d5c3ce85432906"
  }
}
```

Retrieve administrative blocks for any given height.

The admin block contains data related to the identities within the factom system and the decisions the system makes as it builds the block chain. The 'abentries' (admin block entries) in the json response can be of various types, the most common is a directory block signature (DBSig). A majority of the federated servers sign every directory block, meaning every block after m5 will contain 5 DBSigs in each admin block. 

The ABEntries are detailed here: [Github Link](https://github.com/FactomProject/FactomDocs/blob/master/factomDataStructureDetails.md#adminid-bytes)

## ecblock-by-height

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
"ecblock-by-height", "params": {"height":1}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "ecblock-by-height",
  "params": {
    "height": 14460
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "ecblock": {
      "header": {
        "bodyhash": "ef7a85d4bf868e34aff4edce479f6ee412161e1faa3596a112cd5ef75e96f59c",
        "prevheaderhash": "add44ed20133c7b8c9500ab5819d3aee665fffcce7acb6baa098fa8210b43a8b",
        "prevfullhash": "2f1dd9e5f1ab34102f65dea55c1598e2344568d68c0511640b7f436295615746",
        "dbheight": 14460,
        "headerexpansionarea": "",
        "objectcount": 10,
        "bodysize": 20,
        "chainid": "000000000000000000000000000000000000000000000000000000000000000c",
        "ecchainid": "000000000000000000000000000000000000000000000000000000000000000c"
      },
      "body": {
        "entries": [
          {
            "number": 1
          },
          {
            "number": 2
          },
          {
            "number": 3
          },
          {
            "number": 4
          },
          {
            "number": 5
          },
          {
            "number": 6
          },
          {
            "number": 7
          },
          {
            "number": 8
          },
          {
            "number": 9
          },
          {
            "number": 10
          }
        ]
      }
    },
    "rawdata": "000000000000000000000000000000000000000000000000000000000000000cef7a85d4bf868e34aff4edce479f6ee412161e1faa3596a112cd5ef75e96f59cadd44ed20133c7b8c9500ab5819d3aee665fffcce7acb6baa098fa8210b43a8b2f1dd9e5f1ab34102f65dea55c1598e2344568d68c0511640b7f4362956157460000387c00000000000000000a0000000000000014010101020103010401050106010701080109010a"
  }
}
```

Retrieve the entry credit block for any given height. These blocks contain entry credit transaction information.

## fblock-by-height

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
 "fblock-by-height", "params": {"height":1}}' \
 -H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "fblock-by-height",
  "params": {
    "height": 14460
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "fblock": {
      "bodymr": "e12db6a1945d513f066cab66c94dc5cca1b8f90997b95a47b46e70b1656f764a",
      "prevkeymr": "98f3a6bcd978080fb612359f131fdb73c6119dea1f45c977a3fa30dfd507ebf5",
      "prevledgerkeymr": "fe7734478375e16f92f9e5513dbc3f2e830dd2bb263801ba816129242ce83cfe",
      "exchrate": 95369,
      "dbheight": 14460,
      "transactions": [
        {
          "millitimestamp": 1480284840637,
          "inputs": [],
          "outputs": [],
          "outecs": [],
          "rcds": [],
          "sigblocks": [],
          "blockheight": 0
        },
        {
          "millitimestamp": 1480284848556,
          "inputs": [
            {
              "amount": 201144428,
              "address": "dfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f",
              "useraddress": ""
            }
          ],
          "outputs": [
            {
              "amount": 200000000,
              "address": "031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f",
              "useraddress": ""
            }
          ],
          "outecs": [],
          "rcds": [
            "3f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac"
          ],
          "sigblocks": [
            {
              "signatures": [
                "68fd6905eeb276739b2541398db3b1b06d73f99a50803bac83eafabc24be656e26278af6fe8070c85e861e21c39a56a5a422dd2d58dd65a7eeff849f6d02de04"
              ]
            }
          ],
          "blockheight": 0
        },
        {
          "millitimestamp": 1480284956754,
          "inputs": [
            {
              "amount": 401144428,
              "address": "dfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f",
              "useraddress": ""
            }
          ],
          "outputs": [
            {
              "amount": 400000000,
              "address": "031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f",
              "useraddress": ""
            }
          ],
          "outecs": [],
          "rcds": [
            "3f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac"
          ],
          "sigblocks": [
            {
              "signatures": [
                "363c20508bddf5a9d4762e2496a861a1f03ec0dc50389b836dec898a3b37c33a6f831edf057f48a961b2d336231a78137e7402a0ca3a1d5c186ce2bb79e44907"
              ]
            }
          ],
          "blockheight": 0
        }
      ],
      "chainid": "000000000000000000000000000000000000000000000000000000000000000f",
      "keymr": "cbadd7e280377ad8360a4b309df9d14f56552582c05100145ca3367e50adc497",
      "ledgerkeymr": "886747480a30f833a27a819fe4b92fbd617cda028329fd2e4b87c7721ff65dea"
    },
    "rawdata": "000000000000000000000000000000000000000000000000000000000000000fe12db6a1945d513f066cab66c94dc5cca1b8f90997b95a47b46e70b1656f764a98f3a6bcd978080fb612359f131fdb73c6119dea1f45c977a3fa30dfd507ebf5fe7734478375e16f92f9e5513dbc3f2e830dd2bb263801ba816129242ce83cfe00000000000174890000387c000000000b0000071c020158a7da22bd000000020158a7da41ac010100dff4f06cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fdfaf8400031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac68fd6905eeb276739b2541398db3b1b06d73f99a50803bac83eafabc24be656e26278af6fe8070c85e861e21c39a56a5a422dd2d58dd65a7eeff849f6d02de04020158a7da70a5010100b09dae6cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fafd7c200031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac7e503a078b7f5bac25333c54a724530b97d25b8c2a83f82fdde249987b8bf4a4ba3da41643b7723102c3506bae86f6347ae94b72e8ca4c14617d8d3ca57df70500020158a7da9f9f010100818fccb26cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f818f86c600031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971aced5c095795dc3a2fdcf7689718d10f32be9c656049f169900eac51a34b3f1cb2a0d35ba0a9440892219be15927a4702f062e29ac35238ece375bda4dea9a2a0500020158a7dace9101010083ddb1806c031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f83dceb9400dfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f013b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29fdb846a8f9abcb8a1eda9556a8d5f8ef959d1649fddb5ba1ccd3a66b6bc919d8ed225b1273e671685812725a10a7bbac95f0ed9f128bcb3547b068fe3137e50500020158a7dafd8201010081bfa3f46cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f81bede8800031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac66080fa6968bd4b104f1f7a2b5f5bd30b05b066bca956ef28ae94a17f1e18fd102de60f7612811707fda09df69802f5fe4438c1b7b750b57fcc4684c9235520100020158a7db2c7b010100dff4f06cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fdfaf8400031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac40316508538da5dda6d029e6d8b7eca7b9a5074def82a1d78a0f04ac82fe1efbe14f01b01a6778d648ee47c3acf6f9ab2c9f044087703d55f9901403b991780500020158a7db5b75010100dff4f06cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fdfaf8400031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac4f050366992fe0a8fb8939825e1286f096f8f1e3528d23e737a499ba73ac1c041501c77f8baf780b3cb915f630a07ac2c0cb312bfb8c89b27ab550fef070a30500020158a7db8a6e010100b09dae6cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fafd7c200031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971aca6d367d754fd45454c04fd090a68ba4b02ad0316362a7fcd16f164f56d335e8ebd83a3f6e9f5dc1cae9a3ad4eb48a675b8c8b984a1989d359f2bcad368c9c60900020158a7dbb96001010083ddb1806c031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f83dceb9400dfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f013b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29c59178bafe8aca410070ba26fd2d4eb607360f52a1b74b60f55a66a3c65bfc5c9ce9b03f6dd4880246723d8542c93fc935f988bc77cc3b9f3d616b414005730300020158a7dbe85201010081bfa3f46cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f81bede8800031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac363c20508bddf5a9d4762e2496a861a1f03ec0dc50389b836dec898a3b37c33a6f831edf057f48a961b2d336231a78137e7402a0ca3a1d5c186ce2bb79e449070000"
  }
}
```

Retrieve the factoid block for any given height. These blocks contain factoid transaction information.

## receipt

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": 
"receipt", "params":{"hash":"0561491594de81214ebd918f29d1f9f59266ea63ec76341162dc4a252a0225b9"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "receipt",
  "params": {
    "Hash": "0561491594de81214ebd918f29d1f9f59266ea63ec76341162dc4a252a0225b9"
  }
}
```

> Example Response

```
//issue TODO
{
  "jsonrpc":"2.0",
  "id":0,
  "result":{
    "Receipt":{
        "Entry":////TODO
        "MerkleBranch":////TODO
        "EntryBlockKeyMR":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "DirectoryBlockKeyMR":"bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb",
        "BitcoinTransactionHash":"cccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccc",
        "BitcoinBlockHash":"dddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddd"
    }
  }
}
```

Retrieve a reciept providing cryptographially verfiable proof that information was recorded in the factom blockchain and that this was subsequently anchored in the bitcoin blockchain.

## entry-block

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":"entry-block", 
"params":{"KeyMR":"041c3fed14469a3d0f1a022e3d5321583065e691edb9223605c86766ff881883"}}'\
 -H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "entry-block",
  "params": {
    "KeyMR": "f65f67774139fa78344dcdd302631a0d646db0c2be4d58e3e48b2a188c1b856c"
  }
}
```

> Example Response

```json-doc
{  
 "jsonrpc":"2.0",
 "id":0,
 "result":{  
  "header":{  
   "blocksequencenumber":4211,
   "chainid":"0caff62ea5b5aa015c706add7b2463a5be07e1f0537617f553558090f23c7f56",
   "prevkeymr":"f7588bc41f03220a5ba4128432dc58b2027c05f432c91d79e6213ecdd5c923b3",
   "timestamp":1450147800,
   "dbheight":15000
  },
  "entrylist":[  
   {  
    "entryhash":"0ae2ab2cf543eed52a13a5a405bded712444cc8f8b6724a00602e1c8550a4ec2",
    "timestamp":1450147980
   }
  ]
 }
}
```

Retrieve a specified entry block given its merkle root key. The entry block contains 0 to many entries

## entry

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":"entry","params":
{"Hash":"24674e6bc3094eb773297de955ee095a05830e431da13a37382dcdc89d73c7d7"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "entry",
  "params": {
    "hash": "be5216cc7a5a3ad44b49245aec298f47cbdfca9862dee13b0093e5880012b771"
  }
}
```

> Example Response

```json-doc
{  
 "jsonrpc":"2.0",
 "id":0,
 "result":{  
  "chainid":"df3ade9eec4b08d5379cc64270c30ea7315d8a8a1a69efe2b98a60ecdd69e604",
  "content":"...",
  "extids":[  
     "466163746f6d416e63686f72436861696e"
  ]
 }
}
```

Get an Entry from factomd specified by the Entry Hash.

## pending-entries

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
"pending-entries", "params": {}}' -H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"pending-entries",
   "params":{  

   }
}
```

> Example Response

```json-doc
{  
 "jsonrpc":"2.0",
 "id":0,
 "result":[  
    {  
       "EntryHash":"dde3f69025780f58da583b6961cf17291004f733fb2fa1a69738e0a7768387e4",
       "ChainID":"5c7a44a37870ca729d03820339379955781a863bc461545a9df06bbc15110bdb",
       "Status":"AckStatusACK"
    },
    {  
       "EntryHash":"45da41a07c6157839a735147a555ba4b009b72a9a7fe126c0d418413743f1683",
       "ChainID":"f6df2b40bf16be03deddc169a6429804a67a761ed5f2d5499f7e56a7202f854b",
       "Status":"AckStatusACK"
    }
 ]
}
```

Returns an array of the entries that have been submitted but have not been recoreded into the blockchain.

## transaction

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "transaction", "params":
{"hash":"f355ac4e3a0fa9d8a2f1bb2f169bc7a13a00a023e4280e22ec95f7b374ae429c"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"transaction",
   "params":{  
      "hash":"f355ac4e3a0fa9d8a2f1bb2f169bc7a13a00a023e4280e22ec95f7b374ae429c"
   }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "factoidtransaction": {
      "millitimestamp": 1481322322340,
      "inputs": [
        {
          "amount": 201144428,
          "address": "a675d5ad742ccc4f33f5769724e1522be33cc8b09e57e0e73a25c2227847811b",
          "useraddress": ""
        }
      ],
      "outputs": [
        {
          "amount": 200000000,
          "address": "646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc428",
          "useraddress": ""
        }
      ],
      "outecs": [],
      "rcds": [
        "f06f190d3307f52ff56e2ea6874250cb8ce0332dcc809b80100493b1ff064c59"
      ],
      "sigblocks": [
        {
          "Signatures": [
            "cdf206701b87f5f32d3871e20916af11f5d1dc5774bc386c3f543f553c2430207f3948ef69f311750aac4f2b10b4deb61e349389068bbe39f4d462ccda85380d"
          ]
        }
      ],
      "blockheight": 0
    },
    "includedintransactionblock": "",
    "includedindirectoryblock": "",
    "includedindirectoryblockheight": -1
  }
}
```

Retrieve details of a factoid transaction using a transactions hash.

## pending-transactions

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "pending-transactions", "params":
{"Address":"EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwrcmgm2r"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"pending-transactions",
   "params":{  
      "Address":"EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwrcmgm2r"
   }
}
```

> Example Response

```json-doc
{"jsonrpc":"2.0","id":0,"result":[{
    "TransactionID": "337a32712f14c5df0b57a64bd6c321a043081688ecd4f33fd8319470da2256b1",
    "Status": "AckStatusACK"
  }]}
```

Returns an array of factoid transactions that have not yet been recorded in the blockchain, but are known to the system.

## chain-head

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
"chain-head", "params":{"ChainID":"5a77d1e9612d350b3734f6282259b7ff0a3f87d62cfef5f35e91a5604c0490a3"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "chain-head",
  "params": {
    "ChainID": "bb4e132bb2f8792c3174f5c1de108816c36cee86a383e1067926353e41f334bc"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "ChainHead": "f65f67774139fa78344dcdd302631a0d646db0c2be4d58e3e48b2a188c1b856c"
  }
}
```

Return the keymr of the head of the chain for a chain ID (the unique hash created when the chain was created).

## entry-credit-balance

> Example Request

```shell
curl -X POST --data-binary {"jsonrpc": "2.0", "id": 0, "method": 
"entry-credit-balance", "params":
{"address":"EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwrcmgm2r"}} \
-H content-type:text/plain; http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "entry-credit-balance",
  "params": {
    "address": "EC3MAHiZyfuEb5fZP2fSp2gXMv8WemhQEUFXyQ2f2HjSkYx7xY1S"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "balance": 2000
  }
}
```

Return its current balance for a specific entry credit address.

## factoid-balance

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": 
"factoid-balance", "params":{"address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "factoid-balance",
  "params": {
    "address": "FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "balance": 966582271
  }
}
```

This call returns the number of Factoshis (Factoids *10^-8) that are currently available at the address specified.

## entry-credit-rate

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, 
"method": "entry-credit-rate"}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "entry-credit-rate"
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "rate": 95369
  }
}
```
Returns the number of Factoshis (Factoids *10^-8) that purchase a single Entry Credit. The minimum factoid fees are also determined by this rate, along with how complex the factoid transaction is.

## properties

> Example Request

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "properties"
}
```

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": 
"properties"}' -H 'content-type:text/plain;' http://localhost:8088/v2
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "factomdversion": "0.4.0.0",
    "factomdapiversion": "2.0"
  }
}
```

Retrieve current properties of the Factom system, including the software and the API versions.


## factoid-submit

>Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "factoid-submit", "params":
{"transaction":"0201565d109233010100b0a0e100646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc428afd7c200ce7b98bfdae90f942bc1fe88c3dd44d8f4c81f4eeb88a5602da05abc82ffdb5301718b5edd2914acc2e4677f336c1a32736e5e9bde13663e6413894f57ec272e28dc1908f98b79df30005a99df3c5caf362722e56eb0e394d20d61d34ff66c079afad1d09eee21dcd4ddaafbb65aacea4d5c1afcd086377d77172f15b3aa32250a"}}' \
 -H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"factoid-submit",
   "params":{  
      "transaction":"0201565d109233010100b0a0e100646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc428afd7c200ce7b98bfdae90f942bc1fe88c3dd44d8f4c81f4eeb88a5602da05abc82ffdb5301718b5edd2914acc2e4677f336c1a32736e5e9bde13663e6413894f57ec272e28dc1908f98b79df30005a99df3c5caf362722e56eb0e394d20d61d34ff66c079afad1d09eee21dcd4ddaafbb65aacea4d5c1afcd086377d77172f15b3aa32250a"
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "message":"Successfully submitted the transaction",
      "txid":"aa8bac391e744340140ea0d95c7b37f9cc8a58601961bd751f5adb042af6f33b"
   }
}
```

Submit a factoid transaction. The transaction hex encoded string is documented here: [Github Documentation](https://github.com/FactomProject/FactomDocs/blob/master/factomDataStructureDetails.md#factoid-transaction)

## commit-chain

> Example Request

```shell
curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "commit-chain", "params":
{"message":
"00015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c111f4f24c88d9c031b4124395c940e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac120237086112b5ef34fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"}}' \ 
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "commit-chain",
  "params": {
    "message": "00015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c111f4f24c88d9c031b4124395c940e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac120237086112b5ef34fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"
  }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "message":"Chain Commit Success",
      "txid":"76e123d133a841fe3e08c5e3f3d392f8431f2d7668890c03f003f541efa8fc61"
   }
}
```

Send a Chain Commit Message to factomd to create a new Chain. The commit chain hex encoded string is documented here: [Github Documentation](https://github.com/FactomProject/FactomDocs/blob/master/factomDataStructureDetails.md#chain-commit)

## reveal-chain

> Example Request

```
curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "reveal-chain", "params":
{"entry":
"007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531F000E0005746573745A0005746573745A48656C6C6F20466163746F6D21"}}' \
 -H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "reveal-chain",
  "params": {
    "entry": "007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531F000E0005746573745A0005746573745A48656C6C6F20466163746F6D21"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "message": "Entry Reveal Success",
    "entryhash": "f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60669854734"
  }
}
```

Reveal the First Entry in a Chain to factomd after the Commit to compleate the Chain creation. The reveal chain hex encoded string is documented here: [Github Documentation](https://github.com/FactomProject/FactomDocs/blob/master/factomDataStructureDetails.md#entry)

## commit-entry

> Example Request

```shell
curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "commit-entry", "params":
{"message":"00015507C1024BF5C956749FC3EBA4ACC60FD485FB100E601070A44FCCE54FF358D60669854734013B6A27BCCEB6A42D62A3A8D02A6F0D73653215771DE243A63AC048A18B59DA29F4CBD953E6EBE684D693FDCA270CE231783E8ECC62D630F983CD59E559C6253F84D1F54C8E8D8665D493F7B4A4C1864751E3CDEC885A64C2144E0938BF648A00"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "commit-entry",
  "params": {
    "message": "00015507C1024BF5C956749FC3EBA4ACC60FD485FB100E601070A44FCCE54FF358D60669854734013B6A27BCCEB6A42D62A3A8D02A6F0D73653215771DE243A63AC048A18B59DA29F4CBD953E6EBE684D693FDCA270CE231783E8ECC62D630F983CD59E559C6253F84D1F54C8E8D8665D493F7B4A4C1864751E3CDEC885A64C2144E0938BF648A00"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "message": "Entry Commit Success",
    "txid": "bf12150038699f678ac2314e9fa2d4786dc8984d9b8c67dab8cd7c2f2e83372c"
  }
}
```

Send an Entry Commit Message to factom to create a new Entry. The entry commit hex encoded string is documented here: [Github Documentation](https://github.com/FactomProject/FactomDocs/blob/master/factomDataStructureDetails.md#entry-commit)

## reveal-entry

> Example Request

```shell
curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "reveal-entry", "params":
{"entry":"007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531F000E0005746573745A0005746573745A48656C6C6F20466163746F6D21"}}' \
-H 'content-type:text/plain;' http://localhost:8088/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "reveal-entry",
  "params": {
    "entry": "007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531F000E0005746573745A0005746573745A48656C6C6F20466163746F6D21"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "message": "Entry Reveal Success",
    "entryhash": "f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60669854734"
  }
}
```

Reveal an Entry to factomd after the Commit to compleate the Entry creation. The reveal entry hex encoded string is documented here: [Github Documentation](https://github.com/FactomProject/FactomDocs/blob/master/factomDataStructureDetails.md#entry)

## send-raw-message

Send a raw hex encoded binary message to the Factom network. This is mostly just for debugging and testing.

### Commit Chain Example:

> Example Request

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "send-raw-message",
  "params": {
    "message": "0401554b9c15b100015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c111f4f24c88d9c031b4124395c940e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac120237086112b5ef34fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "message": "Successfully sent the message"
  }
}
```

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "send-raw-message", "params":
{"message":"0401554b9c15b100015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c1
11f4f24c88d9c031b4124395c940e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcce
b6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac12
0237086112b5ef34fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"}}' -H 'content-type:text/plain;' htt
p://localhost:8088/v2`

### Reveal Chain Example:

> Example Request

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "send-raw-message",
  "params": {
    "message": "0c01554b8e5881007e18ccc911f057fb111c7570778f6fdc51e189f35a6e6da683ec2a264443531f000e0005746573745a0005746573745a48656c6c6f20466163746f6d21"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "message": "Successfully sent the message"
  }
}
```

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "send-raw-message", "params":
{"message":"0c01554b8e5881007e18ccc911f057fb111c7570778f6fdc51e189f35a6e6da683ec2a264443531f000e0005746573745a0005746573
745a48656c6c6f20466163746f6d21"}}' -H 'content-type:text/plain;' http://localhost:8088/v2`

To Check:
ChainID : 7e18ccc911f057fb111c7570778f6fdc51e189f35a6e6da683ec2a264443531f
Entry Hash : f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60669854734

## errors

> Example Request

```shell
curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "method": "junk"}' -H 'content-type:text/plain;' http://localhost:8088/v2
```
```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "junk"
}
```

> Example Response

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "error": {
    "code": -32601,
    "message": "Method not found"
  }
}
```