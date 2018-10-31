# factom-walletd API

API reference documentation for factom-walletd. factom-walletd serves the wallet API on port 8089.

All these APIs use JSON-RPC, which is a remote procedure call protocol encoded in JSON. It is a very simple protocol (and very similar to XML-RPC), defining only a handful of data types and commands.

They can be invoked as:

`curl  -X GET --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "METHOD_NAME", "params":{"PARAM_1":"DATA_1"}}' -H 'content-type:text/plain;' http://localhost:8089/v2`

 The output will also be JSON.

 An example of a request and a response are given in the right panel for each of the RPC Methods.


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

When adding entry credit outputs, the amount given is in factoshis, not entry credits. This means math is required to determine the correct amount of factoshis to pay to get X EC.

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

Addfee is a shortcut and safeguard for adding the required additional factoshis to covert the fee. The fee is displayed in the returned transaction after each step, but addfee should be used instead of manually adding the additional input. This will help to prevent overpaying.

Addfee will complain if your inputs and outputs do not match up. For example, in the steps above we added the inputs first. This was done intentionally to show a case of overpaying. Obviously, no one wants to overpay for a transaction, so addfee has returned an error and the message: 'Inputs and outputs don't add up'. This is because we have 2,000,000,000 factoshis as input and only 1,000,000,000 + 10,000 as output. Let's correct the input by doing 'add-input', and putting 1000010000 as the amount for the address. It will overwrite the previous input.

Curl to do that:

`curl -X POST --data-binary '{"jsonrpc":"2.0","id":0,"method":"add-input","params":
{"tx-name":"TX_NAME","address":"FA2jK2HcLnRdS94dEcU27rF3meoJfpUcZPSinpb7AwQvPRY6RL1Q","amount":1000010000}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2`

Run the addfee again, and the `feepaid` and `feerequired` will match up


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

Adds an input to the transaction from the given address. The public address is given, and the wallet must have the private key associated with the address to successfully sign the transaction.

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

Adds a factoid address output to the transaction. Keep in mind the output is done in factoshis. 1 factoid is 1,000,000,000 factoshis.

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

Returns all of the identity key pairs that are currently stored in the wallet.

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

