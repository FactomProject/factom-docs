## Read Factom Entries

To read your Factom entries, you need the ChainID you used while creating your first chain. 

First, [Run FF](#run-factom-federation).

Use the get allentries command in the factom-cli Terminal window.

`factom-cli get allentries a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791`

<aside class="notice"><br>
Your ChainID will be different from the example above.
</aside>

> Terminal output for:<br>
> `factom-cli get allentries`

```shell
> factom-cli get allentries a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entry [0] {
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
ExtID: chainName
Content:
my first chain
}
Entry [1] {
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Content:
my first entry
}
```

Sample Terminal output is shown on the right.
<br>
<br>

<aside class="notice"><br>
You may notice that there are two entries in the new chain even though you only made one. This is because every time a new chain is created, it generates an entry containing it's assigned name. 
The second entry, *Entry [ 1 ]*, is the first entry we made in the new chain, the one we named "my first entry."
</aside>

This simple guide is designed to show how chains and entries work in Factom. Refer to the factom-cli help by typing the below command for more options.

`factom-cli -h`

You can then explore other ways and more command flags you can run to make entries suited for your needs.
We will also release more advanced guides in the near future, stay tuned.