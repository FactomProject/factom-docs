## Run Enterprise Wallet

*Time to remember Mr. Miyagi's lesson.*
 
This step will be used every time you need to run Enterprise Wallet, so get familiar with it. Practice makes perfect. Wax on, wax off.

Enterprise Wallet is a desktop app for Mac, Windows and Linux, which allows to run a wallet with a graphic user interface (GUI). There are 2 mothods to run the wallet, choose the one to suit your needs and skills best. Every time you come across **"Run Wallet"** you need to perform the following steps according to your choice below. These are the basic steps to run the wallet.

**Running Enterprise Wallet Online** means you can point to a remote factomd node and don't have to worry about using command line, factomd nor sync the blockchain. This option is probably the one best suited for most users who simply want to send and receive FCT or buy EC.

**Running Enterprise Wallet Locally** means also having to run factomd locally as well as sync the blockchain which can take a long time and require some command line skills. This option is a bit technical but can turn out to be more reliable as everything runs from your own machine.

<aside class="warning"><br>
The online wallet option is still experimental and the hosted factomd node may have reliability issues while we tune things, for production environments we recommend running your own local wallet and factomd nodes.
</aside> 

### Upgrade Your Old Wallet File

<aside class="notice"><br>
This only applies to users who have previously run Factom Genesis and have an old wallet file. If running Factom for the first time you can skip this step. 
</aside>

