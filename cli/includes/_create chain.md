## Create a Factom Chain
To make entries in Factom, you must create a Factom Chain where your entries will be recorded. You can create as many chains as you like. Just remember, it's a BYOEC party. You know... *bring your own entry credit party*. (We know...what you are thinking. This is why we do Blockchains and not Standup)

Here is how to create your first Factom Chain.
 
Creating a chain in Factom has a fee of 10 Entry Credits, so make sure your EC address balance can cover it.

First, [Run FF](#run-factom-federation).

In the factom-cli Terminal window run the addchain command as shown below. 
  
`echo "my first chain" | factom-cli addchain -n chainName EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX`

<aside class="notice"><br>
In your case, the only differences will be the name between quotes and the EC address.<br>
Be sure to use your EC address (not our example).
</aside>
 
> Terminal output for:<br>
> `factom-cli addchain`

```shell
> echo "my first chain" | factom-cli addchain -n chainName EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
Committing Chain Transaction ID: c1a2861d14b788c13d6c48f1e5603f5c53afc599d07d338deeb4c3d5012e24da
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entryhash: 232d1e54ecdfc369cc66e35dda73ce4beb7dffd3e75af94192034e79beaf6c8f
```

You can name the chain whatever you want. In our example "my first chain" is the name of the new chain. 
 
Sample Terminal output is shown on the right.
<br>
<br>

<aside class="success"><br>
Take note of the ChainID as you will need it to make Factom entries later on.
</aside>
