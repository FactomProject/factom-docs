## Redeem Factoids from Koinify
This section is relevant if you participated in the Koinify Software Token Sale hosted by Koinify back in 2015 and haven't redeemed your Factoids (FCT). Although Koinify closed their operations, they never held your FCT, and you only need your 12-word master passphrase to access your FCT.

The 12-word master passphrase can be used with the factom-cli importwords command to create the crypto signatures required to reassign the Factoids to another address or purchase Entry Credits. So go find that magical piece of paper where you wrote down your unique 12-word magic spell and follow the instructions below:

[Run FF](#run-factom-federation).

In this example we use the word "yellow" 12 times, but you probably have a different 12-word master passphrase.

In the factom-cli Terminal window run this command:

`factom-cli importwords "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"`

> Terminal output for:<br>
> `factom-cli importwords`

```shell
> factom-cli importwords "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"
FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1
```

Sample Terminal output is shown on the right.
<br>
<br>

The operation will create a new Factoid Address in your local wallet and present the public key in the terminal output. 
Make note of the FA address for your records. You will need it to verify that the FA address successfully imported with its balance.

Run the listaddresses command to list all the addresses in your wallet.

`factom-cli listaddresses`

> Terminal output for:<br>
> `factom-cli listaddresses`

```shell
> factom-cli listaddresses
FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1 20
```
Sample Terminal output is shown on the right.
<br>
<br>

In this example we successfully imported the FA address showing a balance of 20 factoids. The terminal output will give you a list of all FA and EC addresses in your wallet with their current balances. You can use the Node Visualizer or the Factom Explorer to [verify your local FCT balance](#verify-fct-and-ec-balances).

<aside class="notice">
In your case, the FA address and its balance will be different. 
</aside>

You can now trade your factoids on an exchange or use them to purchase Entry Credits. Life is good. (thumbs up)

<aside class="warning"><br>
The 12-word master passphrase was shown once at the time of purchase to contributors who were prompted to keep it in a safe place.
<br>
Without the Master Passphrase, it is impossible to redeem Factoids, and neither Factom nor Koinify can recover it. We really meant what we said.
<br>
Do not share your passphrase with anybody or they will be able to access your FCT.
<br>
There is no expiry date for the 12-word master passphrase. You will be able to redeem your FCT at your leisure, anytime in the future.
</aside>