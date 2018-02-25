### Purpose
Send and receive money!

### Method

At this point, doing:

```
eth.getBalance(eth.accounts[0])
```
should show a huge amount of Ether!

Now create another account:

    personal.newAccount()

give it a passphrase (and remember it! Write it down somewhere)

This account should have no money in it

    eth.getBalance(eth.accounts[1])

You can now send some money from one account to the other:

    eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value:100000000000000000});

You will end up with a transaction ID, e.g. 0xb983404b383361f27c1016eb7adcd422b0540d8fabf73fec0d5e9181a4fbaa49

In the real blockchain, this transaction would be broadcast to the network, where it would be picked up by the network paricipants (the miners), inserted into a block and "mined" as part of the block. This process could take a minute or more (depending on network traffic). You can see an example of a real transaction here:

https://rinkeby.etherscan.io/tx/0xc4c50cbd4ef9926966db5b34f41aaee58e722f4d90724a56c212f0b14b3e7fc0

Etherscan is a "Blockchain Explorer", which allows you to visualise what is going on inside the blockchain

In our case, the tx will be mined immediately so you should be able to see some value in your second wallet.

Check your balance!

    eth.getBalance(eth.accounts[0])

   
## Learning Points

Your address is like a wallet, which holds value.

It is also like a bank account, which keeps track of activity (money in and out) in a ledger.

You can see an example of one here: 

    https://rinkeby.etherscan.io/address/0xc93e45fb3215cb60e5937ecb0c86bbc2af144dba

Your address and the transactions are public. Anyone can see what it has been doing.

Transactions cost money: You are paying the "miners" to do the work of adding your transaction to the blockchain (see the "TxFee" column in the above link)



