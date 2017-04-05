## Purpose

To add some security, so that only the contract creator can withdraw the money!

## Method 

At the end of Exercise 4 you should have this code:

```
pragma solidity ^0.4.0;

contract jar {

  uint public numDonations;
  uint public target;

  function jar() {
    numDonations = 0;
    target = 200000000000000000;
  }

  function save() payable {
    numDonations++;
  }

  function withdraw () {
    if (this.balance < target) throw;
    if (!msg.sender.send(this.balance)) throw;
  }
}
```
Create a text file called jar4.sol with the above code.

We want to store the creator of the contract. This is done by the constructor. So below the target, we define a variable called "owner", which is of a special type called "address":

    address owner;
    
    
Note that this variable is not "public". We don't want anyone to be able to access it.

Now, in the constructor function, set that variable to be the originator of the contract. You do this by typing:

    owner = msg.sender;
    
Now, write code to check whether the person trying to withdraw funds is the same that originated the contract (it is very similar to the other if statements).

Remember to make sure your code compiles.

Again, follow the steps in [Exercise 2](https://gist.github.com/danmermel/66c87ffb1b6174999762c45d5251ffdf) to get the new contract up on the blockchain.

Now, save 0.21 ether

    jar.save({from:eth.accounts[0], value:"210000000000000000"});

So now you want to try to withdraw money **from someone else's account!**

To do that, you will need to know where the account is. So turn to someone near you, get them to type 

```
jar.address
```

into **their** console, and then give you **their** contract address.

Now you are going to "reach into" their jar by creating it on your machine!

    var otherjar = eth.contract(srcCompiled.jar.info.abiDefinition).at("<other_address>")
    
And now try withdrawing money from their jar:

    otherjar.withdraw({from:eth.accounts[0]});

Check the resulting transaction ID on etherscan. What is going on?

## Learning Points

Once a contract is on the blockchain, ANYONE can access it if they know its location (address) and its method signature (abiDefinition). It is TOTALLY public. So you need to make very sure that you know what it is doing and make sure that your function calls have security in place to prevent unwanted access.
