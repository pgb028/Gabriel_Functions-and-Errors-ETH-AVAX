# Gabriel_Functions-and-Errors-ETH-AVAX

This Solidity program focuses on error handling and the various functions utilized for it.

We will tackle 3 functions given on the project

# Description

This program consists of 3 functions
 
**Require()** - 
**Assert()** - 
**Revert()** - 
# Getting Started

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



# Authors

**Paul Andre A. Gabriel**
Email: paulandreandradagabriel@gmail.com
School Email: 201811412@fit.edu.ph

# License

This project is licensed under the MIT License - see the LICENSE.md file for details



