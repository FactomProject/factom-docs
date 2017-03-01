## Convert FCT to Entry Credits

*“It's still magic even if you know how it's done.”*
 
*-Terry Pratchett, A Hat Full of Sky* 

Before we automagically convert Factoids (FCT) to Entry Credits (EC), here is how the spell works. FCT are burned to create ECs. The number of FCT used will be deducted from your wallet's balance, so don't freak out when you see your FCT balance reduced. Just look for the newly created ECs on the EC address. Now if you don't see the newly created ECs, it's time to freakout and repeat these words, "Houston, we have a problem." (Disclaimer: Factom has no customer service center in Houston.)
Moving on...and getting down to business.

You will need a source address containing some FCT and a destination EC address to be able to to do this. In this example, we assume that you have already created a local EC address (destination) and you have some FCT in your local FA address (source).

To get ECs proceed as follows.

If you haven't already [Run Wallet](#run-enterprise-wallet).

Select "NEW TRANSACTION".

![Wallet 74](images/wallet_046.png)

Choose "BUY ENTRY CREDITS" from the menu.

![Wallet 75](images/wallet_066.png)

Simply select the amount of EC you'd like to buy and the wallet will figure out the rest and warn you if the balance is insufficient to cater for amount and fee. Our example show we have enough balance after selecting "VIEW TRANSACTION" with the prompt suggesting to either "SEND TRANSACTION" or "EDIT TRANSACTION".

![Wallet 76](images/wallet_067.png)

We also got confirmation of the transaction together with its ID from the wallet.

![Wallet 77](images/wallet_068.png)

You can then go back to your transactions list, select the transaction and get more info about it with "VIEW IN EXPLORER" or "LOCAL EXPLORER". 

<aside class="notice"><br>
Note, transactions in Factom confirm every 10 minutes so you may have to wait until the next 00, 10, 20, 30th, and so on, minute of every hour. For example if the time is 12:58, you have to wait 2 minutes until 13:00 before a transaction confirms.
</aside>

<aside class="success"><br>
Most user would be happy up to here with our guide for what they need, simply send and receive Factoids. However, we strongly recommend to read further to get familiar with other wallet uses, functions and settings.
</aside>

### Advanced EC Transactions

Go to settings and select "Enable coin control (specific or multiple input addresses for new transactions)". 

<aside class="notice"><br>
Note, "Enable ability to import/export transactions" doesn't apply to Entry Credits.
</aside>

This is to enable the advanced features.

![Wallet 78](images/wallet_069.png)

Then select "NEW TRANSACTION".

![Wallet 79](images/wallet_046.png)

Choose "BUY ENTRY CREDITS" from the menu.

![Wallet 80](images/wallet_062.png)

You can now select multiple input FA as well as EC addresses. In our example you can see we made an error in the amount of FCT required to buy 1500 EC thanks to "GET NEEDED INPUT" making the right estimate for us. When clicking on "VIEW TRANSACTION" the wallet prompted a warning message. 

![Wallet 81](images/wallet_063.png) 

So we corrected our mistake by specifying the right anount of FCT required, (1.430535 for 1500 EC).

![Wallet 82](images/wallet_064.png)

The transaction finally went through as we can see from the prompt with TxID
 
![Wallet 83](images/wallet_065.png)

<aside class="warning"><br>
Double check all details before using “SEND TRANSACTION”, if in doubt you can always try later when sure, transactions in Factom are irreversible.
</aside>

Once submitted, from your transactions list, select the transaction for info about confirmation, amounts, addresses and more with "VIEW IN EXPLORER" or "LOCAL EXPLORER".

You made it so far, you will be fine going forward. We have touched all of the advanced wallet features. Have a well deserved break! (clap)





