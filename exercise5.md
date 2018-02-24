## Purpose

To add some security, so that only the contract creator can withdraw the money!

## Method 

At the end of Exercise 4 you should have this code:

```
pragma solidity ^0.4.0;

contract jar {
  
  uint public numDonations; 
  uint public target;

  function jar() public {
    numDonations = 0;
    target = 200000000000000000;
  }

  function save() public payable {
    numDonations++ ;
  }

  function withdraw() public payable {
    assert(this.balance >= target);
    assert(msg.sender.send(this.balance));
  }

}
```

Create a text file called jar4.sol with the above code.

We want to store the creator of the contract. This is done by the constructor. So below the target, we define a variable called "owner", which is of a special type called "address":

    address owner;
    
    
Note that this variable is not "public". We don't want anyone to be able to access it.

Now, in the constructor function, set that variable to be the originator of the contract. You do this by typing:

    owner = msg.sender;
    
Now, write code to check whether the person trying to withdraw funds is the same that originated the contract (it is very similar to the other assert statements).

Remember to make sure your code compiles.

Again, follow the steps in [Exercise 2](https://gist.github.com/danmermel/66c87ffb1b6174999762c45d5251ffdf) to get the new contract up on the blockchain.

You can't see this, but the contract was created by eth.accounts[0]

Now, save 0.21 ether

    jar.save({from:eth.accounts[0], value:"210000000000000000"});

So now you want to try to withdraw money **from another account!**

To do that, remember that you created a new account in exercise 1? It was called eth.accounts[1]

First, you will need to unlock the account (that is why you had to remember the passphrase!):

    personal.unlockAccount(eth.accounts[1])
    
Now, give it a bit of money to pay for the gas (hint: it is in exercise 1!)

Now try to reach into the jar from eth.accounts[1]

    jar.withdraw({from:eth.accounts[1]});

Check the balance of the jar. Did the withdrawal succeed?

## Learning Points

Once a contract is on the blockchain, ANYONE can access it if they know its location (address) and its method signature (abi). It is TOTALLY public. So you need to make very sure that you know what it is doing and make sure that your function calls have security in place to prevent unwanted access.
