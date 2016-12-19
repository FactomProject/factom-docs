# Run The Factom Foundation Wallet

*Time to remember Mr. Miyagi's lesson.*
 
This step will be used every time you need to run the Factom Foundation Wallet, so get familiar with it. Practice makes perfect. Wax on, wax off.
 
Every time you come across "Run Wallet" you need to perform the following steps. These are the basic steps to run the wallet.

<aside class="warning"><br>
For Mac and Windows, use the cd command with Terminal to browse to the location of your FF installation. On Linux, you will be able to run commands without having to browse the to install location.
</aside>

This step is required before you run factomd, and EnterpriseWallet. Both applications are required to run the Factom Foundation Wallet.
In a new Terminal window, run

**Mac**

`cd /Applications/Factom/`

**Windows**

`cd C:\Program Files (x86)\Factom\`

On Mac, Windows and Linux, run "factomd" first

`factomd`

Then browse to [http://localhost:8090](http://localhost:8090) to see the Node Visualizer for your local FF node.

![node 01](images/wallet_018.png)

<aside class="notice"><br>
If this is the first time you are running FF, now's a great time to check your Facebook feed or take your dog on a walk. 
Syncing the Factom blockchain may take a little while, the blockchain is ...big. The Node Visualizer will display the progress and notify you when it has finished syncing.
</aside>

Once you are synced, in a new Terminal window browse (cd) to the location of your FF installation as you did above (Mac and Windows only).

<aside class="warning"><br>
There are two options now, one for people who have run Factom Genesis (FG), our previous software release, and one for people who haven't. The former have to import their old FG wallet file, the latter don't, choose the next step accordingly.
</aside>

**If you have previously used Factom Genesis (FG)**, you need to import your FG wallet file (named *factoid_wallet_bolt.db*) the first time your run *EnterpriseWallet* to make sure all its previous addresses and balances are transferred over. You have learned how to backup your wallet file in our [Backup Your Wallet File!](#backup-your-wallets) guide and you should know if still in the default location within the .factom folder at ~/.factom/factoid_wallet_bolt.db.

If your old wallet file is in the default place you don't need to do anything, the new wallet will recognize the file and import it automatically. You can simply follow the same instructions for who has never used FG below. 

If your wallet file is not in the default location then you need to tell EnterpriseWallet where to find it so simply run the next command with a special flag and the path to your wallet file: 

EnterpriseWallet -v1path=PATH_TO_factoid_wallet_bolt.db.

For example, if located on your desktop, run:

`EnterpriseWallet -v1path=~/Desktop/factoid_wallet_bolt.db`
 
This command will tell EnterpriseWallet to look for the file at the specified path and import all its addresses into the new wallet. The file can be located in a different location on your hard drive, just make sure to specify the path properly.

If by any chance the operation fails, quit EnterpriseWallet, delete the new wallet file located at ~/.factom/wallet/factoid_wallet.db and try again until you get all your addresses back.

<aside class="success"><br>
Remember, you only need to do this once the first time you run EnterpriseWallet, thereafter you can run it normally. 
</aside>

Once you are happy continue by following the instructions to run the the wallet in your browser.

**If you have never used FG**, on Mac, Windows and Linux, run the EnterpriseWallet app:

`EnterpriseWallet` 

> This is what the Terminal output will look like:

```shell
Reading from '/Home/.factom/factomd.conf'
Cannot open custom config file,
Starting with default settings.
open /Home/.factom/factomd.conf: no such file or directory

--------- Initiating GUIWallet ----------
Reading from '/Home/.factom/factomd.conf'
Cannot open custom config file,
Starting with default settings.
open /Home/.factom/factomd.conf: no such file or directory

Starting wallet waspi on localhost:8089
Wallet DB using Bolt, GUI DB using Bolt, TX DB using Bolt
Database started from: /Home/.factom/wallet/factom_wallet_gui.db
Database started from: /Home/.factom/wallet/factom_wallet.db
Database started from: /Home/.factom/wallet/factoid_blocks.cache
Starting Wallet WSAPI on http://localhostlocalhost:8089/
2016/12/14 02:43:26 web.go serving :8089
Starting GUI on http://localhostlocalhost:8091/
Step 1/3 for Transactions 0 / 125334
Step 1/3 for Transactions 10000 / 125334
Step 1/3 for Transactions 20000 / 125334
Step 1/3 for Transactions 30000 / 125334
Step 1/3 for Transactions 40000 / 125334
Step 1/3 for Transactions 50000 / 125334
Step 1/3 for Transactions 60000 / 125334
Step 1/3 for Transactions 70000 / 125334
Step 1/3 for Transactions 80000 / 125334
Step 1/3 for Transactions 90000 / 125334
Step 1/3 for Transactions 100000 / 125334
Step 1/3 for Transactions 110000 / 125334
Step 1/3 for Transactions 120000 / 125334
Step 1/3 for Transactions 125334 / 125334
Step 2/3 for Transactions 10000 / 122410
Step 2/3 for Transactions 20000 / 122410
Step 2/3 for Transactions 30000 / 122410
Step 2/3 for Transactions 40000 / 122410
Step 2/3 for Transactions 50000 / 122410
Step 2/3 for Transactions 60000 / 122410
Step 2/3 for Transactions 70000 / 122410
Step 2/3 for Transactions 80000 / 122410
Step 2/3 for Transactions 90000 / 122410
Step 2/3 for Transactions 100000 / 122410
Step 2/3 for Transactions 110000 / 122410
Step 2/3 for Transactions 120000 / 122410
Step 2/3 for Transactions 122410 / 122410
Step 3/3 for Transactions 0 / 122410
Step 3/3 for Transactions 10000 / 122410
Step 3/3 for Transactions 20000 / 122410
Step 3/3 for Transactions 30000 / 122410
Step 3/3 for Transactions 40000 / 122410
Step 3/3 for Transactions 50000 / 122410
Step 3/3 for Transactions 60000 / 122410
Step 3/3 for Transactions 70000 / 122410
Step 3/3 for Transactions 80000 / 122410
Step 3/3 for Transactions 90000 / 122410
Step 3/3 for Transactions 100000 / 122410
Step 3/3 for Transactions 110000 / 122410
Step 3/3 for Transactions 120000 / 122410
Step 3/3 for Transactions 122410 / 122410
Finishing up sync....
```
Sample Terminal output is shown on the right.

<br>
Then with your web browser go to [http://localhwst:8091](http://localhwst:8091) to see your local Factom Foundation Wallet.
<aside class="notice"><br>
If this is the first time you are running the Wallet, now's a great time for a cup of tea! 
The wallet needs to catch up on transactions and may take some time while displaying "syncing transactions", however it doesn't take too long, just about the time to prepare and drink your tea.
</aside>

Once the wallet has synced all transactions it should look like below.

![Wallet 01](images/wallet_019.png)

The first thing you may want to do is change the wallet theme, for the purpose of this guide we will use the Dark Theme going forward.
Click on "Settings" on the bottom left and select "Enable dark theme", then hit "SAVE CHANGES".

![Wallet 02](images/wallet_020.png)

Here's how it will look like in dark.

![Wallet 03](images/wallet_021.png)

Pat yourself on the back for making it this far! You have now "Run FF Wallet for the first time and you managed to change its default theme.

<aside class="success"><br>
There are other advanced features shown on the settings page and we will tell you more about them as we go along with our guides, for the time being we will use the wallet with default settings.
</aside>




