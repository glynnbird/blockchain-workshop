### Purpose
To set up your environment

### Method

#### Install "geth"

```
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum-unstable
```

#### Install "solc" (compiler)

```
sudo apt-get install solc
```

#### Create an account (and tell us about it)
```
geth --rinkeby account new
<enter password>
```

Add your account id here so we can send you ether
https://docs.google.com/spreadsheets/d/1fW_NYpddcuL1QKFtrIyYDkHIYHIFjabMfMfGzG7co0o/edit?usp=sharing


#### Make a symlink to make sure the testnet works

```sh
cd ~/.ethereum
ln -s rinkeby/geth.ipc geth.ipc
cd .. 
```

#### Make a pass_file with the password of your account
```sh
echo "<password>" > pass_file
```

#### Run geth in the background

```sh
geth --rinkeby --rpc --unlock "0x<your_account>" --password pass_file
```

What this does is download a "light" copy of the blockchain, so you need to leave it running, i.e. do not turn off your computer or close this terminal window. 

It will take about an hour to sync the whole blockchain.

#### Attach to the geth instance that you are running

Open another terminal window and in it type:

```sh
geth attach
```

You should see something like this:

```
Welcome to the Geth JavaScript console! instance: 
Geth/v1.5.8-unstable-682875ad/linux/go1.7.3 modules: admin:1.0 debug:1.0 eth:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0 
>
```
Now check that your geth instance is synicing with the blockchain

```
eth.syncing
```
You will see something like this

```
{
  currentBlock: 1756268,
  highestBlock: 1765271,
  knownStates: 0,
  pulledStates: 0,
  startingBlock: 1756116
}
```

When eth.syncing returns "false", you are synced!

Now check that your account is there
```
eth.accounts[0]
```

Now see if your account has any money in it

```
eth.getBalance(eth.accounts[0])
```

We are going to send you some money, so keep checking until you have one Ether, i.e. 1000000000000000000 Wei

You can see a conversion of your Wei into Ether by doing:

```
web3.fromWei(eth.getBalance(eth.accounts[0]))
```
