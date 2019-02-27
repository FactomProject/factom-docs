# factom-walletd API

API reference documentation for factom-walletd. factom-walletd serves the wallet API on port 8089.

All these APIs use JSON-RPC, which is a remote procedure call protocol encoded in JSON. It is a very simple protocol (and very similar to XML-RPC), defining only a handful of data types and commands.

They can be invoked as:

`curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "METHOD_NAME", "params":{"PARAM_1":"DATA_1"}}' -H 'content-type:text/plain;' http://localhost:8089/v2`

 The output will also be JSON.

 An example of a request and a response are given in the right panel for each of the RPC Methods.


## active-identity-keys

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "active-identity-keys", "params": {"chainid":"3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",	"height": 163419}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "active-identity-keys",
  "params": {
	"chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
	"height": 163419
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
    "height": 163419,
    "keys": [
      "idpub2k8zGYQUfekxehyUKeqPw6QPiJ5hkV3bbc9JBgL7GNrEiqMpQX",
      "idpub3fXRj21gXveTk6RKYrpJniWV2pAanQktekEt62yhJUQXyPdvwL",
      "idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w"
    ]
  }
}
```

This command will return an identity's set of public keys (in order of decreasing priority) that were active at a specific block, or at the most recent height if the `"height"` parameter is not included. This is useful for validating entries containing identity signatures (e.g. on identity attributes and endorsements), allowing you to tell if a given signature was created with a key that was valid at the time that the entry was published. Time is measured in directory blocks.

As an example, let's say the identity at chain-id 3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae signs an entry using their level-3 key idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w, and publishes it to the blockchain at height 163420 and then replaces that key one block later at height 163421. Even though the key is no longer valid at the highest block height, we can tell that it was valid at the time that the signature was created, so we can still trust that the entry is authentic. However, if someone then published another entry signed with the key that was just replaced, we will be able to tell that the signer key is no longer valid and that the entry shouldn't be trusted.

If the wallet is encrypted, it must be unlocked prior to using this command.

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

When adding entry credit outputs, the amount given is in factoshis, not entry credits. This means math is required to determine the correct amount of factoshis to pay to get X EC. If the wallet is encrypted, it must be unlocked prior to using this command.

`(ECRate * ECTotalOutput)`

In our case, the rate is 1000, meaning 1000 entry credits per factoid. We added 10 entry credits, so we need 1,000 * 10 = 10,000 factoshis

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

Addfee is a shortcut and safeguard for adding the required additional factoshis to covert the fee. The fee is displayed in the returned transaction after each step, but addfee should be used instead of manually adding the additional input. This will help to prevent overpaying. If the wallet is encrypted, it must be unlocked prior to using this command.

Addfee will complain if your inputs and outputs do not match up. For example, in the steps above we added the inputs first. This was done intentionally to show a case of overpaying. Obviously, no one wants to overpay for a transaction, so addfee has returned an error and the message: 'Inputs and outputs don't add up'. This is because we have 2,000,000,000 factoshis as input and only 1,000,000,000 + 10,000 as output. Let's correct the input by doing 'add-input', and putting 1000010000 as the amount for the address. It will overwrite the previous input.

Curl to do that:

`curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-input","params":
{"tx-name":"TX_NAME","address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q","amount":1000010000}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2`

Run the addfee again, and the `feepaid` and `feerequired` will match up.


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

Adds an input to the transaction from the given address. The public address is given, and the wallet must have the private key associated with the address to successfully sign the transaction. If the wallet is encrypted, it must be unlocked prior to using this command.

The input is measured in factoshis, so to send ten factoids, you must input 1,000,000,000 factoshis (without commas in JSON)


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

Adds a factoid address output to the transaction. If the wallet is encrypted, it must be unlocked prior to using this command. Keep in mind the output is done in factoshis. 1 factoid is 1,000,000,000 factoshis.

So to send ten factoids, you must send 1,000,000,000 factoshis (no commas in JSON).


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

Retrieve the public and private parts of a Factoid or Entry Credit address stored in the wallet. If the wallet is encrypted, it must be unlocked prior to using this command.


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

Retrieve all of the Factoid and Entry Credit addresses stored in the wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

## all-identity-keys

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "all-identity-keys"}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "all-identity-keys"
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "keys": [
      {
        "public": "idpub1y3Z1viJE3zTHDPYDgypJehEGY5BfZaHDkoSUeRvxdkH2SWWVr",
        "secret": "idsec2euiiB66gaLQbhgLX36GBvfxQ11wvMgNmFAQ1YdcgsSjTcyzRT"
      },
      {
        "public": "idpub2EMSb17Rf9jWwoKigMa3EydLc3e8o7uhYbU5mDqpdcXuTymDWa",
        "secret": "idsec2rChEHLz3SPQQx3syQtB11pHAmxyGjux5FntnS7xqTCieHxxTc"
      },
      {
        "public": "idpub2Kcn1dbnz2KrvdST3c25gZfAWRGg9Up1VVg62obhEHvfPiogG2",
        "secret": "idsec2phztdmsMXisSeLUHGrWNraT6Vizu4LMG3GNuq2GRXxmq4dECu"
      },
      {
        "public": "idpub2ucJ6MTVNVGoGQdJKGk6DqtE7xcxYBa4WTuS8APuHHMHuh4M6W",
        "secret": "idsec1xuUyeCCrJhsojf2wLAZqRxPzPFR8Gidd9DRRid1yGy8ncAJG3"
      }
    ]
  }
}

```

