## Purpose 

To count the number of donations that have been made into the jar.

## Method

Create a text file called jar2.sol containing the code from the first example:

```
pragma solidity ^0.4.0;

contract jar {

  function jar() public { }

  function save() public payable { }

  function withdraw() public payable {
    assert(msg.sender.send(this.balance));
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

    solc --abi --bin jar2.sol

Any compilation errors will appear in your console. 
If compilation is successful, you should get only the abi and binary code like before.

Now, in the Geth console you have to follow the steps in [Exercise 2](https://gist.github.com/danmermel/66c87ffb1b6174999762c45d5251ffdf) in order to create a new contract on the blockchain.

Check that the number of donations is currently 0:

```
    jar.numDonations();
```

Now you should be able to run the contract again and save some money:

    jar.save({from:eth.accounts[0], value:"50000000000000000"});

Now check the number of donations in your geth console again.

    
## Learning Points

A contract can have member variables whose state is retained for ever in the blockchain. The value of these variables can be changed by your constructor function at contract creation, or by any of the other contract's functions.

If you declare a variable (or function) to be "public", it means it is accessible to anyone interacting with your contract.
