# CA-on-BASE-burning-token
Smart contract on BASE of a token that's amount can be burned

// SPDX-License-Identifier: MIT
// Generated with Spectral Syntax

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/AccessControl.sol";

contract MyToken is ERC20, AccessControl {
    bytes32 public constant MINT_ROLE = keccak256("MINT_ROLE");

    constructor() ERC20("MyToken", "MTK") {
        _setupRole(MINT_ROLE, msg.sender);
    }

    /**
     * @param _amount Amount of tokens to burn.
     */
    function burn(uint256 _amount) public onlyRole(MINT_ROLE) {
        _burn(_msgSender(), _amount);
    }

    /**
     * @dev Burns tokens from a specified address, assuming they have the required allowance.
     * Can only be called by an account with the MINT_ROLE.
     * @param _account Address to burn tokens from.
     * @param _amount Amount of tokens to burn.
     */
    function burn(address _account, uint256 _amount) public onlyRole(MINT_ROLE) {
        _spendAllowance(_account, _msgSender(), _amount);
        _burn(_account, _amount);
    }
}
