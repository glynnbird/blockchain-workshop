## Purpose

To create a basic smart contract and follow the steps to deploy it to the Ethereum blockchain

## Method 

From exercise 1, you should be in the geth console.

Create a variable containing source code without carriage returns

    var src = "pragma solidity ^0.4.0; contract jar { function jar() { } function save() payable { } function withdraw () { if (!msg.sender.send(this.balance)) throw; } } "

Compile the code using solc

    var srcCompiled = web3.eth.compile.solidity(src);

Create a variable that contains the "abi definition" from the compiled source (this is the method "signature" of the contract.. more on this later).

    var jarContract = web3.eth.contract(srcCompiled['<stdin>:jar'].info.abiDefinition);

Broadcast your intention to create a new smart contract from the compiled source

    var jar =jarContract.new( {from:web3.eth.accounts[0], data: srcCompiled['<stdin>:jar'].code, gas: 2000000});
    
Check the value of jar by typing :

```
jar
```
... when it is mined you should have an "address" and some functions

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
Now, to put 0.05 ETHER into your savings jar, call the save function

    jar.save({from:eth.accounts[0], value:"50000000000000000"});
    
You will end up with a transaction ID, e.g. 0xb983404b383361f27c1016eb7adcd422b0540d8fabf73fec0d5e9181a4fbaa49
Put that into etherscan to check it has been "mined"

https://testnet.etherscan.io/tx/0xd7041f44b65a1b8a98c5a3111106211420a78bafe449dae7f718a2a8c911a706

Check your balance. You should be 0.05 ETH (+a small fee) poorer!

Call the withdraw function

    jar.withdraw({from:eth.accounts[0]});

Again, check the tx on etherscan

Once it is mined, check your balance

    eth.getBalance(eth.accounts[0])

You should now be 0.05 ETH richer!

Remember, you can check the ledger of transactions from your address on Etherscan

https://testnet.etherscan.io/address/<your_address>

## Learning Points

A smart contract deployed to the Blockchain has an address (its location) and an "abi definition" (the list of things -variables and functions- that you can interact with.)
With those two pieces of information, anyone can interact with any contract.
