## Install Enterprise Wallet

Enterprise wallet has been updated to be installed as a Desktop Application for Windows, Mac, or Linux. The process of backing up your wallets remains the same, and the desktop app uses the same file locations as the binary version (factom-walletd).
This guide will go over the installation of the new Enterprise Wallet.

<aside class="warning"><br>
For people who have run Factom Genesis (FG), our previous software release, you may need to import an old wallet file in the new wallet. We strongly recommend to only install the wallet desktop app at this stage without running it until you get familiar with the next guide: Run Enterprise Wallet.  
</aside>

Here is a step by step guide on how to install Enterprise Wallet on Mac, Windows, and Linux.

**Step 1**  Download the installer for Mac, Windows, or Linux on [GitHub](https://github.com/FactomProject/distribution).

These are the file names for the different installers:

* **Mac:** *enterprise-wallet-setup.dmg*
* **Windows 64bit:** *enterprise-wallet-setup-amd64.exe*
* **Linux (Ubuntu/Debian) 64bit:** *enterprise-wallet-setup-amd64.deb*
* **Linux (Redhat/Centos):** *enterprise-wallet-linux.zip*

**Step 2**  Save it to your desktop or downloads folder on your local hard drive.

**Step 3**  Follow the instructions for your OS.

### Mac

Double click on the "enterprise-wallet-setup.dmg" file downloaded at Step 1, when prompted drag EnterpriseWallet.app into the Applications folder.

![Install Mac Wallet](/images/wallet_086.png)

The wallet will be installed at the following location:

/Applications/EnterpriseWallet.app

Double click the app to launch it or drag to your dock to create a shortcut.

You are ready to [Run Enterprise Wallet](#run-enterprise-wallet), however read the guide carefully before you run the app, especially if you have an old wallet file to import. 

### Windows

Double click on the "enterprise-wallet-setup-amd64.exe" file downloaded at Step 1 to run the wallet installer.

Wait until it loads up. 

![Install Windows Wallet](/images/wallet_087.png)

Then follow the prompts and click install. Let the intaller finish.

![Install Windows Wallet 2](/images/wallet_088.png)

The wallet will be installed at the following location:

C:\Users\YOUR_USERNAME\AppData\Local\Programs\enterprisewallet\EnterpriseWallet.exe

A shortcut will also be added to your desktop for easy launch.

You are ready to [Run Enterprise Wallet](#run-enterprise-wallet), however read the guide carefully before you run the app, especially if you have an old wallet file to import.

### Linux

**For Ubuntu/Debian**
 
Locate the "enterprise-wallet-setup-amd64.deb" file downloaded at Step 1 to run the wallet installer.

Open a terminal window and go to where the .deb is located, for example:

`cd ~/Downloads`

Install the .deb package with this command:

`sudo dpkg -i enterprise-wallet-setup-amd64.deb`

![Install Linux Wallet](/images/wallet_089.png)

You will be able to run the wallet by simply searching for it in the search bar.

![Install Linux Wallet 2](/images/wallet_090.png)

**For Redhat/Centos**

Locate the "enterprise-wallet-linux.zip" and unzip it into a folder of your choice. Then open a Terminal window and cd to the "linux-unpacked" folder, for example:

`cd ~/Desktop/linux-unpacked`

<aside class="notice"><br>
You location may be different and you can also change the folder name from "linux-unpacked" to "EnterpriseWallet" or something more meaningful to you.
</aside>

Then run the wallet by executing the "enterprisewallet" binary with the following command:

`enterprisewallet`

You are ready to [Run Enterprise Wallet](#run-enterprise-wallet), however read the guide carefully before you run the app, especially if you have an old wallet file to import.
