## Convert Factoids to Entry Credits
*“It's still magic even if you know how it's done.”*<br> 
*― Terry Pratchett, A Hat Full of Sky*

Before we automagically convert Factoids (FCT) to Entry Credits (EC), here is how the spell works. FCT are burned to create ECs. The number of FCT used will be deducted from your wallet's balance, so don't freak out when you see your FCT balance reduced. Just look for the newly created ECs on the EC address. Now if you don't see the newly created ECs, it's time to freakout and repeat these words, "Houston, we have a problem." (Disclaimer: Factom has no customer service center in Houston.)

Moving on...and getting down to business.

You will need a source address containing some FCT and a destination EC address to be able to execute the necessary command.
  
In this example, we assume that you have already created a local EC address (destination) and you have some FCT in your local FA address (source).

To get ECs proceed as follows.

[Run FF](#run-factom-federation).

Then use the buyec command with: <source FA> <destination EC> <amount of EC to convert>.

`factom-cli buyec FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 30`

<aside class="notice">
Remember this is an example, and your FA and EC address, as well as the amount, will be different.
</aside>

> Terminal output for:<br>
> `factom-cli buyec`

```shell
> factom-cli buyec FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 30
TxID: f378ef393897d5cc5ef910eb3c9aeea5988dfdbb8b94a6cc6a31c5876f629b6a
```

Sample Terminal output is shown on the right.
<br>
<br>

The buyec command burned some Factoids from the FA address and deposited 30 EC in the specified EC address. The Terminal also presented the TxID (Transaction ID).

<aside class="success">
The TxID is useful for checking that ECs have moved to the right address. Take note of it for your records.
</aside>