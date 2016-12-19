## Send and Receive Factoids
**To send Factoids** (FCT) from your local wallet to an external Factoid Address (FA) you will need a source address and a destination address to execute the necessary command.

You need to perform this action when you want to send FCT to an exchange, a friend, or a third party.  
Assuming you have already [created a local FA address](#generate-a-factoid-address) (source address) and have a destination address, you will need to:
  
[Run FF](#run-factom-federation) (Yes, we know it's growing on you)

Then type the sendfct command with: <source FA> <destination FA> <Amount of FCT to send>

Here is an example.

`factom-cli sendfct FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.234`

<aside class="notice">
Note that your FA addresses and FCT amount will be different.
</aside>

> Terminal output for:<br>
> `factom-cli sendfct`

```shell
> factom-cli sendfct FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.234
TxID: 0de09676c65ad18179c5a27cfbfae4f0392a42773b4024aed71eca937f7ce7a6
```

Sample Terminal output is shown on the right.
<br>
<br>

In this example, the sendfct command moved 1.234 FCT from the source address to the destination address. You should be able to see the Transaction ID (TxID) on the terminal and in the Node Visualizer. 

![Factoid Transaction](images/cli_001.png)

**To receive Factoids** use the same command as above. For instance, you may move FCT between two FA addresses within your local wallet.

However, if you are sending yourself FCT from an exchange or want to receive FCT from a third party, just provide your FA Address. Once sent you can [verify your local FCT balance](#verify-fct-and-ec-balances).

<aside class="success">
The TxID is a very useful way to verify that FCT have moved to the correct address. We recommend noting it down especially when sending or receiving to and from a third party.
</aside>