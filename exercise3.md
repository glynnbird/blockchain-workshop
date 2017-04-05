## Purpose 

To count the number of donations that have been made into the jar.

## Method

Create a text file called jar2.sol containing the code from the first example:

```
pragma solidity ^0.4.0;

contract jar {

  function jar() {
  }

  function save() payable {
  }

  function withdraw () {
     if (!msg.sender.send(this.balance)) throw;
  }
}
```

Declare a variable called numDonations at the top of the contract.

    uint public numDonations;
    
In the constructor (this is only done once), set it to 0

    numDonations = 0;

In the save function (every time someone sends money), increment the counter

    numDonations++;
    
Save your file

In your terminal (not the Geth console), make sure it still compiles

    solc jar2.sol

Any compilation errors will appear in your console. 
If compilation is successful, you should get nothing.

Now, in the Geth console you have to follow the steps in [Exercise 2](https://gist.github.com/danmermel/66c87ffb1b6174999762c45d5251ffdf) in order to create a new contract on the blockchain.

Use this tool http://www.textfixer.com/tools/remove-line-breaks.php to remove **line and paragraph breaks** from your code.

Remember to keep checking the value of jar until you can see an address, which indicates it has been mined.

Check that the number of donations is currently 0:

```
    jar.numDonations();
```

Now you should be able to run the contract again and save some money:

    jar.save({from:eth.accounts[0], value:"50000000000000000"});

You will end up with a transaction ID, e.g. 0xb983404b383361f27c1016eb7adcd422b0540d8fabf73fec0d5e9181a4fbaa49

Put that into etherscan to check it has been "mined"

https://testnet.etherscan.io/tx/0xd7041f44b65a1b8a98c5a3111106211420a78bafe449dae7f718a2a8c911a706

Once it has been mined, you can check the number of donations in your geth console:

    jar.numDonations();
    
    
## Learning Points

A contract can have member variables whose state is retained for ever in the blockchain. The value of these variables can be changed by your constructor function at contract creation, or by any of the other contract's functions.
