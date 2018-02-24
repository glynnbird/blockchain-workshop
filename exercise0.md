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

#### Now run geth in "dev" mode
```
geth --dev --rpc
```

Add your account id here so we can send you ether
https://docs.google.com/spreadsheets/d/1fW_NYpddcuL1QKFtrIyYDkHIYHIFjabMfMfGzG7co0o/edit?usp=sharing


#### Make a symlink to make sure the testnet works

```sh
cd ~/.ethereum
ln -s /tmp/geth.ipc geth.ipc
cd .. 
```

What this does is download a "light" copy of the blockchain, so you need to leave it running, i.e. do not turn off your computer or close this terminal window. 

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
Now check that you have an account

```
eth.accounts
```
You will see something like this

```
> eth.accounts
["0x1ee5ba087b20a4ee457e8a8baafd12b44fc6a2fe"]
```

Now see if your account has any money in it

```
eth.getBalance(eth.accounts[0])
```


