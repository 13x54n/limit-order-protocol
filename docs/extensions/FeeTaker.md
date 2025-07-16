
## FeeTaker

### Functions list
- [constructor(limitOrderProtocol, accessToken, weth, owner) public](#constructor)
- [receive() external](#receive)
- [postInteraction(order, extension, orderHash, taker, makingAmount, takingAmount, remainingMakingAmount, extraData) external](#postinteraction)
- [rescueFunds(token, amount) external](#rescuefunds)
- [_postInteraction(order, extension, orderHash, taker, makingAmount, takingAmount, remainingMakingAmount, extraData) internal](#_postinteraction)
- [_getFeeAmounts(, taker, takingAmount, , extraData) internal](#_getfeeamounts)
- [_isWhitelistedPostInteractionImpl(whitelistData, taker) internal](#_iswhitelistedpostinteractionimpl)

### Errors list
- [OnlyLimitOrderProtocol() ](#onlylimitorderprotocol)
- [OnlyWhitelistOrAccessToken() ](#onlywhitelistoraccesstoken)
- [EthTransferFailed() ](#ethtransferfailed)
- [InconsistentFee() ](#inconsistentfee)

### Functions
### constructor

```solidity
constructor(address limitOrderProtocol, contract IERC20 accessToken, address weth, address owner) public
```
Initializes the contract.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| limitOrderProtocol | address | The limit order protocol contract. |
| accessToken | contract IERC20 | Contract address whose tokens allow filling limit orders with a fee for resolvers that are outside the whitelist. |
| weth | address | The WETH address. |
| owner | address | The owner of the contract. |

### receive

```solidity
receive() external payable
```
Fallback function to receive ETH.

### postInteraction

```solidity
function postInteraction(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 makingAmount, uint256 takingAmount, uint256 remainingMakingAmount, bytes extraData) external
```
See {IPostInteraction-postInteraction}.

### rescueFunds

```solidity
function rescueFunds(contract IERC20 token, uint256 amount) external
```
Retrieves funds accidentally sent directly to the contract address

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| token | contract IERC20 | ERC20 token to retrieve |
| amount | uint256 | amount to retrieve |

### _postInteraction

```solidity
function _postInteraction(struct IOrderMixin.Order order, bytes extension, bytes32 orderHash, address taker, uint256 makingAmount, uint256 takingAmount, uint256 remainingMakingAmount, bytes extraData) internal virtual
```
See {IPostInteraction-postInteraction}.

_Takes the fee in taking tokens and transfers the rest to the maker.
`extraData` consists of:
1 byte - flags
20 bytes — integrator fee recipient
20 bytes - protocol fee recipient
20 bytes — receiver of taking tokens (optional, if not set, maker is used)
bytes - fees structure determined by `_getFeeAmounts` implementation
bytes — custom data to call extra postInteraction (optional)_

### _getFeeAmounts

```solidity
function _getFeeAmounts(struct IOrderMixin.Order, address taker, uint256 takingAmount, uint256, bytes extraData) internal virtual returns (uint256 integratorFeeAmount, uint256 protocolFeeAmount, bytes tail)
```

_Calculates fee amounts depending on whether the taker is in the whitelist and whether they have an _ACCESS_TOKEN.
`extraData` consists of:
2 bytes — integrator fee percentage (in 1e5)
1 bytes - integrator rev share percentage (in 1e2)
2 bytes — resolver fee percentage (in 1e5)
bytes — whitelist structure determined by `_isWhitelistedPostInteractionImpl` implementation
Override this function if the calculation of integratorFee and protocolFee differs from the existing logic and requires a different parsing of extraData._

### _isWhitelistedPostInteractionImpl

```solidity
function _isWhitelistedPostInteractionImpl(bytes whitelistData, address taker) internal view virtual returns (bool isWhitelisted, bytes tail)
```

_Parses fee data from `extraData`.
Override this function if whitelist structure in postInteraction is different from getters._

### Errors
### OnlyLimitOrderProtocol

```solidity
error OnlyLimitOrderProtocol()
```

_The caller is not the limit order protocol contract._

### OnlyWhitelistOrAccessToken

```solidity
error OnlyWhitelistOrAccessToken()
```

_The taker is not whitelisted and does not have access token._

### EthTransferFailed

```solidity
error EthTransferFailed()
```

_Eth transfer failed. The target fallback may have reverted._

### InconsistentFee

```solidity
error InconsistentFee()
```

_Fees are specified but FeeTaker is not set as a receiver._

