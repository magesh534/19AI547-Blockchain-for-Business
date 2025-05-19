# Experiment 6: Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography)
# Aim:
To implement a secure passwordless authentication system using public-private key cryptography on Ethereum. This prevents phishing and password leaks.

# Algorithm:
Step 1: User Registration
A user registers with their Ethereum public key (instead of a password).


Step 2: Login Process
When logging in, the user signs a random challenge message using their private key.


The smart contract verifies the signature using the user’s public key.



# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PasswordlessAuth {
    mapping(address => bool) public registeredUsers;

    event UserRegistered(address user);
    event UserAuthenticated(address user);

    function registerUser() public {
        require(!registeredUsers[msg.sender], "Already registered");
        registeredUsers[msg.sender] = true;
        emit UserRegistered(msg.sender);
    }

    function authenticate(bytes32 hash, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        require(registeredUsers[msg.sender], "User not registered");
        address signer = ecrecover(hash, v, r, s);
        return signer == msg.sender;
    }
}
```

# Expected Output:
Users can register without a password.

Users sign a challenge with their private key for authentication.

The smart contract verifies signatures to confirm identity.

# High-Level Overview:
Eliminates password hacks & phishing attacks.

Uses Ethereum's built-in cryptographic functions.

Inspired by Web3 login solutions like MetaMask authentication.

# RESULT: 

![exp 6(i)](https://github.com/user-attachments/assets/23041661-3d7d-462e-8427-03254fde25d8)

![exp6(ii)](https://github.com/user-attachments/assets/9d7786c7-2762-485e-bb71-ae18d0cdefef)

![exp6(iii)](https://github.com/user-attachments/assets/2e2032a8-b75c-43ed-a9d9-9d8df22a74b7)

![exp6(iv)](https://github.com/user-attachments/assets/f78ddd13-e4bc-4b9e-a949-0d89e43b72c2)
