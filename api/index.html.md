---
title: API Documentation - factomd RPC API V2

language_tabs:
  - json


toc_footers:
  - <a href='https://docs.factom.com'>Factom API Documentation</a>
  - <a href='https://docs.factom.com'>Factom Foundation Wallet Documentation</a>
  - <a href='https://docs.factom.com'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/factomproject'>Factom on GitHub</a>
  - <a href='https://factom.com'>Back to FACTOM.COM</a>

includes:
  

search: true
---

# Introduction
This is the API reference for the factomd process. The API is designed for outside application to process transactions and interact with the
Factom federated servers. It's listening port can be configured and runs on 8088 by default.

All these APIs use JSON-RPC, which is a remote procedure call protocol encoded in JSON. It is a very simple protocol (and very similar to XML-RPC), defining only a handful of data types and commands.

They can be invoked as

`curl -X GET –data-binary <JSON input> "method": "directory-block"}' -H 'content-type:text/plain;' http://localhost:8088/v2`
 
 The output will also be JSON.

 An example of a request and a response are given in the Right Panel for each of the RPC Methods



# RPC Methods

##directory-block

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params":
{"KeyMR":"7d7f991a08178f88b4b48ec7d45e7a58c9eab5a404724136f14c0f0d741ba2aa"}, "method": "directory-block"}' -H
'content-type:text/plain;' http://localhost:8088/v2
`
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
> Example Response

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "header": {
            "prevblockkeymr": "59da2e17929da7d132e7f8d1c5c130195ae3960348d8b408563dc2b9dd2ce062",
            "sequencenumber": 22954,
            "timestamp": 1481304240
        },
        "entryblocklist": [{
            "chainid": "000000000000000000000000000000000000000000000000000000000000000a",
            "keymr": "5f6ba4e95cdce6cf3226a5b7e922885fc86dbfd38f4c842e9ab4d35f2fed08f7"
        }, {
            "chainid": "000000000000000000000000000000000000000000000000000000000000000c",
            "keymr": "52ce82963f1a70a6c88ed151e396400b34026a67a6eecf6669e3c5f3e2e18436"
        }, {
            "chainid": "000000000000000000000000000000000000000000000000000000000000000f",
            "keymr": "7a9b23445d01221830e50323e705262a89a67486a9dcdf966ef8c3f14d1411ff"
        }]
    }
}
```
##directory-block-head

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "directory-block-head"}' -H
'content-type:text/plain;' http://localhost:8088/v2
`
> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "directory-block-head"
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"keymr":
"36c360817761e0d92af464f7c2e94a7495104d6b0a6051218cc53e52d3d519b6"
}
}
```

