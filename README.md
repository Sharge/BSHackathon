#Welcome to the Banc Sabadell Blockchain Hackathon

This is your team's base repository for the BS Hackathon, please clone it and upload all code and project resources here.

##Our Ethereum network

In order to ease development during the event we've configured a private Ethereum network, this network is shared by all the teams and composed of several Linux virtual machines, each running a dedicated Ethereum node ([`geth`](https://github.com/ethereum/go-ethereum/wiki/geth)). Each team has access to its own unique VM:

![Network](images/network.png)

To get a better idea of the network and its behavior you can have a look at the different network stats using our monitoring [tool](http://admin-hackathon.westeurope.cloudapp.azure.com:3000/):

![Network](images/monitor.png)

###Access to your Ethereum node

Connecting to your `geth` instance through **JSON-RPC**:

* host: `hackathon-team5.centralus.cloudapp.azure.com`
* port: `8545`

In case your project depends on additional software (e.g. Node) you have full access to the machine via **SSH**:

* host: `hackathon-team5.centralus.cloudapp.azure.com`
* user: `team`
* password: `gb0o5nu3u6qD`

##BSToken contract

![BSToken](images/bstoken.png)

BSToken is a [digital token](https://www.ethereum.org/token) created exclusively by Banc Sabadell for this hackathon, you can integrate your Ethereum contracts with this token to create a variety of applications based on _tradable goods_ (E.g. [debt](https://forum.ethereum.org/discussion/2989/decentralized-system-for-securitizing-collateral-debt-obligations-using-the-ethereum-blockchain), [watts](http://www.coindesk.com/ethereum-used-first-paid-energy-trade-using-blockchain-technology/), etc. See [bs-scrow](https://github.com/BancoSabadell/bs-escrow) below for an example).

BSToken is implemented with a set of Solidity contracts that follow the [ERC20](https://github.com/ethereum/EIPs/issues/20) token specification:

```
// Abstract contract for the full ERC 20 Token standard
// https://github.com/ethereum/EIPs/issues/20
pragma solidity ^0.4.6;

contract Token {
    function totalSupply() constant returns (uint256);
    function balanceOf(address _owner) constant returns (uint256 balance);
    function transfer(address _to, uint256 _value) returns (bool success);
    function transferFrom(address _from, address _to, uint256 _value) returns (bool success);
    function approve(address _spender, uint256 _value) returns (bool success);
    function allowance(address _owner, address _spender) constant returns (uint256 remaining);

    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}
```

<details>
<summary>And its corresponding ABI (click to expand)</summary>
```javascript
[
	{
		"constant": false,
		"inputs": [
			{
				"name": "spender",
				"type": "address"
			},
			{
				"name": "value",
				"type": "uint256"
			}
		],
		"name": "approve",
		"outputs": [
			{
				"name": "success",
				"type": "bool"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [

		],
		"name": "startEmergency",
		"outputs": [

		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [

		],
		"name": "totalSupply",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "from",
				"type": "address"
			},
			{
				"name": "to",
				"type": "address"
			},
			{
				"name": "value",
				"type": "uint256"
			}
		],
		"name": "transferFrom",
		"outputs": [
			{
				"name": "success",
				"type": "bool"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [

		],
		"name": "bsToken",
		"outputs": [
			{
				"name": "",
				"type": "address"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "account",
				"type": "address"
			}
		],
		"name": "balanceOf",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [

		],
		"name": "stopEmergency",
		"outputs": [

		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [

		],
		"name": "merchant",
		"outputs": [
			{
				"name": "",
				"type": "address"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "to",
				"type": "address"
			},
			{
				"name": "value",
				"type": "uint256"
			}
		],
		"name": "transfer",
		"outputs": [
			{
				"name": "success",
				"type": "bool"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "account",
				"type": "address"
			}
		],
		"name": "frozenAccount",
		"outputs": [
			{
				"name": "",
				"type": "bool"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "spender",
				"type": "address"
			},
			{
				"name": "to",
				"type": "address"
			},
			{
				"name": "id",
				"type": "string"
			},
			{
				"name": "value",
				"type": "uint256"
			}
		],
		"name": "approveAndCall",
		"outputs": [

		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [

		],
		"name": "emergency",
		"outputs": [
			{
				"name": "",
				"type": "bool"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "version",
				"type": "address"
			}
		],
		"name": "setBSToken",
		"outputs": [

		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "account",
				"type": "address"
			},
			{
				"name": "spender",
				"type": "address"
			}
		],
		"name": "allowance",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "target",
				"type": "address"
			},
			{
				"name": "freeze",
				"type": "bool"
			}
		],
		"name": "freezeAccount",
		"outputs": [

		],
		"payable": false,
		"type": "function"
	},
	{
		"inputs": [
			{
				"name": "theMerchant",
				"type": "address"
			},
			{
				"name": "permissionManagerAddress",
				"type": "address"
			}
		],
		"payable": false,
		"type": "constructor"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": true,
				"name": "receiver",
				"type": "address"
			},
			{
				"indexed": false,
				"name": "amount",
				"type": "uint256"
			},
			{
				"indexed": false,
				"name": "bankAccount",
				"type": "string"
			}
		],
		"name": "CashOut",
		"type": "event"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": true,
				"name": "_from",
				"type": "address"
			},
			{
				"indexed": true,
				"name": "_to",
				"type": "address"
			},
			{
				"indexed": false,
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "Transfer",
		"type": "event"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": true,
				"name": "_owner",
				"type": "address"
			},
			{
				"indexed": true,
				"name": "_spender",
				"type": "address"
			},
			{
				"indexed": false,
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "Approval",
		"type": "event"
	}
]
```
</details>

The full contract(s) source code can be found [here](https://github.com/BancoSabadell/bs-token), including an utility JavaScript library, you may consider using it, instead of using directly the contract instance. This abstraction layer provides (among other benefits) some internal checks which prevents executing transactions when they are going to be rejected, loosing that way ether for nothing.

###Contract address

The BS Token contract is deployed at address: **`0x4356cd7b6b8cea6e7915137dce47891c1b5a738e`**

###Accounts per team (with 1000 BST and 100 ETH balances)

account | password
---	 | ---
0xd29e2371572bc99ee819b05b55bc4bbbf0d13deb | xIjqc8Jv
0x90d3b2cb9a7b0841a9abd89e0cf4c461152b0b0c | HPBQcoSl
0xeef4e785266ab777b8abe8783d66bdefbe2ebbcb | mEneQ8UX
0x947f712efeec414d4eb448f494c1e4548e417e1a | BPiuJOYf
0x2f369af699c10ab0ad4a4f21030323146c508a71 | DaJObDFD

###Sample integration (Escrow contract)

* [bs-escrow: Escrow contract and JavaScript library](https://github.com/BancoSabadell/bs-escrow)
* [bs-escrow-android-sdk: Android SDK and sample App](https://github.com/BancoSabadell/bs-escrow-android-sdk)

###Add tokens to an account using a credit card (Banking API)

If you want to add more tokens to an account or plan to accept payments in exchange of tokens we provide a simple REST API to add tokens to an account using a (test) credit card.

![Redsys](images/redsys.png)

The API is located at: `http://admin-hackathon.westeurope.cloudapp.azure.com`, including de following endpoints:

**Add tokens to an account**

	GET /bs_banking/api/v1/cashIn
	
This call will return an HTML page that will inmediately redirect to the credit card payment form.

Parameters:

name | description
---	 | ---
account | Ethereum address
amount | token amount _(1 BST == 1/100 EUR)_

Example ([View in browser](http://admin-hackathon.westeurope.cloudapp.azure.com/bs_banking/api/v1/cashIn?amount=120&account=0x6c8f2a135f6ed072de4503bd7c4999a1a17f824b)):

	http://admin-hackathon.westeurope.cloudapp.azure.com/bs_banking/api/v1/cashIn?amount=120&account=0x6c8f2a135f6ed072de4503bd7c4999a1a17f824b

Test credit card:

* Number: `4548 8120 4940 0004`
* Expiry date: `12/20`
* Security code: `123`
* CIP: `123456`

##FAQ's
* **Must our project rely on the token contract?** No, we provide the token and escrow contracts as an starting point or a base for *inspiration*.

##Resources

* [contract-deployer](https://github.com/BancoSabadell/contract-deployer): An utility script to easily deploy contracts from source code.
* [gt-permission-manager](https://github.com/BancoSabadell/gt-permission-manager) A contract to manage relationships and permissions of other contracts.
* [gt-identity](https://github.com/BancoSabadell/gt-identity): An Identity contract to forward calls to other contracts. This contract allows you to have a unique identity in the Ethereum blockchain (ie. same address as msg.sender when executing other contracts) while using several addresses from different devices.
* [gt-attributes](https://github.com/BancoSabadell/gt-attributes): A contract to attach attributes to identities and validate them.
* Ethereum JavaScript [Library](https://github.com/ethereum/web3.js/) and [documentation](https://github.com/ethereum/wiki/wiki/JavaScript-API)
* [Solidity](http://solidity.readthedocs.io/en/develop/) Language Documentation
* [ERC20: Token standard](https://github.com/ethereum/EIPs/issues/20)

##Contact

Need help? Contact us at: [innodev@bancsabadell.com](mailto:innodev@bancsabadell.com)