Returns all of the identity key pairs that are currently stored in the wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

## compose-chain

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method":
 "compose-chain", "params": {"chain": {"firstentry":
 {"extids":["61626364", "31323334"], "content":"3132333461626364"}},
  "ecpub":"EC2DKSYyRcNWf7RS963VFYgMExo1824HVeCfQ9PGPmNzwrcmgm2r"}}'\
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"compose-chain",
   "params":{  
      "chain":{  
         "firstentry":{  
            "extids":[  
               "61626364",
               "31323334"
            ],
            "content":"3132333461626364"
         }
      },
      "ecpub":"EC2DKSYyRcNWf7RS963VFYgMExo1824HVeCfQ9PGPmNzwrcmgm2r"
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "commit":{  
         "jsonrpc":"2.0",
         "id":2885,
         "params":{  
            "message":"00015a9177f43d5df6e0e2761359d30a8275058e299fcc0381534545f55cf43e41983f5d4c9456abc6ea48b1287d0e5f2cf64798647221842e46b37e920cfaea62723c15195c320a9c707c2dfe35d43a21255c51012dae80cefbb14cf6571b6e195f5365bac7d30b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29e84f101bcf1d3a8ca45ad5c1a0ab3cf8ab935a2ad4f75914a0fb08e267facd9540cefe6833f3ea0295c3c2035bcd42a94e26477f096474b05e67538a34945a09"
         },
         "method":"commit-chain"
      },
      "reveal":{  
         "jsonrpc":"2.0",
         "id":2886,
         "params":{  
            "entry":"00e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b85500080002abcd000212341234abcd"
         },
         "method":"reveal-chain"
      }
   }
}
```

This method, compose-chain, will return the appropriate API calls to create a chain in factom. You must first call the [commit-chain](#commit-chain), then the [reveal-chain](#reveal-chain) API calls. To be safe, wait a few seconds after calling commit. If the wallet is encrypted, it must be unlocked prior to using this command.

**Notes**:  
Ensure that all data given in the `firstentry` fields are encoded in hex. This includes the content section.

## compose-entry

> Example Request

```shell
curl -X POST --data-binary '{ "jsonrpc": "2.0", "id": 0, "method":
 "compose-entry", "params": { "entry": 
 {"chainid":"48e0c94d00bf14d89ab10044075a370e1f55bcb28b2ff16206d865e192827645", 
 "extids":["cd90", "90cd"], "content":"abcdef"}, "ecpub":"EC2DKSYyRcNWf7RS963VFYgMExo1824HVeCfQ9PGPmNzwrcmgm2r"}}'\
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"compose-entry",
   "params":{  
      "entry":{  
         "chainid":"48e0c94d00bf14d89ab10044075a370e1f55bcb28b2ff16206d865e192827645",
         "extids":[  
            "cd90",
            "90cd"
         ],
         "content":"abcdef"
      },
      "ecpub":"EC2DKSYyRcNWf7RS963VFYgMExo1824HVeCfQ9PGPmNzwrcmgm2r"
   }
}
```

> Example Response

```json-doc
{  
   "jsonrpc":"2.0",
   "id":0,
   "result":{  
      "commit":{  
         "jsonrpc":"2.0",
         "id":2889,
         "params":{  
            "message":"00015a91804aa917606c4f9717f13e157e0b80c6f482888a62bd20440c7eb49f90393c9c279457013b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29e95f7957b0555b7cb80e93c6923b43e98e9a308503197af70af607fc30abc1b36d52b3388d0507460caf4d30a1be8fba80c5416f34bf6c0394e26a9a9814070a"
         },
         "method":"commit-entry"
      },
      "reveal":{  
         "jsonrpc":"2.0",
         "id":2890,
         "params":{  
            "entry":"0048e0c94d00bf14d89ab10044075a370e1f55bcb28b2ff16206d865e19282764500080002cd90000290cdabcdef"
         },
         "method":"reveal-entry"
      }
   }
}
```

This method, compose-entry, will return the appropriate API calls to create an entry in factom. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit. If the wallet is encrypted, it must be unlocked prior to using this command.

**Notes**:  
Ensure all data given in the `entry` fields are encoded in hex. This includes the content section.

## compose-identity-attribute

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-attribute",
"params": {"receiver-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
"destination-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
"attributes": [{"key":"email","value":"hello@factom.com"}],
"signerkey": "idpub2cw4NS4JZowXTwhGeo2tTGNvnjc5n2QvHBURdvVFCKRDuLEnBh",
"signer-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
"ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4", "force": false}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-attribute",
  "params": {
    "receiver-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
    "destination-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
    "attributes": [{"key":"email","value":"hello@factom.com"}],
    "signerkey": "idpub2cw4NS4JZowXTwhGeo2tTGNvnjc5n2QvHBURdvVFCKRDuLEnBh",
    "signer-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
    "ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4",
    "force": false
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "commit": {
      "jsonrpc": "2.0",
      "id": 2947,
      "params": {
        "message": "000166a2a21adec1891faa2cf5551dd93134639a77b000d598ab86c18efcd2d436119bfbb1ae4b0168abdd047316bdae088db51bf446fdeafd4b61792fb4d4d167d09f38a5ad3d14cfd19ff00159e7cbd56e3e309610f0c3664366fe32ded21da3e0489dce4ee4134e9fa82c579b71b353c53d8868f7b6949b92aa81e4ab5dceeed8e2f14c5b4500"
      },
      "method": "commit-entry"
    },
    "reveal": {
      "jsonrpc": "2.0",
      "id": 2948,
      "params": {
        "entry": "003b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae011200114964656e7469747941747472696275746500403362363964616265323263303134616639613962633964666137393137636534363032613033353739353937646466313834643864653536373032353132616500405391eb6024c14e5e0678dcac53f977f83811b471966d28d381314f7d46b72f8eba34cabd37051b7e26b46fdd3726c318d3800d874fd371da487f85e3921ede0100376964707562326377344e53344a5a6f775854776847656f327454474e766e6a63356e3251764842555264765646434b5244754c456e42680040336236396461626532326330313461663961396263396466613739313763653436303261303335373935393764646631383464386465353637303235313261655b7b226b6579223a22656d61696c222c2276616c7565223a2268656c6c6f40666163746f6d2e636f6d227d5d"
      },
      "method": "reveal-entry"
    }
  }
}
```