If you have run our previous software release "Factom Genesis (FG)" you need to import your FG wallet file (named *factoid_wallet_bolt.db*) the first time your run the Enterprise Wallet app to make sure all its previous addresses and balances are transferred over. You have learned how to backup your wallet file in our [Backup Your Wallet File!](#backup-your-wallets) guide and you should know if still in the default location within the .factom folder at ~/.factom/factoid_wallet_bolt.db.

If your old wallet file is in the default place you don't need to do anything, the new wallet will recognize the file and import it automatically. You can simply follow the same instructions for who has never used FG below. 

If your wallet file is not in the default location then you need to manually add it to ~/.factom/factoid_wallet_bolt.db.

If by any chance the operation fails, quit the wallet, delete the new wallet file located at ~/.factom/wallet/factoid_wallet.db and launch the wallet again until you get all your addresses back.

<aside class="success"><br>
Remember, you only need to do this once the first time you run Enterprise Wallet, thereafter you can run it normally. 
</aside>

Once you are happy continue by following the instructions below to choose your wallet type.

### Choose Your Wallet Type

When you launch Enterprise Wallet you have the option to choose a "secure" or a "not secure" wallet, the former is encrypted the latter is unencrypted. 

Each option maintains a different wallet file. This means you can have both a non secure, and a secure wallet.

To open either one, just close and relaunch EnterpriseWallet, selecting the one you wish to open.

![Online Wallet 00](images/wallet_139.png)

**Secure Wallet**

To create a Secure Wallet simply click on the Secure Wallet button.

![Online Wallet 00](images/wallet_140.png)

You will then need to enter a strong password for your wallet, tick the box next to "I acknowledge that if I lose this password and my seed I will lose access to the wallet and its funds", and finally click the "Proceed to Encrypted Wallet" button to access the Secure Wallet. 

This will automatically generate a new "factom_wallet_encrypted.db" file in your .factom folder (which will be encrypted with the password you just chose). You will need the same password every time you want to access your Secure Wallet, make sure to write it down and keep it safe.

![Online Wallet 00](images/wallet_142.png)

This is what a secure wallet will look like:

![Online Wallet 00](images/wallet_143.png)

<aside class="notice"><br>
Opening a secure wallet will encrypt all private keys and the seed. Keep in mind this means that if you forget your password and seed, there is no recovery option.

Be careful selecting this option, When using an encrypted wallet, be sure to immediately <a href="#backup-your-wallets">back up your seed</a>. This allows you to regenerate your wallet if you lose the password or the database gets corrupted.

This option will not convert a v1 wallet if found on disk. This is intentional, as converting any wallet to an encrypted wallet means the original wallet still exists, and still insecure. Addresses and seeds can still be imported/exported using the settings and address book tabs.
</aside>

Once you are happy continue by following the instructions below for either the Online or Local Enterprise Wallet setup.

**Not Secure Wallet**

To create a Not Secure Wallet simply click on the Not Secure button.

![Online Wallet 00](images/wallet_141.png)

Make sure to tick the box next to "I acknowledge that my private keys will not be encrypted and are thus unprotected", and finally click the "Proceed to Unencrypted Wallet" button to access the Secure Wallet. 

![Online Wallet 00](images/wallet_144.png)

This is what a secure wallet will look like:

![Online Wallet 00](images/wallet_145.png)

<aside class="notice"><br>
A non-secure wallet does not use encryption, and therefore it can be accessed by other users on your machine or malware. This will leave your private keys exposed and unencrypted on your hard drive. Choose your options carefully and be sure to immediately <a href="#backup-your-wallets">back up your seed</a>.
</aside>

Once you are happy continue by following the instructions below for either the Online or Local Enterprise Wallet setup.

### Run Enterprise Wallet Online

On Windows, Mac and Linux locate the Enterprise Wallet app and launch it. 

At first launch it may show an error message under the "Transactions Tab".

![Online Wallet](images/wallet_091.png)

The first thing to do is to change the factomd node the wallet is pointing to. Go to "Settings", by default the wallet uses the local factomd instance at localhost:8088, hence why there was an error.

![Online Wallet 2](images/wallet_092.png)

Now click "Custom Factomd Location" and enter in a valid factomd instance. Use: courtesy-node.factom.com (copy and paste the address in the text field).

![Online Wallet 2](images/wallet_093.png)

Then click "Save Changes". 

You are now using an online version of factomd! No need to sync the whole blockchain, just the transactions.

<aside class="notice"><br>
If this is the first time you are running the wallet, now's a great time for a cup of tea! 
The wallet needs to catch up on transactions and may take some time while displaying "syncing transactions", however it doesn't take too long, just about the time to prepare and drink your tea.
</aside>

Once the wallet has synced all transactions it should look like below.

![Online Wallet 03](images/wallet_019.png)

The first thing you may want to do is change the wallet theme, for the purpose of this guide we will use the Dark Theme going forward.

Click on "Settings" on the bottom left and select "Enable dark theme", then hit "SAVE CHANGES".

![Online Wallet 04](images/wallet_020.png)

Here's how it will look like in dark.

![Online Wallet 05](images/wallet_021.png)

Pat yourself on the back for making it this far! You have now run Enterprise Wallet for the first time and managed to change its theme.

<aside class="success"><br>
There are other advanced features shown on the settings page and we will tell you more about them as we go along with our guides, for the time being we will use the wallet with default settings.
</aside>

### Run Enterprise Wallet Locally

<aside class="notice"><br>
For Mac and Windows, use the cd command with Terminal to browse to the location of your FF installation. On Linux, you will be able to run commands without having to browse the to install location.
</aside>

This step is required before you run factomd. 

In a new Terminal window, run

**Mac**

`cd /Applications/Factom/`

**Windows**

`cd C:\Program Files (x86)\Factom\`

On Mac, Windows and Linux, run "factomd" first

`factomd`

Then browse to [http://localhost:8090](http://localhost:8090) to see the Control Panel for your local FF node.

![node 01](images/wallet_018.png)

<aside class="notice"><br>
If this is the first time you are running FF, now's a great time to check your Facebook feed or take your dog on a walk. 
Syncing the Factom blockchain may take a little while, the blockchain is ...big. The Control Panel will display the progress and notify you when it has finished syncing. This will also occur when it has been a while since the last time you have run factomd. However, after the first full sync is complete, successive syncs are faster and you will only have to sync blocks since the last full sync.
<br>
You can alternatively download the first 70,000 blocks via disk image by following our <a href="#starting-factom-via-bootstrap">Bootstrap Guide</a>.
</aside>

On Windows, Mac and Linux locate the Enterprise Wallet app and launch it.

The wallet may show a warning while your factomd instance is syncing the blockchain.

![Wallet 00](images/wallet_094.png)

<aside class="notice"><br>
If this is the first time you are running the wallet, now's a great time for a cup of tea! 
The wallet needs to catch up on transactions and may take some time while displaying "syncing transactions", however it doesn't take too long, just about the time to prepare and drink your tea.
</aside>

Once the wallet has synced all transactions it should look like below.

![Wallet 01](images/wallet_019.png)

The first thing you may want to do is change the wallet theme, for the purpose of this guide we will use the Dark Theme going forward.
Click on "Settings" on the bottom left and select "Enable dark theme", then hit "SAVE CHANGES".

![Wallet 02](images/wallet_020.png)

Here's how it will look like in dark.

![Wallet 03](images/wallet_021.png)

Pat yourself on the back for making it this far! You have now run Enterprise Wallet for the first time and you managed to change its theme.

<aside class="success"><br>
There are other advanced features shown on the settings page and we will tell you more about them as we go along with our guides, for the time being we will use the wallet with default settings.
</aside>
