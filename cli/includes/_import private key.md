## Import a Private Key
To import a Factoid Address (FA) created with the Factoid Papermill app or by a third party you need the Factoid Private Key for the FA you want to import.
 
First, [Run FF](#run-factom-federation).

Then run the following command in the factom-cli Terminal window:

`factom-cli importaddress Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj`

<aside class="notice"><br>
Note that in our example we use a sample FA address Private Key, replace it with yours.<br>
</aside>

This will import the below address below to your local wallet.

FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC

> Terminal output for:<br>
> `factom-cli importaddress`

```shell
> factom-cli importaddress Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj
```

Sample Terminal output is shown on the right.
<br>
<br>


<br>
<br>
To verify that the FA address and its balance has successfully imported, run the listaddresses command to list all the addresses in your wallet.

`factom-cli listaddresses`

> Terminal output for:<br>
> `factom-cli listaddresses`

```shell
> factom-cli listaddresses
FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC 10
```

Sample Terminal output is shown on the right.
<br>
<br>

<aside class="notice"><br>
Our FA address has a balance of 10 factoids, but your balance will likely be different.
</aside>

You have successfully imported a Factoid Private Key and ready to use your balances! (thumbs up)