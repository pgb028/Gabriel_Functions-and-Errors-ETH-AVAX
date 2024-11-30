# Gabriel_Functions-and-Errors-ETH-AVAX

This Solidity program focuses on error handling and the various functions utilized for it.

We will tackle 3 functions given on the project

This program consists of 3 functions for error handling in Solidity:

Require() - Used to validate inputs and conditions before executing further logic. If the condition is not met, the function stops execution and reverts any changes. This ensures that only valid data is processed (e.g., verifying that the artwork amount is greater than zero or that the caller is the owner).

Assert() - Used to check for conditions that should never fail under normal circumstances, ensuring internal invariants of the contract. If an assert statement fails, it typically indicates a critical bug. For example, assert() is used here to confirm that the artwork count remains logically consistent after addition or subtraction.

Revert() - Provides a way to handle specific error scenarios where execution must stop. It is useful for implementing custom error messages and halting the contract when specific conditions are met, such as the borrowing limit in the borrowArtworks function.

**Executing the program**

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., FuncErrorProject.sol). Copy and paste the following code into the file:


To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.4" (or another compatible version), and then click on the "Compile final-project.sol" button.

After compilation, the contract can be deployed by clicking the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "ErrorHandler" contract from the dropdown menu, and then click on the "Deploy" button.

Code:

// SPDX-License-Identifier: MIT
//Gabriel Paul Andre A.
pragma solidity ^0.8.0;

contract ArtGallery {
    address public owner;
    uint256 public artworkCount;

    constructor() {
        owner = msg.sender;   
        artworkCount = 0;      
    }

  
    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action");
        _;
    }

    function addArtwork(uint256 _artworkAmount) public onlyOwner {
        require(_artworkAmount > 0, "Amount must be greater than 0");
        artworkCount += _artworkAmount;

        assert(artworkCount >= _artworkAmount); 
    }

    function removeArtwork(uint256 _artworkAmount) public onlyOwner {
        require(_artworkAmount > 0, "Amount must be greater than 0");
        require(artworkCount >= _artworkAmount, "Not enough artworks to remove");

        artworkCount -= _artworkAmount;


        assert(artworkCount <= artworkCount + _artworkAmount);  
    }

    function getArtworkCount() public view returns (uint256) {
        return artworkCount;
    }

   
    function borrowArtworks(uint256 _borrowAmount) public onlyOwner {
        if (_borrowAmount > 100) {
            revert("Reached limit of borrowed artworks today.");  
        }

        artworkCount += _borrowAmount; 
    }
}

The ArtGallery contract is a simple yet functional Solidity program designed to manage an inventory of artworks. It incorporates three essential Solidity error-handling functions—require(), assert(), and revert()—to ensure robustness and maintain data integrity. The contract begins by assigning ownership to the deployer using the constructor. The onlyOwner modifier restricts sensitive operations to the contract owner, ensuring unauthorized users cannot manipulate the artwork inventory.

The addArtwork and removeArtwork functions are at the core of this contract. The require() function validates inputs, such as ensuring artwork amounts are positive and that there is enough inventory for removal. The assert() function provides additional safeguards to verify that critical invariants, like the updated artwork count, remain logically consistent. This two-tiered approach—require() for input validation and assert() for state integrity—makes the contract robust against potential misuse.

Additionally, the borrowArtworks function introduces an error-handling example using the revert() function. This explicitly halts execution if the borrowing limit exceeds 100 artworks, demonstrating its use in scenarios where input conditions require custom error messages. Together, these functions illustrate Solidity's comprehensive error-handling mechanisms, making this contract a great learning example for secure and efficient smart contract design.

# Authors

**Paul Andre A. Gabriel**
Email: paulandreandradagabriel@gmail.com
School Email: 201811412@fit.edu.ph

# License

This project is licensed under the MIT License - see the LICENSE.md file for details



