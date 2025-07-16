
## AmountGetterBase

### Functions list
- [getMakingAmount(order, extension, orderHash, taker, takingAmount, remainingMakingAmount, extraData) external](#getmakingamount)
- [getTakingAmount(order, extension, orderHash, taker, makingAmount, remainingMakingAmount, extraData) external](#gettakingamount)
- [_getMakingAmount(order, extension, orderHash, taker, takingAmount, remainingMakingAmount, extraData) internal](#_getmakingamount)
- [_getTakingAmount(order, extension, orderHash, taker, makingAmount, remainingMakingAmount, extraData) internal](#_gettakingamount)

### Functions
### getMakingAmount

```solidity
function getMakingAmount(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 takingAmount, uint256 remainingMakingAmount, bytes extraData) external view returns (uint256)
```
See {IAmountGetter-getMakingAmount}.

### getTakingAmount

```solidity
function getTakingAmount(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 makingAmount, uint256 remainingMakingAmount, bytes extraData) external view returns (uint256)
```
See {IAmountGetter-getTakingAmount}.

### _getMakingAmount

```solidity
function _getMakingAmount(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 takingAmount, uint256 remainingMakingAmount, bytes extraData) internal view virtual returns (uint256)
```

### _getTakingAmount

```solidity
function _getTakingAmount(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 makingAmount, uint256 remainingMakingAmount, bytes extraData) internal view virtual returns (uint256)
```

