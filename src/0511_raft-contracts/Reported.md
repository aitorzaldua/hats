## [LOW-1] Floating Pragma Solidity Version and consistency

The version used is ^  indicates that any compiler version after the number, e.g 0.8.19 , can be used to compile the source code.
Even if it is the latest version today, it leaves room for it to be attacked in the future.

### Lines of Code:

https://github.com/aitorzaldua/hats/blob/main/src/0511_raft-contracts/Dependencies/AggregatorV3Interface.sol

`2: pragma solidity ^0.8.19;`

### Recomendation: Remove the symbol ^

`2: pragma solidity 0.8.19;`

## [GAS-1] Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier or require such as onlyOwner/onlyX is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. 

The extra opcodes avoided are CALLVALUE(2), DUP1(3), ISZERO(3), PUSH2(3), JUMPI(10), PUSH1(3), DUP1(3), REVERT(0), JUMPDEST(1), POP(2) which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost.

### Lines of Code:

Contract: https://github.com/aitorzaldua/hats/blob/main/src/0511_raft-contracts/FeeCollector.sol

`37: function setFeeRecipient(address newFeeRecipient) external onlyOwner {`


Contract: https://github.com/aitorzaldua/hats/blob/main/src/0511_raft-contracts/PositionManager.sol

`290: function setBorrowingSpread(uint256 newBorrowingSpread) external override onlyOwner {`

`298: function setRedemptionRebate(uint256 newRedemptionRebate) public override onlyOwner {`

`320: function addCollateralToken(IERC20 collateralToken, IPriceFeed priceFeed) public override onlyOwner {`

`351: onlyOwner`

`365: onlyOwner`

`374: function setRedemptionSpread(uint256 newRedemptionSpread) public override onlyOwner {`


Contract: https://github.com/aitorzaldua/hats/blob/main/src/0511_raft-contracts/PriceFeed.sol

`41: function setPrimaryOracle(IPriceOracle newPrimaryOracle) external override onlyOwner {`

`45: function setSecondaryOracle(IPriceOracle newSecondaryOracle) external override onlyOwner {`

`49: function setPriceDifferenceBetweenOracles(uint256 newPriceDifferenceBetweenOracles) external override onlyOwner {`

Contract: https://github.com/aitorzaldua/hats/blob/main/src/0511_raft-contracts/RToken.sol

`55: function setFlashMintFeePercentage(uint256 feePercentage) public override onlyOwner {`