##heights

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "heights"}' -H 'content-type:text/plain;'
http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "heights"
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"directoryblockheight": 14460,
"leaderheight": 22955,
"entryblockheight": 14460,
"entryheight": 14460,
"missingentrycount": 0,
"entryblockdbheightprocessing": 14460,
"entryblockdbheightcomplete": 14460
}
}
```

##raw-data
`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params":
{"hash":"1f2931558c0ef6ef9d40450fa3a49dc3a29d18c30ced91c791bbe6060d405e39"}, "method": "raw-data"}' -H
'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"raw-data",
"params":{
"hash":"1f2931558c0ef6ef9d40450fa3a49dc3a29d18c30ced91c791bbe6060d405e39"
}
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result":{
"data":"0561491594de81214ebd918f29d1f9f59266ea63ec76341162dc4a252a0225b9bb
4e132bb2f8792c3174f5c1de108816c36cee86a383e1067926353e41f334bc1f2931558c0e
f6ef9d40450fa3a49dc3a29d18c30ced91c791bbe6060d405e39"
}
}
```

##dblock-by-height
`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "dblock-by-height",
"params":{"height":14460}}' -H 'content-type:text/plain;' http://localhost:8088/v2
`
> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"dblock-by-height",
"params":{
"height": 1
}
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"dblock": {
"header": {
"version": 0,
"networkid": 4203931043,
"bodymr":

"7716df6083612597d4ef18a8076c40676cd8e0df8110825c07942ca5d30073b4",
"prevkeymr":
"fa7e6e2d37b012d71111bc4e649f1cb9d6f0321964717d35636e4637699d8da2",
"prevfullhash":
"469c7fdce467d222363d55ac234901d8acc61fd4045ae26dd54dac17c556ef86",
"timestamp": 24671414,
"dbheight": 14460,
"blockcount": 3,
"chainid":
"000000000000000000000000000000000000000000000000000000000000000d"
},
"dbentries": [
{
"chainid":
"000000000000000000000000000000000000000000000000000000000000000a",
"keymr":
"574e7d6178e04c92879601f0cb84a619f984eb2617ff9e76ee830a9f614cc9a0"
},
{
"chainid":
"000000000000000000000000000000000000000000000000000000000000000c",
"keymr":
"2a10f1678b9736f213ef3ac76e4f8aa910e5fed66733aa30dafdc91245157b3b"
},
{
"chainid":
"000000000000000000000000000000000000000000000000000000000000000f",
"keymr":
"cbadd7e280377ad8360a4b309df9d14f56552582c05100145ca3367e50adc497"
}
],
"dbhash":
"aa7d881d23aad83425c3f10996999d31c76b51b14946f7aca204c150e81bc6d6",
"keymr":
"18509c431ee852edbe1029d676217a0d9cb4fcc11ef8e9aef27fd6075167120c"
},
"rawdata":
"00fa92e5a37716df6083612597d4ef18a8076c40676cd8e0df8110825c07942ca5d30073b
4fa7e6e2d37b012d71111bc4e649f1cb9d6f0321964717d35636e4637699d8da2469c7fdce
467d222363d55ac234901d8acc61fd4045ae26dd54dac17c556ef86017874b60000387c000
00003000000000000000000000000000000000000000000000000000000000000000a574e7
d6178e04c92879601f0cb84a619f984eb2617ff9e76ee830a9f614cc9a0000000000000000
000000000000000000000000000000000000000000000000c2a10f1678b9736f213ef3ac76
e4f8aa910e5fed66733aa30dafdc91245157b3b00000000000000000000000000000000000
0000000000000000000000000000fcbadd7e280377ad8360a4b309df9d14f56552582c0510
0145ca3367e50adc497"
}
}
```

