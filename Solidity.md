##存钱罐合约
```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.28;

contract Bank {
    address public immutable owner;
    event Deposit(address account, uint256 amount);
    event Withdraw(uint256 amount);

    constructor(){
        owner = msg.sender;
    }

    receive() external payable {
        emit Deposit(msg.sender, msg.value);
    }

    function withdraw(uint256 amount) external {
        require(msg.sender == owner, "Only owner can withdraw");
        require(address(this).balance >= amount, "Insufficient balance");
        emit Withdraw(amount);
        selfdestruct(payable(msg.sender));
    }

}
```

