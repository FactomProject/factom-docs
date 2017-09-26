## Install Factom Federation (FF)

If you got this far, you are doing well Grasshopper. Ready to get your hands on FF? You will be up and running in a few minutes. Promise.

Here is a step by step guide on how to install FF binaries on Mac, Windows, and Linux.

**Step 1**  Download the installer for Mac, Windows, or Linux on [GitHub](https://github.com/FactomProject/distribution). There are various versions, make sure to select the one best suited for your system.

**Step 2**  Save it to your desktop or downloads folder on your local hard drive.

**Step 3**  Follow the instructions for your OS.

### Mac

This installer is for factomd, factom-walletd, factom-cli, the three binaries will be installed in /Applications/Factom/ together with a .factom folder in the root of the local user Home Folder. These are all required to run Factom via command line.

Before you start, go to System Preferences/Security & Privacy, click on the lock at the bottom left of the window, type your username and password, then select "Allow apps downloaded from: Anywhere." At the prompt click on “Allow From Anywhere.”

![Security & Privacy](/images/wallet_005.png)

Note that after running the Factom installer it is recommended you revert your Security & Privacy settings to their original state.

Next, locate the "factom.mpkg.zip" file you just downloaded, double-click to unzip it, then double-click the "factom.mpkg" file to run the installer.

The installer will open, click continue. 

![Installer Step 1](/images/wallet_006.png)

Then click install.

![Installer Step 2](/images/wallet_007.png)

The installer will prompt for your username and password. You need to have Admin privileges on the Mac (means you need to be able to install applications on your Mac).

Enter your username and password then click Install Software.

![Installer Step 3](/images/wallet_008.png)

The installer will proceed with the installation and once finished it will prompt with "The installation was successful." Then click close.

![Installer Step 4](/images/wallet_009.png)

You made it so far! Wasn't that hard, was it?

You are now ready to [install Enterprise Wallet](#install-enterprise-wallet). 

### Windows
This installer is for factomd, factom-walletd, factom-cli, the three binaries will be installed in c:\Program Files (x86)\Factom\ or c:\Program Files\Factom\ (depending on your system) together with a .factom folder in the root of the local user Home Folder. These are all required to run Factom via command line.

Next, locate the "FactomInstall-amd64.msi" or "FactomInstall-i386.msi" file you just downloaded in Step 1.

Double click the .msi installer to run it, but you may be prompted with the following message.

![Windows Prompt 1](/images/wallet_010.png)

Click on "more info" to expand it then select "Run anyway."

![Windows Prompt 2](/images/wallet_011.png)

The Installer will open, click "Next."

![Installer Step 1](/images/wallet_012.png)

Select "I accept the terms in the License Agreement" and click "Next" to continue.

![Installer Step 2](/images/wallet_013.png)

Make sure Factom is installed into c:\Program Files (x86)\Factom\ folder and click "Next" to continue.

![Installer Step 3](/images/wallet_014.png)

Then click "Install."

![Installer Step 4](/images/wallet_015.png)

Select "Yes" to continue if you get the following message.

![Windows Prompt 3](/images/wallet_016.png)

When the installation is over select "Finish" to exit the installer.

![Installer Step 5](/images/wallet_017.png)

You made it so far, and ready to [install Enterprise Wallet](#install-enterprise-wallet). 

### Linux
This installer is for factomd, factom-walletd, factom-cli, the three binaries will be installed on your local drive together with a .factom folder in the root of the local user Home Folder ~/.factom. These are all required to run Factom via command line or the Factom Foundation Wallet.

Download the "factom-amd64.deb" or "factom-i386.deb" installer that suits your system as per Step 1 then run the following command to install.

`sudo dpkg -i ./factom-amd64.deb`

or

`sudo dpkg -i ./factom-i386.deb`

We are aware Linux users are hardcore, so we made sure one command is all they need to be ready to [install Enterprise Wallet](#install-enterprise-wallet)!

