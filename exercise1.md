### Purpose
Send and receive money!

### Method

At this point, doing:

```
eth.getBalance(eth.accounts[0])
```
should show a huge amount of Ether!

Now create another account:

    d


    eth.sendTransaction({from:eth.accounts[0], to:"<the recipient>", value:100000000000000000});

You will end up with a transaction ID, e.g. 0xb983404b383361f27c1016eb7adcd422b0540d8fabf73fec0d5e9181a4fbaa49
Put that into etherscan to check it has been "mined"

https://rinkeby.etherscan.io/tx/0xc4c50cbd4ef9926966db5b34f41aaee58e722f4d90724a56c212f0b14b3e7fc0

YOu will probably see a "Pending" state.
Eventually it will show with a "Block" number, which means it has been added to a block in the blockchain. It is now "mined"!

Once it is mined, check your balance

    eth.getBalance(eth.accounts[0])

You should see it go down by approx 0.1 Ether. Eventually you will receive 0.1 Ether. So when all is done you are back where you started, i.e. with 1 Ether. Or are you?

Your address ("wallet") is becoming like a bank statement or a ledger.It has all the inputs and outputs:

https://rinkeby.etherscan.io/address/0xc93e45fb3215cb60e5937ecb0c86bbc2af144dba
    
## Learning Points

Your address is like a wallet, which holds value.

It is also like a bank account, which keeps track of activity (money in and out) in a ledger

Your address and the transactions are public. Anyone can see what it has been doing

Transactions cost money: You are paying the "miners" to do the work of adding your transaction to the blockchain. 