This request allows one identity to state an attribute about another identity and publish that entry to any existing chain. An attribute is a set of generic key:value pairs that can be assigned to an identity and is flexible enough to accommodate many different use-cases. In the example request, an identity is giving itself an attribute describing its current email address, and writing that entry to its own identity chain.  Each attribute must be in the format of `{"key":KEY, "value":VALUE}` where KEY and VALUE can be of any valid JSON type. Each attribute you wish to assign must be put into an array, even if it is just a single key/value pair. For example: `[{"key":"worksAt", "value":"Factom Inc."}, {"key":"isNice", "value":true}]` would be a valid attributes array to use as a parameter. If the wallet is encrypted, it must be unlocked prior to using this command.

The entry will be constructed based on the information you included in the request. 

- `receiver-chainid` - the Chain ID for the identity being assigned the attribute

- `destination-chainid` - the Chain ID where the attribute entry will be written. Could be any existing chain, dream big.

- `attributes` - the array of attributes that you are assigning to the receiver

- `signerkey` - the public identity key being used to sign the entry. Must be stored in the wallet already and should be a currently valid key for the signer identity.

- `signer-chainid` - the Identity Chain of the signing party (who is giving the attribute)

The response you receive is similar to the [compose-entry](#compose-entry) response. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit.


## compose-identity-attribute-endorsement

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-attribute-endorsement",
"params": {"destination-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
"entry-hash": "c07f1d89bb6c43e7e3166b9e53672110ff8077c367758fbe4265561c8b91e675",
"signerkey": "idpub2cw4NS4JZowXTwhGeo2tTGNvnjc5n2QvHBURdvVFCKRDuLEnBh",
"signer-chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
"ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4","force": "false"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-attribute-endorsement",
  "params": {
    "destination-chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
    "entry-hash": "c07f1d89bb6c43e7e3166b9e53672110ff8077c367758fbe4265561c8b91e675",
    "signerkey": "idpub2cw4NS4JZowXTwhGeo2tTGNvnjc5n2QvHBURdvVFCKRDuLEnBh",
    "signer-chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
    "ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4",
    "force": "false"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "commit": {
      "jsonrpc": "2.0",
      "id": 2947,
      "params": {
        "message": "00015a9177f43d5df6e0e2761359d30a8275058e299fcc0381534545f55cf43e41983f5d4c9456abc6ea48b1287d0e5f2cf64798647221842e46b37e920cfaea62723c15195c320a9c707c2dfe35d43a21255c51012dae80cefbb14cf6571b6e195f5365bac7d30b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29e84f101bcf1d3a8ca45ad5c1a0ab3cf8ab935a2ad4f75914a0fb08e267facd9540cefe6833f3ea0295c3c2035bcd42a94e26477f096474b05e67538a34945a09"
      },
      "method": "commit-entry"
    },
    "reveal": {
      "jsonrpc": "2.0",
      "id": 2948,
      "params": {
        "entry": "22927282de49c4f6d19e9b2a9fa9b70a7edf96df3430b336553c1dca21ed8d0b"
      },
      "method": "reveal-entry"
    }
  }
}
```

This method helps you endorse an attribute that has already been registered on the Factom blockchain. To do this, you'll need to create a structured entry on to the Identity chain. The `compose-identity-attribute-endorsement` method will return the API calls needed to create that entry. If the wallet is encrypted, it must be unlocked prior to using this command.

An "endorsement" is a statement that one identity agrees with, recognizes, or co-signs an attribute that has been given to another identity. In the example request, we created an endorsement entry that points to the email attribute entry we gave in the previous section. Depending on the application context this could mean different things. One such use-case would be to reconfirm that the attribute is still valid and that email address is still correct at present. Just like attributes, endorsements are very generic so that they can be used in a variety of ways.

The entry will be constructed based on the information you included in the request:

- `destination-chainid` - the Chain ID where the attribute entry will be written. Could be any existing chain, dream big.

- `entry-hash` - the entry hash of the attribute that will be endorsed

- `signerkey` - the public identity key being used to sign the entry. Must be stored in the wallet already and should be a currently valid key for the signer identity.

- `signer-chainid` - the Identity Chain of the signing party (who is endorsing the attribute located at `entry-hash`) 

The response you receive is similar to the [compose-entry](#compose-entry) response. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit.

## compose-identity-chain

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-chain", 
"params": {"name":["Factom","Test","Identity"], "pubkeys": ["idpub2k8zGYQUfekxehyUKeqPw6QPiJ5hkV3bbc9JBgL7GNrEiqMpQX",
"idpub3fXRj21gXveTk6RKYrpJniWV2pAanQktekEt62yhJUQXyPdvwL","idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w"],
"ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4", "force": false}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-chain",
  "params": {
    "name": [
      "Factom",
      "Test",
      "Identity"
    ],
    "pubkeys": [
      "idpub2k8zGYQUfekxehyUKeqPw6QPiJ5hkV3bbc9JBgL7GNrEiqMpQX",
      "idpub3fXRj21gXveTk6RKYrpJniWV2pAanQktekEt62yhJUQXyPdvwL",
      "idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w"
    ],
    "ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4",
    "force": false
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "commit": {
      "jsonrpc": "2.0",
      "id": 2944,
      "params": {
        "message": "000166a25437f43d649a2896dcf342bf9a5cdf5ca7bfa4d54a06bc2c803dbb71934dbddf6004615594d0f413466a329f9d6b59e258e88c29b0612994a9fecac84d3102b74be780d309c8638ae88899a0c3971324797095ce712add73088d4d971ce4c1684646b80b68abdd047316bdae088db51bf446fdeafd4b61792fb4d4d167d09f38a5ad3d14a9b76caa1f4e769fccd8724fb5955f6dbe3f0e6a5600ae9e7ca01839be2dd998e88b1009708d34c68f6bc69f43405b877dacf0bed4553b692368e3efb10c6f07"
      },
      "method": "commit-chain"
    },
    "reveal": {
      "jsonrpc": "2.0",
      "id": 2945,
      "params": {
        "entry": "003b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae00180006466163746f6d00045465737400084964656e746974797b226964656e746974792d76657273696f6e223a312c226b657973223a5b226964707562326b387a4759515566656b78656879554b65715077365150694a35686b5633626263394a42674c37474e724569714d705158222c226964707562336658526a323167587665546b36524b5972704a6e695756327041616e516b74656b4574363279684a55515879506476774c222c226964707562324755315063617832506962483868485a673538664b5269534a4b5157516b57596b706d74375648316a4358426771703977225d7d"
      },
      "method": "reveal-chain"
    }
  }
}
```

The `compose-identity-chain` method will return the appropriate API calls to create an identity chain in factom. The chain will be constructed based on the name and public keys that you send in the request. The response you receive is similar to the [compose-chain](#compose-chain) response. You must first call the [commit-chain](#commit-chain), then the [reveal-chain](#reveal-chain) API calls. To be safe, wait a few seconds after calling commit. If the wallet is encrypted, it must be unlocked prior to using this command.

The chain to be created will contain the identity name as the ExtIDs of the first entry (a.k.a. the Chain Name) and also a JSON object in the Content field signifying the identity version and initial valid keys. This first set of keys are listed in order of decreasing priority. The first key is a "master" key of sorts that should be kept as securely as possible and used infrequently — it is the only key that can transfer complete ownership of an identity. The last key in the array is the lowest priority, meaning that it can be kept in less secure locations and used more frequently. A higher priority key can always just replace a lower priority key that was compromised or simply lost. For more information on key replacements, see the [compose-identity-key-replacement](#compose-identity-key-replacement) section.

## compose-identity-key-replacement

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-key-replacement",
"params": {"chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
"oldkey": "idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w",
"newkey": "idpub2cw4NS4JZowXTwhGeo2tTGNvnjc5n2QvHBURdvVFCKRDuLEnBh",
"signerkey": "idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w",
"ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4","force": false}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-key-replacement",
  "params": {
    "chainid": "3b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae",
    "oldkey": "idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w",
    "newkey": "idpub2cw4NS4JZowXTwhGeo2tTGNvnjc5n2QvHBURdvVFCKRDuLEnBh",
    "signerkey": "idpub2GU1Pcax2PibH8hHZg58fKRiSJKQWQkWYkpmt7VH1jCXBgqp9w",
    "ecpub": "EC2ZFTmTv5Fs7UyKZzxY8km4jF635VkhR5KKBMzNP4BK4fPKaVw4",
    "force": false
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "commit": {
      "jsonrpc": "2.0",
      "id": 2947,
      "params": {
        "message": "000166a287a1188512f61e16dd9c90200cf2e2da58cb94b091a8a3cc52dc605fe6a95ec079ada20168abdd047316bdae088db51bf446fdeafd4b61792fb4d4d167d09f38a5ad3d14f796fd9e35bc3cff5f9b15b64fe48ad45532a3c490d07815f150c281478c87e85d8f3e8f8d926fe53eb15b706f85b1fef4f8e595ad83f43d0bf906ab237e1b06"
      },
      "method": "commit-entry"
    },
    "reveal": {
      "jsonrpc": "2.0",
      "id": 2948,
      "params": {
        "entry": "003b69dabe22c014af9a9bc9dfa7917ce4602a03579597ddf184d8de56702512ae00f9000a5265706c6163654b657900376964707562324755315063617832506962483868485a673538664b5269534a4b5157516b57596b706d74375648316a435842677170397700376964707562326377344e53344a5a6f775854776847656f327454474e766e6a63356e3251764842555264765646434b5244754c456e426800409fe26bf14754a65a1cb19ce97edae87b3639589188073c639b465df44f919a17595e25f5d346b208d056b89805c34c18680b46f2d40c2e43dc20abe14afe1e0300376964707562324755315063617832506962483868485a673538664b5269534a4b5157516b57596b706d74375648316a4358426771703977"
      },
      "method": "reveal-entry"
    }
  }
}
```

Replacing one of an identity's keys is done by adding a structured entry onto the identity's chain. This will need to be done if you feel that a key was compromised or has been in use for too long. The `compose-identity-key-replacement` method will return the API calls needed to create the replacement entry. The response you receive is similar to the [compose-entry](#compose-entry) response. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit. If the wallet is encrypted, it must be unlocked prior to using this command.

The entry will be constructed based on the information you included in the request. 

- `chainid` - the ChainID of the identity chain in question

- `oldkey` - the public identity key for the level to be replaced

- `newkey` - the public identity key that will be replacing `oldkey`

- `signerkey` - the public identity key that will sign the entry and authorize the replacement. This key must be stored in the wallet already and must be of the same or higher priority than the `oldkey` in the context of the given Identity Chain. 

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

Compose transaction marshals the transaction into a hex encoded string. The string can be inputted into the factomd API [factoid-submit](#factoid-submit) to be sent to the network. If the wallet is encrypted... you know the drill.

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

Deletes a working transaction in the wallet. The full transaction will be returned, and then deleted. If the wallet is encrypted, it must be unlocked prior to using this command.


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

Create a new Entry Credit Address and store it in the wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

## generate-factoid-address

> Example Request

```shell
curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "generate-factoid-address"}' \ 
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


Create a new Factoid Address and store it in the wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

## generate-identity-key

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "generate-identity-key"}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "generate-identity-key"
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "public": "idpub26PEBWuumVp19yUSpfGJ2HPrTrU7hgw5empU7FPiTHdCKoy5Ao",
    "secret": "idsec1kYsShFhYEfy28bkEJReHjR6AH9ybMZ4L9FDdYtb4VcRryaQsa"
  }
}
```

Creates a new identity key and adds it to the wallet. New keys are generated from the same mnemonic seed used for FCT and EC addresses. If the wallet is encrypted, it must be unlocked prior to using this command.

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

Get the current hight of blocks that have been cached by the wallet while syncing. You can run this command even if a wallet is currently locked.

## identity-key

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "identity-key",
"params":{"public":"idpub1y3Z1viJE3zTHDPYDgypJehEGY5BfZaHDkoSUeRvxdkH2SWWVr"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "identity-key",
  "params": {
    "public": "idpub1y3Z1viJE3zTHDPYDgypJehEGY5BfZaHDkoSUeRvxdkH2SWWVr"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "public": "idpub1y3Z1viJE3zTHDPYDgypJehEGY5BfZaHDkoSUeRvxdkH2SWWVr",
    "secret": "idsec2euiiB66gaLQbhgLX36GBvfxQ11wvMgNmFAQ1YdcgsSjTcyzRT"
  }
}
```

