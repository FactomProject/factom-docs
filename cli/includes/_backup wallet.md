## Backup Your Wallet File!

**If you've used Factom Genesis (FG)**, our previous software release, you should have a local wallet file. We highly recommend you backup your (FG) wallet file every time you import or generate a new address. 
Do read this guide fully, at least once.

**If you have never run FG** you can skip the backup right now, but we strongly recommend backing up your new FF wallet once you get FF running. 

Get back to this guide when you are ready to do your backup, don't forget!

<aside class="warning"><br>
Factom Federation (FF) introduced a new way to generate addresses compared to our FG release. Simply put, it generates all new addresses from a seed. The seed is a 12-word passphrase which allows you to recover all your addresses, created with the seed in question, at a later date even if you lose your wallet file. There are many reasons why you may have misplaced your original wallet file such as because you changed computer, your hard drive failed, have overwritten the wallet file by mistake, and so on.<br>
<br> 
The seed comes to the rescue because if you ever lose your wallet file, you can always re-generate your addresses from it. However, some of you may have imported a Private Key generated with the Factoid Papermill app, or have imported a 12-word Koinify passphrase, or generated addresses with our previous FG wallet, these types of addresses are called "External Addresses." Please remember that a seed file will only allow you to recover addresses that were created with the same seed, external addresses will not be recovered.<br> 
<br>
So how to recover External Addresses?<br> 
<i>The simple way</i>: if you have any balances on addresses not generated from your wallet seed, you may want to transfer them to an address generated from your seed.<br> 
<i>The easy way</i>: keep a backup of your wallet file, whatever addresses are in there will always be, no need to recover them. 
<br> 
<i>The alternative way</i>: make sure to keep your external addresses' Private Keys safe, write them down or copy/paste them to a file, you can always import them even if you create a new wallet.<br>
<br>
Keep this in mind especially if you are migrating from our FG wallet to our FF wallet. If you are not careful, you may lose access to your Factoids and Entry Credits!
</aside>

**Backup your Factom Genesis (FG) wallet file**

Make sure to backup your FG wallet file before you run the new Factom Federation software. The wallet file is called "factoid_wallet_bolt.db" and is located in the .factom folder at the following locations:

* **Mac** `/Users/YourUsername/.factom/factoid_wallet_bolt.db`
* **Windows** `C:\Users\YourUsername\.factom\factoid_wallet_bolt.db`
* **Linux** `~/.factom/factoid_wallet_bolt.db`

<aside class="notice"><br>
Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for "how to show hidden files and folders on YOUR OS", replacing YOUR OS with Mac or Linux accordingly.
</aside>

**To backup** your FG wallet file, locate the factoid_wallet_bolt.db file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.

<aside class="success"><br>
By having a backup somewhere safe, if something goes wrong, you can always try again, but most importantly, you'll be able to import all your FG addresses and their balances into your new FF wallet the first time you run FF.
We will explain to you how to do that when "we cross that bridge" in the Run Factom Federation guide.
</aside>

**Backup your Factom Federation (FF) wallet file**

The wallet file is called "factom_wallet.db" and is located in the .factom folder at the following locations:

* **Mac** `/Users/YourUsername/.factom/wallet/factom_wallet.db`
* **Windows** `C:\Users\YourUsername\.factom\wallet\factom_wallet.db`
* **Linux** `~/.factom/wallet/factom_wallet.db` 

<aside class="notice"><br>
Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for "how to show hidden files and folders on YOUR OS," replacing YOUR OS with Mac or Linux accordingly.
</aside>

**To backup** your FF wallet file, quit factomd and factom-walletd, locate the factom_wallet.db file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.

**To create a fresh** FF wallet file, quit factomd and factom-walletd then move your wallet file to a safe location out of the .factom folder. There should be no wallet file in the .factom folder. Restart factomd and factom-walletd and a new empty wallet will be generated.

**To restore** a previous FF wallet file backup, quit factomd and factom-walletd, make sure you have a backup of the current wallet first, then drag & drop the previous backup in the .factom folder, overwrite if needed. Restart factomd and factom-walletd and your previous wallet will now be used instead.

<aside class="notice"><br>
Pay attention when performing backups and restores. Each wallet file has its unique seed and addresses. Overwriting a wallet may result in losing all your Factoids and Entry Credits. Not cool.
</aside>