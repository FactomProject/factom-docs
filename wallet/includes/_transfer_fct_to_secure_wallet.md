## Transfer FCT To Secure Wallet

### Create Backup of Your Current Wallet

First of all, make sure to [Backup Your Wallets!](#backup-your-wallets)

<aside class="warning"><br>
Important: This backup should be copied to a safe location.
</aside>

### Upgrade Factom Enterprise Wallet

Then upgrade Enterprise Wallet to the latest version by following our [Install Enterprise Wallet guide](#install-enterprise-wallet).

### Create Secure Wallet & FCT Address

**1.** [Run Enterprise Wallet](#run-enterprise-wallet).

**2.** On the first screen, choose the “Secure” option.

![Online Wallet 00](images/wallet_140.png)

**3.** Enter a strong password and write it down – if you forget it and cannot recover it, you will lose access to the factoids that are stored in your Secure Wallet. Tick the checkbox to acknowledge this, and then click “Proceed To Encrypted Wallet” to automatically generate a new "factom_wallet_encrypted.db" file in your .factom folder (which will be encrypted with the password you just chose).

![Online Wallet 00](images/wallet_142.png)

**4.** From the Enterprise Wallet application, you can now [create a new factoid address](#create-a-factoid-address).

**5.** Copy the address you generated in the previous step so that you can fund it with factoids later in the process. You may want to save this in a separate text document for future reference (and to make it easy to copy and paste later on).

**6.** Once you are sure you have a backup of your wallet data, exit the application, and make sure that it is no longer running.

### Create Backup of Your Secure Wallet

Now it's time to backup your newly created secure wallet (encrypted) by following the [Backup Your Wallets!](#backup-your-wallets) guide.

<aside class="warning"><br>
Important: This backup should be copied to a safe location, and should be clearly distinguished from the first backup you made (in other words, make sure that you can keep the Secure and Not Secure backups safe).
</aside>

### Send FCT to Your Secure Wallet

**1.** Once again, run [Enterprise Wallet](#run-enterprise-wallet).

**2.** On the first screen, choose the “Not Secure” option.

![Online Wallet 00](images/wallet_141.png)

On the second screen tick the checkbox and click the "Proceed to Unencrypted Wallet" button.

![Online Wallet 00](images/wallet_144.png)

**3.** When the wallet has fully loaded, you should see your original factoid balances again. You can now send your factoids to the new Secure Wallet address you just generated by following the [Send and Receive FCT Guide](#send-and-receive-fct).

<aside class="warning"><br>
Important: Double-check the address you are funding before sending the transaction.
</aside>

**4.** Once you have sent your factoids from the Not Secure wallet addresses to the new, Secure wallet address(es) and waited for the transaction(s) to confirm, exit the application once again and make sure that it is no longer running.

### The End
If you have followed the above steps, when you next [Run Enterprise Wallet](#run-enterprise-wallet) and select the "Secure" option using the password you chose earlier, your balances will include the factoids that you sent to it, and your wallet will be securely encrypted.

<aside class="notice"><br>
Users who hold Entry Credits in a Not Secure wallet (unencrypted) can also import them into a Secure Wallet (encrypted) by simply <a href="#import-private-key">importing the private keys</a> of their EC Addresses.
</aside>