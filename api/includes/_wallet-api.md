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

```cURL
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

```cURL
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

```cURL
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

```cURL
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

```cURL
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

```cURL
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

```cURL
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

```cURL
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

```cURL
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

```cURL
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
