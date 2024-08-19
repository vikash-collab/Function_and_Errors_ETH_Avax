# RequireAssertRevert Contract
Description
The RequireAssertRevert contract is a Solidity-based smart contract designed to manage a simple balance system. It includes mechanisms for depositing, withdrawing, and transferring funds, while enforcing certain conditions using require, assert, and revert. This contract serves as a practical example of error handling in Solidity, ensuring that operations are secure and valid.

## Getting Started
Prerequisites
To interact with this contract, you'll need:

## Access to Remix, an online Solidity IDE.
MetaMask or another Ethereum wallet to deploy the contract on an Ethereum testnet or local blockchain.
Executing the Program
Open Remix:

## Navigate to Remix.
Create a New File:

### Click the "+" icon in the left-hand sidebar.
Save the file with a .sol extension (e.g., RequireAssertRevert.sol).
Copy and Paste the Code:

solidity
Copy code
pragma solidity ^0.8.0;

contract RequireAssertRevert {
    address private owner;
    uint public balance;

    constructor() {
        owner = msg.sender;
        balance = 0;
    }

    function deposit(uint amount) public {
        require(msg.sender == owner, "Only the owner can deposit funds");
        require(amount > 0, "Deposit amount must be greater than 0");
        balance += amount;
    }

    function withdraw(uint amount) public {
        require(msg.sender == owner, "Only the owner can withdraw funds");
        require(amount > 0, "Withdrawal amount must be greater than 0");
        require(balance >= amount, "Insufficient balance");

        balance -= amount;
        assert(balance >= 0);
    }

    function transfer(address recipient, uint amount) public {
        require(msg.sender == owner, "Only the owner can transfer funds");
        require(amount > 0, "Transfer amount must be greater than 0");
        require(balance >= amount, "Insufficient balance");

        balance -= amount;
        (bool success, ) = recipient.call{value: amount}("");
        if (!success) {
            revert("Transfer failed");
        }
    }
}
## Compile the Contract:

In the "Solidity Compiler" tab, ensure the compiler version is set to 0.8.0 or another compatible version.
Click "Compile RequireAssertRevert.sol".
Deploy the Contract:

Go to the "Deploy & Run Transactions" tab.
Select RequireAssertRevert from the contract dropdown and click "Deploy".
Ensure you're deploying the contract from the intended account (the owner's account).
Interact with the Contract:

Once deployed, you can interact with the contract’s functions (deposit, withdraw, transfer) through the Remix interface.
Only the contract owner (the account that deployed the contract) can execute these functions.
## Authors
Vikash Singh
## License
This project is licensed under the MIT License - see the LICENSE.md file for details
