
## ETHOrders

### Types list
- [ETHOrder](#ethorder)

### Functions list
- [constructor(weth, limitOrderProtocol, accessToken) public](#constructor)
- [ethOrdersBatch(orderHashes) external](#ethordersbatch)
- [ethOrderDeposit(order, extension, maximumPremium, auctionDuration) external](#ethorderdeposit)
- [cancelOrder(makerTraits, orderHash) external](#cancelorder)
- [cancelOrderByResolver(makerTraits, orderHash) external](#cancelorderbyresolver)
- [isValidSignature(orderHash, signature) external](#isvalidsignature)
- [postInteraction(, , orderHash, , makingAmount, , , ) external](#postinteraction)

### Events list
- [ETHDeposited(orderHash, amount) ](#ethdeposited)
- [ETHOrderCancelled(orderHash, amount) ](#ethordercancelled)
- [ETHOrderCancelledByThirdParty(orderHash, amount, reward) ](#ethordercancelledbythirdparty)

### Errors list
- [AccessDenied() ](#accessdenied)
- [InvalidOrder() ](#invalidorder)
- [NotEnoughBalance() ](#notenoughbalance)
- [ExistingOrder() ](#existingorder)
- [OrderNotExpired() ](#ordernotexpired)
- [RewardIsTooBig() ](#rewardistoobig)
- [CancelOrderByResolverIsForbidden() ](#cancelorderbyresolverisforbidden)

### Types
### ETHOrder

ETH order struct.

```solidity
struct ETHOrder {
  address maker;
  uint96 balance;
  uint16 maximumPremium;
  uint32 auctionDuration;
}
```

### Functions
### constructor

```solidity
constructor(contract IWETH weth, address limitOrderProtocol, contract IERC20 accessToken) public
```

### ethOrdersBatch

```solidity
function ethOrdersBatch(bytes32[] orderHashes) external view returns (struct ETHOrders.ETHOrder[] ethOrders)
```

### ethOrderDeposit

```solidity
function ethOrderDeposit(struct IOrderMixin.Order order, bytes extension, uint16 maximumPremium, uint32 auctionDuration) external payable returns (bytes32 orderHash)
```

### cancelOrder

```solidity
function cancelOrder(MakerTraits makerTraits, bytes32 orderHash) external
```
Sets ordersMakersBalances to 0, refunds ETH and does standard order cancellation on Limit Order Protocol.

### cancelOrderByResolver

```solidity
function cancelOrderByResolver(MakerTraits makerTraits, bytes32 orderHash) external
```
Allows third-party to cancel an expired order and receive a reward.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| makerTraits | MakerTraits | The traits of the maker |
| orderHash | bytes32 | Hash of the order to cancel |

### isValidSignature

```solidity
function isValidSignature(bytes32 orderHash, bytes signature) external view returns (bytes4)
```
Checks if orderHash signature was signed with real order maker.

### postInteraction

```solidity
function postInteraction(struct IOrderMixin.Order, bytes, bytes32 orderHash, address, uint256 makingAmount, uint256, uint256, bytes) external
```
Callback method that gets called after all funds transfers.
Updates _ordersMakersBalances by makingAmount for order with orderHash.

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
|  | struct IOrderMixin.Order |  |
|  | bytes |  |
| orderHash | bytes32 | Hash of the order being processed |
|  | address |  |
| makingAmount | uint256 | Actual making amount |
|  | uint256 |  |
|  | uint256 |  |
|  | bytes |  |

### Events
### ETHDeposited

```solidity
event ETHDeposited(bytes32 orderHash, uint256 amount)
```

### ETHOrderCancelled

```solidity
event ETHOrderCancelled(bytes32 orderHash, uint256 amount)
```

### ETHOrderCancelledByThirdParty

```solidity
event ETHOrderCancelledByThirdParty(bytes32 orderHash, uint256 amount, uint256 reward)
```

### Errors
### AccessDenied

```solidity
error AccessDenied()
```

### InvalidOrder

```solidity
error InvalidOrder()
```

### NotEnoughBalance

```solidity
error NotEnoughBalance()
```

### ExistingOrder

```solidity
error ExistingOrder()
```

### OrderNotExpired

```solidity
error OrderNotExpired()
```

### RewardIsTooBig

```solidity
error RewardIsTooBig()
```

### CancelOrderByResolverIsForbidden

```solidity
error CancelOrderByResolverIsForbidden()
```