##ablock-by-height
`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params": {"height":1}, "method":
"ablock-by-height"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"ablock-by-height",
"params":{
"height": 14460
}
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"ablock": {
"header": {
"prevbackrefhash":
"77e4fb398e228ec9710c20988647a01e2259a40ab77e27c005baf7f2deae3415",
"dbheight": 14460,
"headerexpansionsize": 0,
"headerexpansionarea": "",
"messagecount": 4,
"bodysize": 516,
"adminchainid":
"000000000000000000000000000000000000000000000000000000000000000a",
"chainid":
"000000000000000000000000000000000000000000000000000000000000000a"
},
"abentries": [
{
"identityadminchainid":
"888888e238492b2d723d81f7122d4304e5405b18bd9c7cb22ca6bcbc1aab8493",
"prevdbsig": {
"pub":
"0186ad82617edf3565d944aa104590eb6adb338e92ee6fcd750c2ab2b2707e25",
"sig":
"5796cd49835088ea0d6b8e4a75611ebc674fb791d6e9ebc7f6e5bb1a5e86fc25a8a7742e8
f60870e2cb8523fd122ef54bb95ac94b3676b81e07c921ed2196508"
}
},

{
"identityadminchainid":
"888888fc37fa418395eeccb95ab0a4c64d528b2aeefa0d1632c8a116a0e4f5b1",
"prevdbsig": {
"pub":
"c845f47df202a649e2262d3da0e35556aab62e361425ad7d2e7813a215c8f277",
"sig":
"a5c976c4d18814916fc893f7b4dee78120d20e0deab2b04df2e3b67c2ea1123224db28559
ca6d022822388a5ce41128bf5a09ccbbd02b1c5b17a4152183a3d06"
}
},
{
"identityadminchainid":
"88888815ac8a1ab6b8f57cee67ba15aad23ab7d8e70ffdca064200738c201f74",
"prevdbsig": {
"pub":
"f18512813300d8c1d11e78216d0640ddcc35156a20b53d5ced351a7d5ad90010",
"sig":
"1051c165d7ad33e1f764bb96e5e661053da381ebd708c8ac137da2a1b6847eac07e83472d
4fa6096768c7904760c821e45b5ebe23a691cc5bad1b61937f9e303"
}
},
{
"identityadminchainid":
"888888271203752870ae5e6fa0cf96f93cf14bd052455ad476ab26de1ad2c077",
"prevdbsig": {
"pub":
"4f2d34f0417297e2e985e0cc6e4cf3d0814416d09f37af7375517ea236786ed3",
"sig":
"01206ff2963af7df29bb6749a4c29bc1eb65a48bd7b3ec6590c723e11c3a3c5342e72f9b0
79a58d77a2562c25289d799fadfc5205f1e99c4f1d5c3ce85432906"
}
}
],
"backreferencehash":
"1786de6a72311dd4b60c6608d60c2b9367642fb1ee6b867b2c9f4c57c87b8cba",
"lookuphash":
"574e7d6178e04c92879601f0cb84a619f984eb2617ff9e76ee830a9f614cc9a0"
},
"rawdata":
"000000000000000000000000000000000000000000000000000000000000000a77e4fb398
e228ec9710c20988647a01e2259a40ab77e27c005baf7f2deae34150000387c00000000040
000020401888888e238492b2d723d81f7122d4304e5405b18bd9c7cb22ca6bcbc1aab84930
186ad82617edf3565d944aa104590eb6adb338e92ee6fcd750c2ab2b2707e255796cd49835
088ea0d6b8e4a75611ebc674fb791d6e9ebc7f6e5bb1a5e86fc25a8a7742e8f60870e2cb85
23fd122ef54bb95ac94b3676b81e07c921ed219650801888888fc37fa418395eeccb95ab0a
4c64d528b2aeefa0d1632c8a116a0e4f5b1c845f47df202a649e2262d3da0e35556aab62e3
61425ad7d2e7813a215c8f277a5c976c4d18814916fc893f7b4dee78120d20e0deab2b04df
2e3b67c2ea1123224db28559ca6d022822388a5ce41128bf5a09ccbbd02b1c5b17a4152183
a3d060188888815ac8a1ab6b8f57cee67ba15aad23ab7d8e70ffdca064200738c201f74f18
512813300d8c1d11e78216d0640ddcc35156a20b53d5ced351a7d5ad900101051c165d7ad3
3e1f764bb96e5e661053da381ebd708c8ac137da2a1b6847eac07e83472d4fa6096768c790
4760c821e45b5ebe23a691cc5bad1b61937f9e30301888888271203752870ae5e6fa0cf96f

93cf14bd052455ad476ab26de1ad2c0774f2d34f0417297e2e985e0cc6e4cf3d0814416d09
f37af7375517ea236786ed301206ff2963af7df29bb6749a4c29bc1eb65a48bd7b3ec6590c
723e11c3a3c5342e72f9b079a58d77a2562c25289d799fadfc5205f1e99c4f1d5c3ce85432
906"
}
}
```

