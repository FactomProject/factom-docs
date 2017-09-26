## Before You Begin

Before attempting to transact factoids (FCT) read these guides thoroughly (at least once). 
The software is still in Beta, so use the instructions at your risk. Do not use a lot of Factoids in case there are issues, bugs, or you mistype a command. 
Phoning a friend after the damage is done will not fix things. Sorry, this is just the way of the Blockchain. 

The following directions and commands are optimized for Linux but should work with minor modifications for Mac or Windows. Be aware of slight differences in commands on different platforms:

**Mac**

`./factomd < rest of the command >`

**Windows**

`factomd < rest of the command >`

**Linux**

`factomd < rest of the command >`

Make sure to change the commands accordingly.

The interface you will be using to run Factom Federation software related commands is called:

* "Terminal" on the Mac and Linux
* "CMD Prompt" or "Windows Power Shell" on Windows

Give it a try and get familiar before you go any further. Going forward we will use "Terminal" to describe the interface where you type commands, just don't forget it has a different name in Windows.

FF is composed of three main components:

* factomd 
* factom-walletd 
* factom-cli 

However, to run the wallet you only need the new desktop app (Enterprise Wallet) if used online or the app + factomd if running locally, factom-walletd and factom-cli are only required if you want to run the command line wallet.

<aside class="notice"><br>
<i>Pop quiz</i><br>
How many windows will you need?<br>
Answer: Either Desktop App only or Desktop App + One Terminal window (factomd).
</aside>

<aside class="warning"><br>
<i>What your tech-savvy mother would say?</i><br>
Do not run Factom Federation while connected to an unsafe network, like at a cafe, an airport, public wifi hotspot, etc. The wallet is not encrypted, and hackers could potentially steal your precious Factoids. You do not want to feel like Gollum without his ring.<br>
</aside>

### Starting Factom Via Bootstrap

Factom takes a while to download the blockchain. You can expedite this by downloading the first 70k blocks via HTTP. Factomd still checks the blockchain on each boot; if there are any inconsistencies in the download, factomd will find them.

<aside class="notice"><br>
Note: currently factomd uses a lot of drive accesses when running. It is recommended to hold the blockchain on a solid state drive. Running factomd on a spinning hard drive will be arduously slow. Since factomd currently scans the entire blockchain each time it is started, bootup takes a while (~30 min on an SSD). You can watch the progress on the Control Panel.
</aside>

Download the blockchain [here](https://www.factom.com/assets/site/factom_bootstrap.zip). 

Extract the zip file to your home directory. It will create files in the location: 

~/.factom/m2/main-database/ldb/MAIN/factoid_level.db/

<aside class="success"><br>
The newly created .factom folder is an invisible folder on Mac and Linux so you won't be able to see it unless you browse to it via Terminal. On Mac, in Finder, you can also use Go/Go to Folder... and type ~/.factom to see its content. 
</aside>

Compressed, the blockchain is currently about 5 GB and uncompressed it is over 9 GB at the time of writing.

<aside class="warning"><br>
After factomd boots for the first time and is 100% synced, it will need to be restarted at least once. Successive restarts should be fine without having to restart.
</aside>