This method, compose-chain, will return the appropriate API calls to create a chain in factom. You must first call the [commit-chain](#commit-chain), then the [reveal-chain](#reveal-chain) API calls. To be safe, wait a few seconds after calling commit.

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

This method, compose-entry, will return the appropriate API calls to create an entry in factom. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit.

**Notes**:  
Ensure all data given in the `entry` fields are encoded in hex. This includes the content section.

## compose-identity-attribute

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-attribute",   "params": {"receiver-chainid": "string","destination-chainid": "string","attributes": "string","signerkey": "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C","signer-chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C","ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80","force": "false"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-attribute",
  "params": {
    "receiver-chainid": "string",
    "destination-chainid": "string",
    "attributes": "string",
    "signerkey": "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C",
    "signer-chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
    "ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80",
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

You can use this method help you replace one of the keys of an identity. This will need to be done if you feel that the key is compromised or have been in use for too long. Replacing a key is done by adding a structured entry on to the identity's Factom chain. The `compose-identity-key-replacement` method will return the API calls needed to create that entry.

The entry will be constructed based on the information you included in the request. 

`receiver-chainid`
This is the Chain ID for the identity receiving the endorsement.

`destination-chainid`
The Chain ID of the destination. Dream big.

`attributes`
The attribute you are attesting to.

`signer-chainid`
The `signer-chainid` leads to the Identity Chain of the signing party. 

`signerkey`
The `signerkey` should be the secret key of the lowest level key from the signer's Identity

The response you receive is similar to the [compose-entry](#compose-entry) response. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit.


## compose-identity-attribute-endorsement

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-attribute-endorsement", "params": {"destination-chainid": "string","entry-hash": "string","signerkey": "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C","signer-chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C","ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80","force": "false"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-attribute-endorsement",
  "params": {
    "destination-chainid": "string",
    "entry-hash": "string",
    "signerkey": "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C",
    "signer-chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
    "ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80",
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

This method helps you endorse an attribute that has already been registered on the Factom blockchain. To do this, you'll need to create a structured entry on to the Identity chain. The `compose-identity-attribute-endorsement` method will return the API calls needed to create that entry.

The entry will be constructed based on the information you included in the request. 

`destination-chainid`
This is the ID of the identity chain in question.

`entry-hash`
Sure, you need that too.

`signer-chainid`
The `signer-chainid` leads to the Identity Chain of the signing party. 

`signerkey`
The `signerkey` should be the secret key of the lowest level key from the signer's Identity

The response you receive is similar to the [compose-entry](#compose-entry) response. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit.

## compose-identity-chain

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-chain", "params": {"name":["Factom","Test","Identity"],"pubkeys": ["E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C","916782D56AC554826534746D37635A3739E17738D114EF4FF98FAAC610817D54","BDA798F34A9FF3F103380436D540BD5FCCFD6D00BA1CDDA0F6A27D3A58E471B3","ECA4BD2B2E4026F75D26AE8B96E321845CB0C691BD205F933E07DCA80B7DC86C"],"ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80"}}' \
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
      "Inc"
    ],
    "pubkeys": [
      "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C",
      "916782D56AC554826534746D37635A3739E17738D114EF4FF98FAAC610817D54",
      "BDA798F34A9FF3F103380436D540BD5FCCFD6D00BA1CDDA0F6A27D3A58E471B3",
      "ECA4BD2B2E4026F75D26AE8B96E321845CB0C691BD205F933E07DCA80B7DC86C"
    ],
    "ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80",
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
      "id": 2944,
      "params": {
        "message": "00015a9177f43d5df6e0e2761359d30a8275058e299fcc0381534545f55cf43e41983f5d4c9456abc6ea48b1287d0e5f2cf64798647221842e46b37e920cfaea62723c15195c320a9c707c2dfe35d43a21255c51012dae80cefbb14cf6571b6e195f5365bac7d30b3b6a27bcceb6a42d62a3a8d02a6f0d73653215771de243a63ac048a18b59da29e84f101bcf1d3a8ca45ad5c1a0ab3cf8ab935a2ad4f75914a0fb08e267facd9540cefe6833f3ea0295c3c2035bcd42a94e26477f096474b05e67538a34945a09"
      },
      "method": "commit-chain"
    },
    "reveal": {
      "jsonrpc": "2.0",
      "id": 2945,
      "params": {
        "entry": "22927282de49c4f6d19e9b2a9fa9b70a7edf96df3430b336553c1dca21ed8d0b"
      },
      "method": "reveal-chain"
    }
  }
}
```

The `compose-identity-chain` method will return the appropriate API calls to create an identity chain in factom. The chain will be constructed based on the name and public keys that you send in the request. The response you receive is similar to the [compose-chain](#compose-chain) response. You must first call the [commit-chain](#commit-chain), then the [reveal-chain](#reveal-chain) API calls. To be safe, wait a few seconds after calling commit.

## compose-identity-key-replacement

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "compose-identity-key-replacement", "params": {"chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C","oldkey": "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C","newkey": "86E30A28F45D91A205185576854A31620D8D705945ACB83BC0EDFA325228B9FD","signerkey": "916782D56AC554826534746D37635A3739E17738D114EF4FF98FAAC610817D54","ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80","force": "false"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "compose-identity-key-replacement",
  "params": {
    "chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
    "oldkey": "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C",
    "newkey": "86E30A28F45D91A205185576854A31620D8D705945ACB83BC0EDFA325228B9FD",
    "signerkey": "916782D56AC554826534746D37635A3739E17738D114EF4FF98FAAC610817D54",
    "ecpub": "564B030BB8FD5C22D1305EFB616F94043C66BC82C06ACD1B84F6AB5021A93A80",
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

You can use this method help you replace one of the keys of an identity. This will need to be done if you feel that the key is compromised or have been in use for too long. Replacing a key is done by adding a structured entry onto the identity's Factom chain. The `compose-identity-key-replacement` method will return the API calls needed to create that entry.

The entry will be constructed based on the information you included in the request. 

`chain_id`
This is the ID of the identity chain in question.

`oldkey`
The `oldkey` is the private key for the level to be replaced.

`newkey`
The `newkey` is the key that will be replacing it. 

`signerkey`
The `signerkey` is a private key that must be from the level directly above the `oldkey` in the Identity Chain.

The response you receive is similar to the [compose-entry](#compose-entry) response. You must first call the [commit-entry](#commit-entry), then the [reveal-entry](#reveal-entry) API calls. To be safe, wait a few seconds after calling commit.

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

Compose transaction marshals the transaction into a hex encoded string. The string can be inputted into the factomd API [factoid-submit](#factoid-submit) to be sent to the network.

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

Creates a new identity key and adds it to the wallet. New keys are generated from the same mnemonic seed used for FCT and EC addresses.

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

## identity-key

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "identity-key", "params":{"public":"idpub1y3Z1viJE3zTHDPYDgypJehEGY5BfZaHDkoSUeRvxdkH2SWWVr"}}' \
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

Given an identity public key as input, this command will respond with the corresponding public/private key pair from the wallet. If the desired identity key isn't currently stored in the wallet, an error is returned to indicate this.

## identity-keys-at-height

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "identity-keys-at-height", "params": {"chainid":"2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",    "height": "121393"}}' \
-H 'content-type:text/plain;' http://localhost:8089/v2
```

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "method": "identity-keys-at-height",
  "params": {
    "chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
    "height": "121393"
  }
}
```

> Example Response

```json-doc
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "chainid": "2321663B3B8A09CB4E701B84DEE49ABCE3C9D3EFDE867A9875E536D5ECEB653C",
    "height": "121393",
    "keys": [
      "E53DE57E2F3AA5244237B2E490DBAB9E7864E506137AE87DFB47247A5FEFAB9C",
      "916782D56AC554826534746D37635A3739E17738D114EF4FF98FAAC610817D54",
      "BDA798F34A9FF3F103380436D540BD5FCCFD6D00BA1CDDA0F6A27D3A58E471B3",
      "ECA4BD2B2E4026F75D26AE8B96E321845CB0C691BD205F933E07DCA80B7DC86C"
    ]
  }
}
```

This command will return the valid public keys for an identity at a given point in time. This is useful for validating old data. Time is indicated by the block height of the Factom blockchain at the desired time. This will return a set of four public keys.

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

## import-identity-keys

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "import-identity-keys", "params":{"keys":[{"secret":"idsec2rWrfNTD1x9HPPesA3fz8dmMNZdjmSBULHx8VTXE1J4D9icmAK"},{"secret":"idsec1iuqCFoiEfSZ1rU2FNpa7oFY3Kc29hHxP1R2PDyacJQEA8iShB"}]}}' \
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

Allows a user to add one or more identity keys to the wallet. Using the secret keys as input, the command will return the corresponding key pairs that were imported.

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

This will create a new transaction. The txid is in flux until the final transaction is signed. Until then, it should not be used or recorded.

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

Retrieve current properties of factom-walletd, including the wallet and wallet API versions.

## remove-identity-key

> Example Request

```shell
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "remove-identity-key", "params":{"public": "idpub26PEBWuumVp19yUSpfGJ2HPrTrU7hgw5empU7FPiTHdCKoy5Ao"}}' \
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

Given an identity public key, this command deletes the corresponding identity key pair from the wallet. Once executed, the user will no longer be able to retrieve that key pair or sign attributes/endorsements with the key pair from this wallet.

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

Signs the transaction. It is now ready to be executed.


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

When paying from a transaction, you can also make the receiving transaction pay for it. Using sub fee, you can use the receiving address in the parameters, and the fee will be deducted from their output amount.

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

Lists all the current working transactions in the wallet. These are transactions that are not yet sent.


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