##ecblock-by-height

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params": {"height":1}, "method":
"ecblock-by-height"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"ecblock-by-height",
"params":{
"height": 14460
}
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"ecblock": {
"header": {
"bodyhash":
"ef7a85d4bf868e34aff4edce479f6ee412161e1faa3596a112cd5ef75e96f59c",
"prevheaderhash":
"add44ed20133c7b8c9500ab5819d3aee665fffcce7acb6baa098fa8210b43a8b",
"prevfullhash":
"2f1dd9e5f1ab34102f65dea55c1598e2344568d68c0511640b7f436295615746",
"dbheight": 14460,
"headerexpansionarea": "",
"objectcount": 10,
"bodysize": 20,
"chainid":
"000000000000000000000000000000000000000000000000000000000000000c",
"ecchainid":
"000000000000000000000000000000000000000000000000000000000000000c"
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
"rawdata":
"000000000000000000000000000000000000000000000000000000000000000cef7a85d4b
f868e34aff4edce479f6ee412161e1faa3596a112cd5ef75e96f59cadd44ed20133c7b8c95
00ab5819d3aee665fffcce7acb6baa098fa8210b43a8b2f1dd9e5f1ab34102f65dea55c159
8e2344568d68c0511640b7f4362956157460000387c00000000000000000a0000000000000

014010101020103010401050106010701080109010a"
}
}
```

##fblock-by-height

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params": {"height":1}, "method": "fblock-by-height"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"fblock-by-height",
"params":{
"height": 14460
}
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"fblock": {
"bodymr":
"e12db6a1945d513f066cab66c94dc5cca1b8f90997b95a47b46e70b1656f764a",
"prevkeymr":
"98f3a6bcd978080fb612359f131fdb73c6119dea1f45c977a3fa30dfd507ebf5",
"prevledgerkeymr":
"fe7734478375e16f92f9e5513dbc3f2e830dd2bb263801ba816129242ce83cfe",
"exchrate": 95369,
"dbheight": 14460,
"transactions": [
{
"millitimestamp": 1480284840637,
"inputs": [
],
"outputs": [
],

"outecs": [
],
"rcds": [
],
"sigblocks": [
],
"blockheight": 0
},
{
"millitimestamp": 1480284848556,
"inputs": [
{
"amount": 201144428,
"address":
"dfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f",
"useraddress": ""
}
],
"outputs": [
{
"amount": 200000000,
"address":
"031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f",
"useraddress": ""
}
],
"outecs": [
],
"rcds": [
"3f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac"
],
"sigblocks": [
{
"signatures": [
"68fd6905eeb276739b2541398db3b1b06d73f99a50803bac83eafabc24be656e26278af6f
e8070c85e861e21c39a56a5a422dd2d58dd65a7eeff849f6d02de04"
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

"address":
"dfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8f",
"useraddress": ""
}
],
"outputs": [
{
"amount": 400000000,
"address":
"031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f",
"useraddress": ""
}
],
"outecs": [
],
"rcds": [
"3f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac"
],
"sigblocks": [
{
"signatures": [
"363c20508bddf5a9d4762e2496a861a1f03ec0dc50389b836dec898a3b37c33a6f831edf0
57f48a961b2d336231a78137e7402a0ca3a1d5c186ce2bb79e44907"
]
}
],
"blockheight": 0
}
],
"chainid":
"000000000000000000000000000000000000000000000000000000000000000f",
"keymr":
"cbadd7e280377ad8360a4b309df9d14f56552582c05100145ca3367e50adc497",
"ledgerkeymr":
"886747480a30f833a27a819fe4b92fbd617cda028329fd2e4b87c7721ff65dea"
},
"rawdata":
"000000000000000000000000000000000000000000000000000000000000000fe12db6a19
45d513f066cab66c94dc5cca1b8f90997b95a47b46e70b1656f764a98f3a6bcd978080fb61
2359f131fdb73c6119dea1f45c977a3fa30dfd507ebf5fe7734478375e16f92f9e5513dbc3
f2e830dd2bb263801ba816129242ce83cfe00000000000174890000387c000000000b00000
71c020158a7da22bd000000020158a7da41ac010100dff4f06cdfda7feae63901816101867
6f141c5744397278c9021e1e9d36e89656c7abe8fdfaf8400031cce24bcc43b596af105167
de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9ac
f42f72da96d74acd64d2935d75971ac68fd6905eeb276739b2541398db3b1b06d73f99a508
03bac83eafabc24be656e26278af6fe8070c85e861e21c39a56a5a422dd2d58dd65a7eeff8
49f6d02de04020158a7da70a5010100b09dae6cdfda7feae639018161018676f141c574439
7278c9021e1e9d36e89656c7abe8fafd7c200031cce24bcc43b596af105167de2c03603c20
ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d7
4acd64d2935d75971ac7e503a078b7f5bac25333c54a724530b97d25b8c2a83f82fdde2499

87b8bf4a4ba3da41643b7723102c3506bae86f6347ae94b72e8ca4c14617d8d3ca57df7050
0020158a7da9f9f010100818fccb26cdfda7feae639018161018676f141c5744397278c902
1e1e9d36e89656c7abe8f818f86c600031cce24bcc43b596af105167de2c03603c20ada331
4a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64
d2935d75971aced5c095795dc3a2fdcf7689718d10f32be9c656049f169900eac51a34b3f1
cb2a0d35ba0a9440892219be15927a4702f062e29ac35238ece375bda4dea9a2a050002015
8a7dace9101010083ddb1806c031cce24bcc43b596af105167de2c03603c20ada3314a7cfb
47befcad4883e6f83dceb9400dfda7feae639018161018676f141c5744397278c9021e1e9d
36e89656c7abe8f013b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18
b59da29fdb846a8f9abcb8a1eda9556a8d5f8ef959d1649fddb5ba1ccd3a66b6bc919d8ed2
25b1273e671685812725a10a7bbac95f0ed9f128bcb3547b068fe3137e50500020158a7daf
d8201010081bfa3f46cdfda7feae639018161018676f141c5744397278c9021e1e9d36e896
56c7abe8f81bede8800031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befc
ad4883e6f013f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971a
c66080fa6968bd4b104f1f7a2b5f5bd30b05b066bca956ef28ae94a17f1e18fd102de60f76
12811707fda09df69802f5fe4438c1b7b750b57fcc4684c9235520100020158a7db2c7b010
100dff4f06cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8
fdfaf8400031cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f0
13f8f50d848f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac403165085
38da5dda6d029e6d8b7eca7b9a5074def82a1d78a0f04ac82fe1efbe14f01b01a6778d648e
e47c3acf6f9ab2c9f044087703d55f9901403b991780500020158a7db5b75010100dff4f06
cdfda7feae639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fdfaf84000
31cce24bcc43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d84
8f1973751c5776e2f34ab9acf42f72da96d74acd64d2935d75971ac4f050366992fe0a8fb8
939825e1286f096f8f1e3528d23e737a499ba73ac1c041501c77f8baf780b3cb915f630a07
ac2c0cb312bfb8c89b27ab550fef070a30500020158a7db8a6e010100b09dae6cdfda7feae
639018161018676f141c5744397278c9021e1e9d36e89656c7abe8fafd7c200031cce24bcc
43b596af105167de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c
5776e2f34ab9acf42f72da96d74acd64d2935d75971aca6d367d754fd45454c04fd090a68b
a4b02ad0316362a7fcd16f164f56d335e8ebd83a3f6e9f5dc1cae9a3ad4eb48a675b8c8b98
4a1989d359f2bcad368c9c60900020158a7dbb96001010083ddb1806c031cce24bcc43b596
af105167de2c03603c20ada3314a7cfb47befcad4883e6f83dceb9400dfda7feae63901816
1018676f141c5744397278c9021e1e9d36e89656c7abe8f013b6a27bcceb6a42d62a3a8d02
a6f0d73653215771de243a63ac048a18b59da29c59178bafe8aca410070ba26fd2d4eb6073
60f52a1b74b60f55a66a3c65bfc5c9ce9b03f6dd4880246723d8542c93fc935f988bc77cc3
b9f3d616b414005730300020158a7dbe85201010081bfa3f46cdfda7feae63901816101867
6f141c5744397278c9021e1e9d36e89656c7abe8f81bede8800031cce24bcc43b596af1051
67de2c03603c20ada3314a7cfb47befcad4883e6f013f8f50d848f1973751c5776e2f34ab9
acf42f72da96d74acd64d2935d75971ac363c20508bddf5a9d4762e2496a861a1f03ec0dc5
0389b836dec898a3b37c33a6f831edf057f48a961b2d336231a78137e7402a0ca3a1d5c186
ce2bb79e449070000"
}
}
```

