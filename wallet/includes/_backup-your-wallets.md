## Backup Your Wallets!

When you first load up your enterprise wallet, you'll probably notice a message on the sidebar prompting you to back up your wallet. This is a way to maintain access to your factoids in case something happens to your Enterprise Wallet installation or your machine. We highly recommend backing up your wallets in a secure location. But hey, what do we know.... we only built it.

![Back That Thing Up](/images/wallet_145.png)

### Backing Up Your Wallet Seed

Addresses that you generate using the enterprise wallet are going to be based on a common seed. This seed is the most private of private keys. Anyone who has it can regenerate and claim all of the addresses that are spawned by it one by one. This means that it's a good idea to keep this seed around, but it's also smart to make sure that no one else can gain access to it. We'll give you a quick guide on how to get the seed for your wallet, but be sure to only go through these steps in a place where you can have some privacy.

To begin, select the Backup button on the sidebar. If you have some addresses that originate from another seed, you'll see a warning about those addresses first. The seed you're about to view does not cover these public keys... You won't be able to recreate them with your back up. On the main screen, this is notated by these addresses not have a filled star next to them. Once you've made a note of these uncovered addresses, you can move on to the next step with the continue button.

### Viewing your Seed Phrase

On the next page, you'll see a message reminding you once again to be sure that you're in a safe location. That guy standing behind you right now? Pretending to be disinterested? He can totally steal your factoids if he wants to. Don't give him a chance! Move to another room or shoo him away.

Once you've dealt with the factoid vampires, you can safely view the next screen. You'll see the twelve words that make up your seed phrase along with their proper order. You'll want to write (not type!) these words down on a piece of paper you can place in a secure location. For good measure, you can keep this article, which will probably begin to glow faintly with secrets, in a safe or safety deposit box. For bonus points, you can even use a cipher to obscure the actual words in your key phrase in case someone does get to the paper. For double bonus points, you can even forgo the paper altogether and commit the phrase to memory.

Whatever you do, just remember that if you lose access to or forget the key phrase, you won't be able to recreate your wallet. That defeats the purpose of this guide and, thus, is not recommended.

### Verify Your Seed Phrase

Finally, you'll be asked to verify your seed phrase. This gives you a chance to make sure you've properly recorded your seed phrase. If you can complete this step, you will have officially backed up your Factom Wallet. Congrats!

![Success!](/images/wallet_146.png)

### Importing a Seed

Importing your backed up wallet is just a matter of plugging in your seed phrases. To recall a wallet using this method, you'll need to make your way to the settings page. You can do this by clicking the button on the sidebar.

![Settings Button](/images/wallet_147.png)

Next, scroll down to the bottom of the page until you see the "Restore a Seed". You can click the orange button to proceed from here.

![Restore Button](/images/wallet_148.png)

Then, enter the seed phrases of the wallet you want to restore. If done properly, your seed will change to the one you have entered. However, if you go to the Address book, you may notice something... Not much has changed. While your addresses no longer have filled white stars next to them, the addresses themselves will be exactly as you left them. What gives?

Well, changing the seed doesn't actually pull your addresses back automatically. It simply gives you the mathematical base that you need to recreate those addresses. As you create new addresses based on the seed, you'll be recreating the addresses from your previous wallet. That means you have the private keys and access to the balances of those addresses as well. So to fully recreate your wallet, you need to repopulate your address book with those lost addresses. If you had five before, you'd get those same five addresses when you repopulate. And, of course, any addresses you had before you imported the new seed will still be there for you to use.

### External Addresses

As mentioned earlier, a backup of your Seed Phrases will not allow you to recreate addresses that are not based on that same seed. These are called external addresses and are marked by the open star that sits next to their entry in the address book.

![Open Star](/images/wallet_149.png)

So how do I recover External Addresses?
 
<i>The simple way</i>: if you have any balances on addresses not generated from your wallet seed, you may want to transfer them to an address generated from your seed.<br>
<i>The easy way</i>: keep a backup of your wallet file, whatever addresses are in there will always be, no need to recover them.<br>  
<i>The alternative way</i>: make sure to keep your external addresses' Private Keys safe, write them down or copy/paste them to a file, you can always import them even if you create a new wallet.


### Backup Wallet File

We have two types of wallets for users to choose from when using Enterprise Wallet: Secure Wallet (encrypted) and Not Secure Wallet (unencrypted). The wallet files have different names accordingly:

1. `factom_wallet_encrypted.dbis` (encrypted)
2. `factom_wallet.db` (unencrypted wallet file) 

They are located in the .factom folder at the following locations:

*Encrypted Wallet File Locations*

* **Mac** `/Users/YourUsername/.factom/wallet/factom_wallet_encrypted.dbis`
* **Windows** `C:\Users\YourUsername\.factom\wallet\factom_wallet_encrypted.dbis`
* **Linux** `~/.factom/wallet/factom_wallet_encrypted.dbis`

*Unencrypted Wallet File Locations*

* **Mac** `/Users/YourUsername/.factom/wallet/factom_wallet.db`
* **Windows** `C:\Users\YourUsername\.factom\wallet\factom_wallet.db`
* **Linux** `~/.factom/wallet/factom_wallet.db`

Learn more on how to setup a Secure or Not Secure Wallet by following the [Choose Your Wallet Type guide](#choose-your-wallet-type).

<aside class="notice"><br>  
Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for "how to show hidden files and folders on YOUR OS", replacing YOUR OS with Mac or Linux accordingly.
</aside>

**To backup** your FF wallet file, quit factomd and EnterpriseWallet, locate the factom_wallet.db or factom_wallet_encrypted.dbis file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.

### Restore/Refresh Wallet File

**To create a fresh** FF wallet file, quit factomd and EnterpriseWallet then move your wallet file to a safe location out of the .factom folder. There should be no wallet file in the .factom folder. Restart factomd and factom-walletd and a new empty wallet will be generated.

**To restore** a previous FF wallet file backup, quit factomd and EnterpriseWallet, make sure you have a backup of the current wallet first, then drag & drop the previous backup in the .factom folder, overwrite if needed. Restart factomd and factom-walletd and your previous wallet will now be used instead.

<aside class="warning"><br>
Pay attention when performing backups and restores. Each wallet file has its unique seed and addresses. Overwriting a wallet may result in losing all your Factoids and Entry Credits. Not cool.
</aside>