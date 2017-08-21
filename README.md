# Read before making API doc changes
[![CircleCI](https://circleci.com/gh/FactomProject/factom-docs/tree/develop.svg?style=svg)](https://circleci.com/gh/FactomProject/factom-docs/tree/develop)

The docs have docs? Yes, they do.


## API Doc Formatting
There is a specific format that Slate likes when making changes to anything inside the api/ directory. The format will be documented here, and be mindful to stick to it.

The sections will be documented according to the header's markdown level (Amount of these \#\#)

###    Each \#\# Section

See the numbered list for a longer explanation. Be mindful each component MUST be followed by a newline. So a 1 line space between each component.

|Component Order|Markdown|
|:--|:--|
|(1) Title|\#\# METHOD_HERE|
|(2) Example Request| \> Example Request|
|(2.a) Shell Example| \`\`\`shell <br>EXAMPLE_SHELL<br> \`\`\`
|(2.b) Json Example| \`\`\`json <br>EXAMPLE_JSON<br> \`\`\`
|(3) Example Response| \> Example Response|
|(3.a) Json Example| \`\`\`json-doc <br>EXAMPLE_JSON<br> \`\`\`
|(4) Description | DESCRIPTION_HERE|


1) Section Name starts with a double pound sign, a SPACE, and the method in the curl. (the space is for consistency, it actually doesn't change anything. to Prove that, there is actually many leading spaces before the title of this section ;) )

2) Yes the Example Request MUST come before the description. That is how it knows to lay it next to the description, and not below it.

2.a) The shell example will look as shown. To break shell examples into more than one line, use '\' followed by NO SPACES so when copy pasting, the newline character is ignored. See other examples to know what I mean. The Json bits can be broken by a newline, but NEVER break up a string between two double quotes ""

2.b) I use https://jsonformatter.curiousconcept.com/ to format my json

3) Same as example request

3.a) Yup, json-doc. That way it is always shown, despite being on the 'curl' or 'json' tab.

4) Now your text

Full Example

<pre>
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

</pre>
