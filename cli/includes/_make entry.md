## Make a Factom Entry
Once you have created your first Factom chain and noted the ChainID you are ready to make your first entry! 
Writing an entry in Factom costs 1 Entry Credit.

First, [Run FF](#run-factom-federation).

In the factom-cli Terminal window run the addentry command as constructed below:

`echo "my first entry" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX`

<aside class="notice"><br>
In your case, the only differences will be the name between quotes, the ChainID, and the EC address.
The name of the entry can be anything you want. In our example "my first entry" is the name of the new entry.<br> 
Our ChainID a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 should be replaced by your own.<br>
Finally, the EC address above should be replaced by your own, again, make sure it has enough EC balance to cover for the fee.   
</aside>

> Terminal output for:<br>
> `factom-cli addentry`

```shell
> echo "my first entry" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
Commiting Entry Transaction ID: 1d6b9d7159a27b91cd389738eb2b3b01143aaaf39ef46388f47abb8b32698811
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entryhash: 2460e676d4f4c89ccf0608b2e3134421b9075fb956af76c02af78991e6faafdc
```

Sample Terminal output is shown on the right.
<br>
<br>

<aside class="success"><br>
To make additional entries, repeat these steps using the same ChainID.
</aside>

You are now officially a Factom Jedi!




