## Purpose
To create a basic smart contract and follow the steps to deploy it to the Ethereum blockchain

## Method 

You should have a terminal window open running geth and another one with the geth console.

Open a third terminal window

Create a file called jar.sol

    nano jar.sol

Paste this code in

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
Save (CTRL+O) and exit (CTRL+X)

Compile the code using solc

    solc --abi --bin jar.sol;

This will output two things: an long list of numbers and letters (the code binary) and an array (the code abi definition. This is the method "signature" of the contract.. more on this later).

At this point go **back to the geth console** and do

    var abi = <abi from solc>;
    var jarContract = eth.contract(abi); 
    var bin = '0x' + "<bytecode from solc>";
    var txDeploy = {from:eth.accounts[0], data: bin, gas: 1000000}; 
    
Broadcast your intention to create a new smart contract from the compiled source

    var jar = jarContract.new(txDeploy); 
    
Check the value of jar by typing :

```
jar
```
...  you should have an "address" and some functions

```js
{
	abi: [{
		constant: false,
		inputs: [],
		name: "withdraw",
		outputs: [],
		payable: false,
		type: "function"
	}, {
		constant: false,
		inputs: [],
		name: "save",
		outputs: [],
		payable: true,
		type: "function"
	}, {
		inputs: [],
		payable: false,
		type: "constructor"
	}],
	address: "0x0ef7cde2c00b0d0c52192e0be6a3a06773fdd833",
	transactionHash: "0x774a93c883cff95fb8728861130e4624f0cd4950797e75efc1d16b4d7cf10b73",
	allEvents: function(),
	save: function(),
	withdraw: function()
}

```
Again, in your private blockchain this happens immediately. In a real blockchain, this is another transaction and will take a bit of time to get processed. But eventually you will get your "address" value and you know it has been added to the blockchain.

The "address" is the location of your savings jar on the blockchain. 

Now, to put 0.05 ETHER into your savings jar, call the save function

    jar.save({from:eth.accounts[0], value:"50000000000000000"});
    
You will end up with a transaction ID, e.g. 0xb983404b383361f27c1016eb7adcd422b0540d8fabf73fec0d5e9181a4fbaa49

#### Addresses and "wallets" are the same thing

The jar "address" (jar.address) behaves in exactly the same way as one of the wallets you created previously. So you can do:

    eth.getBalance(jar.address)

...and you will see the 50000000000000000 Wei you put into it!

Now call the withdraw function

    jar.withdraw({from:eth.accounts[0]});

And the jar should be empty... look in the address. The money has gone back to to eth.accounts[0] 

## Learning Points

A smart contract deployed to the Blockchain has an address (its location) and an "abi definition" (the list of things -variables and functions- that you can interact with.)

With those two pieces of information, anyone can interact with any contract.