##receipt
`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params":
{"hash":"0561491594de81214ebd918f29d1f9f59266ea63ec76341162dc4a252a0225b9"}, "method": "receipt"}' -H 'content-type:text/plain;' http://lo
calhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"receipt",
"params":{
"Hash":"0561491594de81214ebd918f29d1f9f59266ea63ec76341162dc4a252a0225b9"
}
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result":{
"Receipt":{
"Entry":////TODO
"MerkleBranch":////TODO
"EntryBlockKeyMR":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaa",
"DirectoryBlockKeyMR":"bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
bbbbbbbbbbbbb",
"BitcoinTransactionHash":"cccccccccccccccccccccccccccccccccccccccccccccccc
cccccccccccccccc",
"BitcoinBlockHash":"dddddddddddddddddddddddddddddddddddddddddddddddddddddd
dddddddddd"
}
}
}
```

##entry-block

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0,
"params":{"KeyMR":"f65f67774139fa78344dcdd302631a0d646db0c2be4d58e3e48b2a188c1b856c"},"method":"entry-block"}' -H
'content-type:text/plain;' http://localhost:8088/v2
`
> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"entry-block",
"params":{
"KeyMR":"f65f67774139fa78344dcdd302631a0d646db0c2be4d58e3e48b2a188c1b856c"
}
}
```

> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result":{
"Header:{
"BlockSequenceNumber":0,
"ChainID":"bb4e132bb2f8792c3174f5c1de108816c36cee86a383e1067926353e41f334bc",
"PrevKeyMR":"0000000000000000000000000000000000000000000000000000000000000
000",
"Timestamp":0,
"DBHeight":24
},
"EntryList":[]
}
}
```

##entry
Get an Entry from factomd specified by the Entry Hash.

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method":"entry","params":
{"Hash":"be5216cc7a5a3ad44b49245aec298f47cbdfca9862dee13b0093e5880012b771"}}' -H 'content-type:text/plain;'
http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method":"entry",
"params": {
"hash":
"be5216cc7a5a3ad44b49245aec298f47cbdfca9862dee13b0093e5880012b771"
}
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"chainid":
"ffd6a308e6ec9a746a84c33dbff73190e900f5ba2f8d27731d8c1a1d603a8230",
"content": "6869",
"extids": ["33343533343537383334"]
}
}
```

##pending-entries

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params": "", "method": "pending-entries"}' -H 'content-type:text/plain;' http://localhost:8088/
`

```json
//result
{
"jsonrpc": "2.0",
"id": 0,
"result": [{
"entryhash":
"bb4abd1c5eac490158ae0b25d9ff0453ece01e65e6fb9465c5661ea3d937ec90",
"chainid":
"6bd0ba63e1c6b34313b4050e82f9646cd551f2099cdd22119b5241fca15f32c1"
}]
}
```

##transaction

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params":
{"hash":"f355ac4e3a0fa9d8a2f1bb2f169bc7a13a00a023e4280e22ec95f7b374ae429c"}, "method": "transaction"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

```json
//result
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"factoidtransaction": {
"millitimestamp": 1481322322340,
"inputs": [
{
"amount": 201144428,
"address":
"a675d5ad742ccc4f33f5769724e1522be33cc8b09e57e0e73a25c2227847811b",
"useraddress": ""
}
],
"outputs": [
{
"amount": 200000000,
"address":
"646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc428",
"useraddress": ""
}
],
"outecs": [
],
"rcds": [
"f06f190d3307f52ff56e2ea6874250cb8ce0332dcc809b80100493b1ff064c59"
],
"sigblocks": [
{
"Signatures": [
"cdf206701b87f5f32d3871e20916af11f5d1dc5774bc386c3f543f553c2430207f3948ef6
9f311750aac4f2b10b4deb61e349389068bbe39f4d462ccda85380d"
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

##pending-transactions

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params":
{"Address":"EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwrcmgm2r"}, "method": "pending-transactions"}' -H
'content-type:text/plain;' http://localhost:8088/v2`

```
{
"TransactionID":"337a32712f14c5df0b57a64bd6c321a043081688ecd4f33fd8319470da2256b1", "Status":"AckStatusACK"
},
{
"TransactionID":"9f94b2c0e827ac4e09fa1a649d4f2296cf19654a8589700c395ace0066357b14", "Status":"AckStatusACK"
}

```

##chain-head

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0,
"params":{"ChainID":"5a77d1e9612d350b3734f6282259b7ff0a3f87d62cfef5f35e91a5604c0490a3"}, "method": "chain-head"}' -H
'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "chain-head",
"params":{
"ChainID":"bb4e132bb2f8792c3174f5c1de108816c36cee86a383e1067926353e41f334bc"
}
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result":{
"ChainHead":"f65f67774139fa78344dcdd302631a0d646db0c2be4d58e3e48b2a188c1b8
56c"
}
}
```

##entry-credit-balance

`curl -X POST --data-binary {"jsonrpc": "2.0", "id": 0, "params":
{"address":"EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwrcmgm2r"}, "method": "entry-credit-balance"} -H
content-type:text/plain; http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "entry-credit-balance",
"params":{
"address":"EC3MAHiZyfuEb5fZP2fSp2gXMv8WemhQEUFXyQ2f2HjSkYx7xY1S"
}
}
```

> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"balance": 2000
}
}
```

##factoid-balance

This call returns the number of Factoshis (Factoids *10^-8) that are currently available at the address specified.

`curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "params":{"address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"
}, "method": "factoid-balance"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "factoid-balance",
"params":{
"address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q"
}
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"balance": 966582271
}
}
```

