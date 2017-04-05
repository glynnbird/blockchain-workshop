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
geth --testnet account new
<enter password>
```

Add your account id here so we can send you ether
https://docs.google.com/spreadsheets/d/1fW_NYpddcuL1QKFtrIyYDkHIYHIFjabMfMfGzG7co0o/edit?usp=sharing


#### Make a symlink to make sure the testnet works

```sh
cd ~/.ethereum
ln -s testnet/geth.ipc geth.ipc
cd .. 
```

#### Make a pass_file with the password of your account
```sh
echo "<password>" > pass_file
```

#### Run geth in the background

```sh
geth --testnet --fast --unlock "0x<your_account>" --password pass_file --bootnodes "enode://20c9ad97c081d63397d7b685a412227a40e23c8bdc6688c6f37e97cfbc22d2b4d1db1510d8f61e6a8866ad7f0e17c02b14182d37ea7c3c8b9c2683aeb6b733a1@52.169.14.227:30303,enode://6ce05930c72abc632c58e2e4324f7c7ea478cec0ed4fa2528982cf34483094e9cbc9216e7aa349691242576d552a2a56aaeae426c5303ded677ce455ba1acd9d@13.84.180.240:30303" 
```


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

This will take a few minutes to complete... wait until eth.syncing returns "false".

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
