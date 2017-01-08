## Before We Begin

Before attempting to transact factoids (FCT) read these guides thoroughly (at least once). The software is still in beta, so use the instructions at your risk. Do not use a large number of Factoids in case there are issues, bugs, or you mistype a command. Phoning a friend after the damage is done will not fix things. Sorry, this is just the way of the Blockchain. If you are unsure how to use the command line, we suggest you try our Factom Foundation Wallet instead which is simpler to use and has a Graphic User Interface (GUI).

The following directions and commands are optimized for Linux but should work with minor modifications for Mac or Windows. Be aware of slight differences in commands on different platforms:

**Mac**

`./factom-cli < rest of the command >`

**Windows**

`factom-cli.exe < rest of the command >`

**Linux**

`factom-cli < rest of the command >`

Make sure to modify the commands accordingly.

The interface you will be using to run Factom Federation software related commands is called:

* "Terminal" on the Mac and Linux
* "CMD Prompt" or "Windows Power Shell" on Windows

Give it a try and get familiar before you go any further. Going forward we will use "Terminal" to describe the interface where you type commands, just don't forget it has a different name in Windows.

FF is composed of four main components:

* factomd
* factom-walletd
* factom-cli
* enterprise-wallet

However, to run Factom Federation via command line you only need factomd, factom-walletd, and factom-cli. Each one of these apps needs to run in separate Terminal windows.

<aside class="notice"><br>
Pop quiz<br>
How many windows will you need?<br>
Answer: Three Terminal windows.
</aside>

<aside class="warning"><br>
What your tech savvy mother would say?<br>
Do not run Factom Federation while connected to an unsafe network, like at a cafe, an airport, public wifi hotspot, etc. The wallet is not encrypted, and hackers could potentially steal your precious Factoids. You do not want to feel like Gollum without his ring. 
</aside>