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

### Docker

If you've made it this far, you may not have an operating system. This will make it very difficult to run Factom Federation since, at this point, we do still require you to use a computing device. However, if you're simply looking for a way to get started in ANY environment, you've come to the right place.

Because we are a very modern organization, we've made arrangements for you to get started in a containerized environment. All you need is [Docker](https://www.docker.com/) at minimum v17 and a clone of the [factomd repo](https://github.com/FactomProject/factomd).

#### Build
From wherever you have cloned the factomd repo, run

`docker build -t factomd_container .`

(yes, you can replace **factomd_container** with whatever you want to call the container.  e.g. **factomd**, **foo**, etc.)

<aside class="notice"><br>
<strong>Cross-Compile</strong>
<br>
<p>To cross-compile for a different target, you can pass in a <code>build-arg</code> as so
<br><br>
<code>docker build -t factomd_container --build-arg GOOS=darwin .</code></p>
</aside>


#### Run

##### No Persistence
`docker run --rm -p 8090:8090 factomd_container`
  
* This will start up **factomd** with no flags.
* The Control Panel is accessible at port 8090  
* When the container terminates, all data will be lost

<aside class="notice">
In the above, replace <strong>factomd_container</strong> with whatever you called it when you built it - e.g. <strong>factomd</strong>, <strong>foo</strong>, etc.
</aside>

##### With Persistence
1. `docker volume create factomd_volume`
2. `docker run --rm -v $(PWD)/factomd.conf:/source -v factomd_volume:/destination busybox /bin/cp /source /destination/factomd.conf`
3. `docker run --rm -p 8090:8090 -v factomd_volume:/root/.factom/m2 factomd_container`

* This will start up **factomd** with no flags.
* The Control Panel is accessible at port 8090  
* When the container terminates, the data will remain persisted in the volume **factomd_volume**
* The above copies **factomd.conf** from the local directory into the container. Put _your_ version in there, or change the path appropriately.


<aside class="notice">
In the above
<ul>
    <li>replace <strong>factomd_container</strong> with whatever you called it when you built it - e.g. <strong>factomd</strong>, <strong>foo</strong>, etc.</li>
    <li>replace <strong>factomd_volume</strong> with whatever you might want to call it - e.g. <strong>myvolume</strong>, <strong>barbaz</strong>, etc.</li>
</ul>
</aside>

##### Additional Flags
In all cases, you can startup with additional flags by passing them at the end of the docker command, e.g.

`docker run --rm -p 8090:8090 factomd_container -port 9999`


#### Copy

```shell
docker run --rm --entrypoint='' \
    -v <FULLY_QUALIFIED_PATH_TO_TARGET_DIRECTORY>:/destination factomd_container \
    /bin/cp /go/bin/factomd /destination
```

>The following will copy the binary to `/tmp/factomd`

```shell
docker run --rm --entrypoint='' \
-v /tmp:/destination factomd_container \
/bin/cp /go/bin/factomd /destination
```


So yeah, you want to get your binary _out_ of the container. To do so, you basically mount your target into the container and copy the binary over as shown.


<aside class="notice">You should replace <strong>factomd_container</strong> with whatever you called it in the <a href="#build">build</a> section above  e.g. <strong>factomd</strong>, <strong>foo</strong>, etc.
</aside>








#### Cross-Compile Copy

>Cross-Compile copy

```shell
docker run --rm --entrypoint='' \
-v <FULLY_QUALIFIED_PATH_TO_TARGET_DIRECTORY>:/destination \
factomd_container \
/bin/cp /go/bin/darwin_amd64/factomd /destination
```

>To copy the darwin_amd64 version of the binary to `/tmp/factomd`...

```shell
docker run --rm --entrypoint='' 
-v /tmp:/destination factomd_container \
/bin/cp /go/bin/darwin_amd64/factomd /destination
``` 

If you cross-compiled to a different target, your binary will be in `/go/bin/<target>/factomd`.  e.g. If you built with `--build-arg GOOS=darwin`, then you can copy out the binary using the commands shown on the right.

<aside class="notice">You should replace <strong>factomd_container</strong> with whatever you called it in the <strong>build</strong> section above  e.g. <strong>factomd</strong>, <strong>foo</strong>, etc.
</aside>

