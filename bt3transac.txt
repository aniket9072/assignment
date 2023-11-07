// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Bank {
    // Define the structure for a customer account
    struct Customer {
        uint accountNumber;
        uint balance;
    }
    
    // Array to store customer accounts
    Customer[] public customers;
    
    // Function to create a new customer account
    function createCustomer(uint _accountNumber, uint _initialBalance) public {
        Customer memory newCustomer = Customer({
            accountNumber: _accountNumber,
            balance: _initialBalance
        });
        customers.push(newCustomer);
    }
    
    // Function to deposit money into a customer's account
    function deposit(uint _accountNumber, uint _amount) public {
        for (uint i = 0; i < customers.length; i++) {
            if (customers[i].accountNumber == _accountNumber) {
                customers[i].balance += _amount;
                return;
            }
        }
        revert("Customer not found");
    }
    
    // Function to withdraw money from a customer's account
    function withdraw(uint _accountNumber, uint _amount) public {
        for (uint i = 0; i < customers.length; i++) {
            if (customers[i].accountNumber == _accountNumber) {
                require(customers[i].balance >= _amount, "Insufficient balance");
                customers[i].balance -= _amount;
                return;
            }
        }
        revert("Customer not found");
    }
    
    // Function to check the balance of a customer's account
    function getBalance(uint _accountNumber) public view returns (uint) {
        for (uint i = 0; i < customers.length; i++) {
            if (customers[i].accountNumber == _accountNumber) {
                return customers[i].balance;
            }
        }
        revert("Customer not found");
    }
}