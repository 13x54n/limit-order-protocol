
## AmountGetterWithFee

### Functions list
- [_getMakingAmount(order, extension, orderHash, taker, takingAmount, remainingMakingAmount, extraData) internal](#_getmakingamount)
- [_getTakingAmount(order, extension, orderHash, taker, makingAmount, remainingMakingAmount, extraData) internal](#_gettakingamount)
- [_parseFeeData(extraData, taker, _isWhitelisted) internal](#_parsefeedata)
- [_isWhitelistedGetterImpl(whitelistData, taker) internal](#_iswhitelistedgetterimpl)

### Errors list
- [InvalidIntegratorShare() ](#invalidintegratorshare)
- [InvalidWhitelistDiscountNumerator() ](#invalidwhitelistdiscountnumerator)

### Functions
### _getMakingAmount

```solidity
function _getMakingAmount(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 takingAmount, uint256 remainingMakingAmount, bytes extraData) internal view virtual returns (uint256)
```

_Calculates makingAmount with fee._

### _getTakingAmount

```solidity
function _getTakingAmount(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 makingAmount, uint256 remainingMakingAmount, bytes extraData) internal view virtual returns (uint256)
```

_Calculates takingAmount with fee._

### _parseFeeData

```solidity
function _parseFeeData(bytes extraData, address taker, function (bytes,address) view returns (bool,bytes) _isWhitelisted) internal view returns (bool isWhitelisted, uint256 integratorFee, uint256 integratorShare, uint256 resolverFee, bytes tail)
```

_`extraData` consists of:
2 bytes — integrator fee percentage (in 1e5)
1 byte - integrator share percentage (in 1e2)
2 bytes — resolver fee percentage (in 1e5)
1 byte - whitelist discount numerator (in 1e2)
bytes — whitelist structure determined by `_isWhitelisted` implementation
bytes — custom data (optional)_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| extraData | bytes |  |
| taker | address |  |
| _isWhitelisted | function (bytes,address) view returns (bool,bytes) | internal function to parse and check whitelist |

### _isWhitelistedGetterImpl

```solidity
function _isWhitelistedGetterImpl(bytes whitelistData, address taker) internal pure returns (bool isWhitelisted, bytes tail)
```

_Validates whether the taker is whitelisted._

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| whitelistData | bytes | Whitelist data is a tightly packed struct of the following format: ``` 1 byte - size of the whitelist (bytes10)[N] whitelisted addresses; ``` Only 10 lowest bytes of the address are used for comparison. |
| taker | address | The taker address to check. |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
isWhitelisted | bool | Whether the taker is whitelisted. |
tail | bytes | Remaining calldata. |

### Errors
### InvalidIntegratorShare

```solidity
error InvalidIntegratorShare()
```

### InvalidWhitelistDiscountNumerator

```solidity
error InvalidWhitelistDiscountNumerator()
```