Given an identity public key as input, this command will respond with the corresponding public/private key pair from the wallet. If the desired identity key isn't currently stored in the wallet, an error is returned to indicate this. If the wallet is encrypted, it must be unlocked prior to using this command.

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

Import Factoid and/or Entry Credit address secret keys into the wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

## import-identity-keys

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "import-identity-keys",
"params":{"keys":[{"secret":"idsec2rWrfNTD1x9HPPesA3fz8dmMNZdjmSBULHx8VTXE1J4D9icmAK"},
{"secret":"idsec1iuqCFoiEfSZ1rU2FNpa7oFY3Kc29hHxP1R2PDyacJQEA8iShB"}]}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "import-identity-keys",
  "params": {
    "keys": [
      {
        "secret": "idsec2rWrfNTD1x9HPPesA3fz8dmMNZdjmSBULHx8VTXE1J4D9icmAK"
      },
      {
        "secret": "idsec1iuqCFoiEfSZ1rU2FNpa7oFY3Kc29hHxP1R2PDyacJQEA8iShB"
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
    "keys": [
      {
        "public": "idpub2g25nPNZ2kf6KGTjthYdHT3nykDbwEUEPyGJ52fo55SHwtAvLA",
        "secret": "idsec2rWrfNTD1x9HPPesA3fz8dmMNZdjmSBULHx8VTXE1J4D9icmAK"
      },
      {
        "public": "idpub2cUE3EMmof6DfaVuprQWk3bfSa6s2D9NUKu2g12Wt7FkoRsDrg",
        "secret": "idsec1iuqCFoiEfSZ1rU2FNpa7oFY3Kc29hHxP1R2PDyacJQEA8iShB"
      }
    ]
  }
}
```

Allows a user to add one or more identity keys to the wallet. Using the secret keys as input, the command will return the corresponding key pairs that were imported. If the wallet is encrypted, it must be unlocked prior to using this command.

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

Import a Koinify crowd sale address into the wallet. In our examples we used the word "yellow" twelve times, note that in your case the master passphrase will be different. If the wallet is encrypted, it must be unlocked prior to using this command.

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

> Example Response

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

This will create a new transaction. The txid is in flux until the final transaction is signed. Until then, it should not be used or recorded. If the wallet is encrypted, it must be unlocked prior to using this command.

When dealing with transactions all factoids are represented in factoshis. 1 factoid is 1e8 factoshis, meaning you can never send anything less than 0 to a transaction (0.5).

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

Retrieve current properties of factom-walletd, including the wallet and wallet API versions. You can check the properties of a wallet even if it's currently locked.


## remove-address

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "remove-address",
"params":{"address": "EC3geo9QBmA1UGiwDApHHxoNQu5Xkc9rdBsk1XqPJP4ycDUGpooX"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "remove-address",
  "params": {
    "address": "EC3geo9QBmA1UGiwDApHHxoNQu5Xkc9rdBsk1XqPJP4ycDUGpooX"
  }
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
      "success": "true"
    }
}
```

**Be careful using this function! Ensure that you have backups of important keys before removing them.** Given a factoid or entry-credit address, this command deletes the corresponding key pair from the wallet. Once executed, the user will no longer be able to retrieve the private key or make transactions with the address from this wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

## remove-identity-key

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "remove-identity-key",
"params":{"public": "idpub26PEBWuumVp19yUSpfGJ2HPrTrU7hgw5empU7FPiTHdCKoy5Ao"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "remove-identity-key",
  "params": {
    "public": "idpub26PEBWuumVp19yUSpfGJ2HPrTrU7hgw5empU7FPiTHdCKoy5Ao"
  }
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
      "success": "true"
    }
}
```

**Be careful using this function! Ensure that you have backups of important keys before removing them.** Given an identity public key, this command deletes the corresponding identity key pair from the wallet. Once executed, the user will no longer be able to retrieve that key pair or sign attributes/endorsements with the key pair from this wallet. If the wallet is encrypted, it must be unlocked prior to using this command.

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

> Example Response

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

Signs the transaction. It is now ready to be executed. Make sure you unlock the wallet first.


## sub-fee

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method"
:"sub-fee","params": {"tx-name":"TX_NAME","address":
"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{  
   "jsonrpc":"2.0",
   "id":0,
   "method":"sub-fee",
   "params":{  
      "tx-name":"TX_NAME",
      "address":"FA2H7gecy8Nr7cxF7ngtByW23PxvrysuzYMAiAhbRTddCWZTLs4P"
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

When paying from a transaction, you can also make the receiving transaction pay for it. Using sub fee, you can use the receiving address in the parameters, and the fee will be deducted from their output amount. Assuming you've unlocked your wallet, of course.

This allows a wallet to send all it's factoids, by making the input and output the remaining balance, then using sub fee on the output address.


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

Lists all the current working transactions in the wallet. These are transactions that are not yet sent. If the wallet is encrypted, it must be unlocked prior to using this command.


## transactions (Retrieving)

This command allows you to retrieve transactions made by this wallet. Since the transactions are public, this can be done even if a wallet is currently locked. There are a few ways to search for a transaction...

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

> Example Response 

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

> Example Response

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

This call in the backend actually pushes the request to factomd. For a more informative response, it is advised to use the <a href="#transaction">factomd transaction method</a>

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

Retrieves all transactions that involve a particular address.

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

*The developers were so preoccupied with whether or not they could, they didn’t stop to think if they should.*

The amount of data returned by this is so large, I couldn't get you a sample output as it froze my terminal window. It is strongly recommended to use other techniques to retrieve transactions; it is rarely the case to require EVERY transaction in the blockchain. If you are still determined to retrieve EVERY transaction in the blockchain, use other techniques such as using the 'range' method and specifically requesting for transactions between blocks X and Y, then incrementing your X's and Y's until you reach the latest block. This is much more manageable.


## unlock-wallet

> Example Request

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "unlock-wallet",
  "params": {
    "passphrase": "opensesame",
    "timeout": 300
  }
}
```

