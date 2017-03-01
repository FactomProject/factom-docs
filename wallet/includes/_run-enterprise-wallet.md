## Run Enterprise Wallet

*Time to remember Mr. Miyagi's lesson.*
 
This step will be used every time you need to run Enterprise Wallet, so get familiar with it. Practice makes perfect. Wax on, wax off.

Enterprise Wallet is a desktop app for Mac, Windows and Linux, which allows to run a wallet with a graphic user interface (GUI). There are 2 mothods to run the wallet, choose the one to suit your needs and skills best. Every time you come across **"Run Wallet"** you need to perform the following steps according to your choice below. These are the basic steps to run the wallet.

**Running Enterprise Wallet Online** means you can point to a remote factomd node and don't have to worry about using command line, factomd nor sync the blockchain. This option is probably the one best suited for most users who simply want to send and receive FCT or buy EC.

**Running Enterprise Wallet Locally** means also having to run factomd locally as well as sync the blockchain which can take a long time and require some command line skills. This option is a bit technical but can turn out to be more reliable as everything runs from your own machine.

<aside class="notice"><br>
The online wallet option is still experimental and the hosted factomd node may have reliability issues while we tune things, for production environments we recommend running your own local wallet and factomd nodes.
</aside> 

### Run Enterprise Wallet Online

<aside class="warning"><br>
There are two options, one for people who have run Factom Genesis (FG), our previous software release, and one for people who haven't. The former have to import their old FG wallet file, the latter don't, choose the next step accordingly.
</aside>

**If you have previously used Factom Genesis (FG)**, you need to import your FG wallet file (named *factoid_wallet_bolt.db*) the first time your run the Enterprise Wallet app to make sure all its previous addresses and balances are transferred over. You have learned how to backup your wallet file in our [Backup Your Wallet File!](#backup-your-wallets) guide and you should know if still in the default location within the .factom folder at ~/.factom/factoid_wallet_bolt.db.

If your old wallet file is in the default place you don't need to do anything, the new wallet will recognize the file and import it automatically. You can simply follow the same instructions for who has never used FG below. 

If your wallet file is not in the default location then you need to manually add it to ~/.factom/factoid_wallet_bolt.db.

If by any chance the operation fails, quit the wallet, delete the new wallet file located at ~/.factom/wallet/factoid_wallet.db and launch the wallet again until you get all your addresses back.

<aside class="success"><br>
Remember, you only need to do this once the first time you run Enterprise Wallet, thereafter you can run it normally. 
</aside>

Once you are happy continue by following the instructions below.

**If you have never used FG**, on Windows, Mac and Linux locate the Enterprise Wallet app and launch it.

At first launch it may show an error message under the "Transactions Tab".

![Online Wallet](images/wallet_091.png)

The first thing to do is to change the factomd node the wallet is pointing to. Go to "Settings", by default the wallet uses the local factomd instance at localhost:8088, hence why there was an error.

![Online Wallet 2](images/wallet_092.png)

Now click "Custom Factomd Location" and enter in a valid factomd instance. Use: factomd-live.cloudapp.net:8088 (copy and paste the address in the text field).

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

**README FIRST - Starting Factom**

Factom takes a while to download the blockchain. It can be expedited by downloading the first 70k blocks via HTTP. Factomd still checks the blockchain on each bootup, so it will check for inconsistencies in the download.

<aside class="notice"><br>
Note: currently factomd uses a lot of drive accesses when running. It is reccomended to hold the blockchain on a solid state drive. Running factomd on a spinning hard drive will be arduously slow. Since factomd currently scans the entire blockchain each time it is started, bootup takes a while (~30 min on an SSD). You can watch the progress on the Control Panel.
</aside>

Download the blockchain [here](https://www.factom.com/assets/site/factom_bootstrap.zip). 

Extract the zip file to your home directory. It will create files in the location: 

~/.factom/m2/main-database/ldb/MAIN/factoid_level.db/

<aside class="success"><br>
The newly created .factom folder is an invisible folder on Mac and Linux so you won't be able to see it unless you browse to it via Terminal. On Mac, in Finder, you can also use Go/Go to Folder... and type ~/.factom to see its content. 
</aside>

Compressed the blockchain is currently about 5 GB and uncompressed is over 9 GB.

After factomd boots and downloads the remaining blocks, it likely is not keeping up with minutes. To see if it is, on the control panel click the "More Detailed Node Information" button. Towards the right of the top line there will be a field "-/ 0". If the 0 number does not increase after a minute, then it is not keeping up with minutes.

In most cases factomd will need to be restarted after synching to the latest blockchain.

**Run Enterprise Wallet**

<aside class="warning"><br>
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
Syncing the Factom blockchain may take a little while, the blockchain is ...big. The Control Panel will display the progress and notify you when it has finished syncing. This will also occur when it has been a while since the last time you have run factomd.
</aside>

Once you are synced, in a new Terminal window browse (cd) to the location of your FF installation as you did above (Mac and Windows only).

<aside class="warning"><br>
There are two options now, one for people who have run Factom Genesis (FG), our previous software release, and one for people who haven't. The former have to import their old FG wallet file, the latter don't, choose the next step accordingly.
</aside>

**If you have previously used Factom Genesis (FG)**, you need to import your FG wallet file (named *factoid_wallet_bolt.db*) the first time your run the Enterprise Wallet app to make sure all its previous addresses and balances are transferred over. You have learned how to backup your wallet file in our [Backup Your Wallet File!](#backup-your-wallets) guide and you should know if still in the default location within the .factom folder at ~/.factom/factoid_wallet_bolt.db.

If your old wallet file is in the default place you don't need to do anything, the new wallet will recognize the file and import it automatically. You can simply follow the same instructions for who has never used FG below. 

If your wallet file is not in the default location then you need to manually add it to ~/.factom/factoid_wallet_bolt.db.

If by any chance the operation fails, quit the wallet, delete the new wallet file located at ~/.factom/wallet/factoid_wallet.db and launch the wallet again until you get all your addresses back.

<aside class="success"><br>
Remember, you only need to do this once the first time you run Enterprise Wallet, thereafter you can run it normally. 
</aside>

Once you are happy continue by following the instructions to run the the wallet below.

**If you have never used FG**, on Windows, Mac and Linux locate the Enterprise Wallet app and launch it.

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