## Purpose

To add a savings "target". Until you get to it, you cannot withdraw the money.

## Method

After exercise 3, you should have code that looks like this:

```
pragma solidity ^0.4.0;

contract jar {
  
  uint public numDonations; 

  function jar() public {
    numDonations = 0;
  }

  function save() public payable {
    numDonations++ ;
  }

  function withdraw() public payable {
    assert(msg.sender.send(this.balance));
  }

}


```

Create a text file called jar3.sol with the above code.

Now, add another global variable called target (see Exercise 3 for hints)

Then, in the constructor, set that variable to 200000000000000000  (0.2 ether)

Now, your "withdraw" function has to check whether you have saved enough money:

```
  function withdraw () {
    assert(this.balance >= target);
    assert(msg.sender.send(this.balance);
  }
```
- **this.balance** is an internal variable that holds the amount of ether in the contract.  
- **target** is your local variable with the target
- **assert** indicates that the expression inside the brackets needs to be **TRUE**. If it isn't then an exception occurs, the programme stops executing.

Save your code and make sure it compiles

    solc -- abi --bin jar3.sol

Again, follow the steps in [Exercise 2](https://gist.github.com/danmermel/66c87ffb1b6174999762c45d5251ffdf) to get the new contract up on the blockchain.

Now, save 0.05 ether

    jar.save({from:eth.accounts[0], value:"50000000000000000"});

...make sure that is mined. You can do that by checking the number of donations.

...and then try to withdraw the money:

    jar.withdraw({from:eth.accounts[0]});

Check the tx id on Etherscan. It should have failed.  Because the amount saved is less than the target then an exception is thrown and the contract stops executing. 
As a side effect of this, the sender of the transaction loses all of the ether they sent to pay for the execution.

Now, save more money, e.g. 0.16 ether:

    jar.save({from:eth.accounts[0], value:"160000000000000000"});
    
After that has mined, you should be able to withdraw your savings!

## Learning Points

Contract will not work if you do not meet its terms. Your code, once mined, is fixed forever - if you make the target 2 ETH instead of 0.2 ETH, you cannot change that!  
New code = completely new contract  
Hacking attempts are not cost-free - every time you try to execute a contract function and it fails (e.g. calling "withdraw" before the target is reached), you lose all the Ether you sent in to pay for the transaction.
