# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
1. The manufacturer records product creation details on-chain.

2. The product moves through different supply chain checkpoints.

3. The ownership of the product can be transferred securely.

4. Buyers can verify the product’s authenticity.


# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
A luxury good (e.g., a Rolex watch) is registered on-chain.

Ownership is transferred at every checkpoint.

Buyers can check the authenticity before purchasing.

![bb3-1](https://github.com/user-attachments/assets/1a7174bd-33ef-4afe-803f-bf707ca18495)
![bb3-2](https://github.com/user-attachments/assets/8cc0b7de-fb29-4890-9680-37c76f58cdac)
![bb3-3](https://github.com/user-attachments/assets/759742ba-2466-40e8-8e4f-dc91b3986701)


# High-Level Overview:
Helps prevent counterfeit luxury goods.
Teaches real-world supply chain use cases.

# RESULT : 
Thus to develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity is implemented successfully.