##entry-credit-rate

This call returns the number of Factoshis (Factoids *10^-8) that purchase a single Entry Credit. The minimum factoid fees are also determined by
this rate, along which how complex the factoid transaction is.

`curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "entry-credit-rate"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "entry-credit-rate"
}
```
> Example Response

```json

{
"jsonrpc": "2.0",
"id": 0,
"result": {
"rate": 95369
}
}
```

##properties

`curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "properties"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"method": "properties"
}
```
> Example Response

```json

{
"jsonrpc": "2.0",
"id": 0,
"result": {
"factomdversion": "0.4.0.0",
"factomdapiversion": "2.0"
}
}
```

##factoid-submit

`curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "factoid-submit", "params":
{"transaction":"0201565d109233010100b0a0e100646f3e8750c550e4582eca5047546ffef89c13a175985e320232bacac81cc428afd7c200ce7b98b
fdae90f942bc1fe88c3dd44d8f4c81f4eeb88a5602da05abc82ffdb5301718b5edd2914acc2e4677f336c1a32736e5e9bde13663e6413894f57ec272
e28dc1908f98b79df30005a99df3c5caf362722e56eb0e394d20d61d34ff66c079afad1d09eee21dcd4ddaafbb65aacea4d5c1afcd086377d77172f15
b3aa32250a"}} -H 'content-type:text/plain;' http://localhost:8088/v2`

##commit-chain

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "params":
{"message":"00015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c111f4f24c88d9c03
1b4124395c940e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcceb6a42d62a3a8d0
2a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac120237086112b5ef3
4fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"}, "method": "commit-chain"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"params": {
"message":
"00015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1
c76466cb3bc3f3cc68d8b2c111f4f24c88d9c031b4124395c940e5e2c5ea496e8aaa2f5c95
6749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcceb6a
42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c53
5b26d0d446bc69b22c887c534297c7d01b2ac120237086112b5ef34fc6474e5e941d60aa05
4b465d4d770d7f850169170ef39150b"
},
"method": "commit-chain"
}
```

```json
//result
{
"jsonrpc":"2.0",
"id":0,
"result":
{
"message":"Chain Commit Success",
"txid":"1580788d133a9e21406e6406a4a85150fe450895117a4365f77affe0fe5899fd"
}
}
```

##reveal-chain

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "params":
{"entry":"007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531F000E0005746573745A0005746573745A48656
C6C6F20466163746F6D21"}, "method": "reveal-chain"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"params": {
"entry":"007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531
F000E0005746573745A0005746573745A48656C6C6F20466163746F6D21"},
"method": "reveal-chain"
}
```
> Example Response

```json
{
"jsonrpc": "2.0",
"id": 0,
"result": {
"message": "Entry Reveal Success",
"entryhash":
"f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60669854734"
}
}
```

##commit-entry

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "params":
{"entry":"00015507C1024BF5C956749FC3EBA4ACC60FD485FB100E601070A44FCCE54FF358D60669854734013B6A27BCCEB6A42D62A3
A8D02A6F0D73653215771DE243A63AC048A18B59DA29F4CBD953E6EBE684D693FDCA270CE231783E8ECC62D630F983CD59E559C625
3F84D1F54C8E8D8665D493F7B4A4C1864751E3CDEC885A64C2144E0938BF648A00"}, "method": "commit-entry"}' -H 'content-type:text/plain;'
http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"params": {
"entry":
"00015507C1024BF5C956749FC3EBA4ACC60FD485FB100E601070A44FCCE54FF358D606698
54734013B6A27BCCEB6A42D62A3A8D02A6F0D73653215771DE243A63AC048A18B59DA29F4C
BD953E6EBE684D693FDCA270CE231783E8ECC62D630F983CD59E559C6253F84D1F54C8E8D8
665D493F7B4A4C1864751E3CDEC885A64C2144E0938BF648A00"
},
"method": "commit-entry"
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result": {
"message":"Entry Commit Success",
"txid":"bf12150038699f678ac2314e9fa2d4786dc8984d9b8c67dab8cd7c2f2e83372c"
}
}
```

##reveal-entry

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "params":
{"entry":"007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531F000E0005746573745A0005746573745A48656
C6C6F20466163746F6D21"}, "method": "reveal-entry"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc": "2.0",
"id": 0,
"params": {
"entry":"007E18CCC911F057FB111C7570778F6FDC51E189F35A6E6DA683EC2A264443531
F000E0005746573745A0005746573745A48656C6C6F20466163746F6D21"
},
"method": "reveal-entry"
}
```

> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result": {
"message":"Entry Reveal Success",
"entryhash":"f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60669854
734"
}
}
```

##send-raw-message

Does the commit and reveal chain example as raw messages

Commit Chain Example

`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "params":
{"message":"0401554b9c15b100015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c1
11f4f24c88d9c031b4124395c940e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d606698547340b3b6a27bcce
b6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac12
0237086112b5ef34fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"}, "method": "send-raw-message"}' -H 'content-type:text/plain;' htt
p://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc":"2.0",
"id":0,
"params": {
"message":"0401554b9c15b100015507b2f70bd0165d9fa19a28cfaafb6bc82f538955a98
c7b7e60d79fbf92655c1bff1c76466cb3bc3f3cc68d8b2c111f4f24c88d9c031b4124395c9
40e5e2c5ea496e8aaa2f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60
6698547340b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da2
946c901273e616bdbb166c535b26d0d446bc69b22c887c534297c7d01b2ac120237086112b
5ef34fc6474e5e941d60aa054b465d4d770d7f850169170ef39150b"
},
"method":"send-raw-message"
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result": {
"message":"Successfully sent the message"
}
}
```

Reveal Chain Example
`curl -X POST --data '{"jsonrpc": "2.0", "id": 0, "params":
{"message":"0c01554b8e5881007e18ccc911f057fb111c7570778f6fdc51e189f35a6e6da683ec2a264443531f000e0005746573745a0005746573
745a48656c6c6f20466163746f6d21"}, "method": "send-raw-message"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

> Example Request

```json
{
"jsonrpc":"2.0",
"id":0,
"params": {
"message":"0c01554b8e5881007e18ccc911f057fb111c7570778f6fdc51e189f35a6e6da
683ec2a264443531f000e0005746573745a0005746573745a48656c6c6f20466163746f6d21
},
"method":"send-raw-message"
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"result": {
"message":"Successfully sent the message"
}
}
```

To Check:
ChainID : 7e18ccc911f057fb111c7570778f6fdc51e189f35a6e6da683ec2a264443531f
Entry Hash : f5c956749fc3eba4acc60fd485fb100e601070a44fcce54ff358d60669854734

##Encrypted Connections:

When factomd is run with TLS enabled, the calling program needs to specify the certificate file generated by factomd. This is how to use curl with
TLS:

`curl -X POST --cacert ~/.factom/m2/factomdAPIpub.cert --data-binary '{"jsonrpc":"2.0","id":0,"method":"properties"}' -H 'content-type:text/plain;' https://localhost:8088/v2`

##Password Protection:

When factomd is run with a password, it uses HTTP Basic Authentication. It is recommended to encrypt the connection when using a password,
because otherwise the password can be sniffed on the network. Here is how to run with just the password:

`curl -X POST -u userHere:securePassHere --data-binary '{"jsonrpc":"2.0","id":0,"method":"properties"}' -H 'content-type:text/plain;' http://localhost:8088/v2`

##Combined Password and Encryption:

`curl -X POST -u userHere:securePassHere --cacert ~/.factom/m2/factomdAPIpub.cert --data-binary '{"jsonrpc":"2.0","id":0,"method":"properties"}'
-H 'content-type:text/plain;' https://localhost:8088/v2`

##Creating Certificates:
Normally, when started the program creates a new certificate if one is not found. The certificates are bound to a set of specific IP addresses.
Normally it finds the IP address by asking the OS. When using cloud services that use a different public IP than the server sees (AWS, Azure) the

certificate needs to be told what the external IP address is manually. There are two options for this.
Edit the config file to show the external IP address instead of localhost for FactomdLocation
start factomd with the selfaddr flag and pass a comma separated list of authorized domains and IP addresses
factomd -tls=true -selfaddr=domain.net,123.23.111.444

##errors

> Example Response

```json
{
"jsonrpc":"2.0",
"id": 0,
"method":"junk"
}
```
> Example Response

```json
{
"jsonrpc":"2.0",
"id":0,
"error":{
"code":-32601,
"message":"Method not found"
}
}
```