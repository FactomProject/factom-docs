# Compile Factom Federation

Quick-start guide to compile and run Factom Federation software.

**Requirements not covered in guide**

GoLang (golang 1.7.4 recommended)

**Requirements**

Glide Package Manager

**Getting Glide**

Automatic install method:

`curl https://glide.sh/get | sh`

Manual installation can be found here: [https://glide.sh/](https://glide.sh/)

<aside class="warning"><br>
BEFORE BUILDING FACTOMD!
Glide can use github to gather all dependencies, but there is a chance your local github repos could cause some errors. If glide runs into an issue downloading a dependency, try deleting that folder it complains about (90% of dependecies are in '$GOPATH/src/github.com/FactomProject/'), and run glide install again.
</aside>

**Compile factomd**

This will take some time and place the source code into your GOPATH:

`go get github.com/FactomProject/factomd`

Cd into factomd:

`cd $GOPATH/src/github.com/FactomProject/factomd`

<aside class="notice"><br>
By default, the master branch will be selected. If you wish to build a different branch, change it now.
</aside>

Use glide to install all the dependencies:

`glide install`

Now install factomd, go install will place the binary in $GOPATH/bin:

`go install -v`

If you wish the binary to be built in the active directory:

`go build -v`

**Run factomd**

If compiled with 'go install':

`factomd`

If compiled with 'go build':

`cd $GOPATH/src/github.com/FactomProject/factomd`

Then run: 

`./factomd`

Open a web browser and go to [http://localhost:8090](http://localhost:8090) to see your factomd's status.

**Compile factom-cli**

Get the repo:

`go get github.com/FactomProject/factom-cli`

Cd into factom-cli:

`cd $GOPATH/src/github.com/FactomProject/factom-cli`

<aside class="notice"><br>
By default, the master branch will be selected. If you wish to build a different branch, change it now.
</aside>

Use glide to install all the dependencies:

`glide install`

Now install factom-cli, go install will place the binary in $GOPATH/bin:

`go install -v`

If you wish the binary to be built in the active directory:

`go build -v`

**Compile factom-walletd**

Get the repo:

`go get github.com/FactomProject/factom-walletd`

Cd into factom-walletd:

`cd $GOPATH/src/github.com/FactomProject/factom-walletd`

<aside class="notice"><br>
By default, the master branch will be selected. If you wish to build a different branch, change it now.
</aside>

Use glide to install all the dependencies:

`glide install`

Now install factom-walletd, go install will place the binary in $GOPATH/bin:

`go install -v`

If you wish the binary to be built in the active directory:

`go build -v`