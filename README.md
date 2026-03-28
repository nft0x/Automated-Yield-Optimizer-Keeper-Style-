# Automated-Yield-Optimizer-Keeper-Style-
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/access/Ownable.sol";

contract YieldOptimizer is Ownable {
    uint256 public lastOptimize;
    uint256 public interval = 6 hours;

    event Optimized(uint256 timestamp, uint256 yieldGained);

    constructor(address initialOwner) Ownable(initialOwner) {}

    function checkUpkeep(bytes calldata) external view returns (bool, bytes memory) {
        return (block.timestamp >= lastOptimize + interval, "");
    }

    function performUpkeep(bytes calldata) external {
        require(block.timestamp >= lastOptimize + interval, "Too soon");
        lastOptimize = block.timestamp;
        // Call harvest, rebalance, or compound logic here
        emit Optimized(block.timestamp, 100 ether); // demo
    }
}