```shell
curl -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "unlock-wallet", "params":{"passphrase": "opensesame", "timeout": 300}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "success": true,
        "unlockeduntil": 1542062049
    }
}
```

Unlocks this wallet for the amount of time specified in seconds by `timeout`. The maximum amount of time a wallet can be unlocked for is 2<sup>30</sup> seconds (Roughly 34 Years... Give or take a decade).
This command will only work on wallets that are encrypted. If successful, returns the expiration time of your access as a Unix timestamp.

While the wallet is locked, the only accessible RPC API commands are `get-height`, `properties`, `transactions`, and `unlock-wallet`.

<aside class="notice"><br>
To see how to create a shiny new encrypted wallet, check the <a href="#creating-an-encrypted-wallet">securtity guide</a>.
</aside> 

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

Return the wallet seed and all addresses in the wallet for backup and offline storage. If the wallet is encrypted, it *definitely* must be unlocked prior to using this command.

## wallet-balances

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "wallet-balances"}'
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "wallet-balances"
}
```

> Example Response

```json-doc
{
    "jsonrpc": "2.0",
    "id": 0,
    "result": {
        "fctaccountbalances": {
            "ack": 1999857527000,
            "saved": 1999857527000
        },
        "ecaccountbalances": {
            "ack": 7893,
            "saved": 7893
        }
    }
}
```

The *wallet-balances* API is used to query the acknowledged and saved balances for all addresses in the currently running factom-walletd. The saved balance is the last saved to the database and the acknowledged or “ack” balance is the balance after processing any in-flight transactions known to the Factom node responding to the API call. The factoid address balance will be returned in factoshis  (a factoid is 10^8 factoshis) not factoids(FCT) and the entry credit balance will be returned in entry credits. 

* If walletd and factomd are not **both** running this call will not work.

* If factomd is not loaded up all the way to last saved block it will return:
"result":{"Factomd Error":"Factomd is not fully booted, please wait and try again."}

* If an address is not in the correct format the call will return:
“result”:{“Factomd Error”:”There was an error decoding an address”}

* If an address does not have a public and private address known to the wallet it will not be included in the balance.

* If the wallet is encrypted and locked, shame on you for trying this command. 

* `"fctaccountbalances"` are the total of all factoid account balances returned in factoshis. 
* `"ecaccountbalances"` are the total of all entry credit account balances returned in entry credits.  


## *Errors*

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

