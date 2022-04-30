# Smart-contracts PrivateSale.sol Token.sol HolbornPool.sol

Summary
 - [reentrancy-eth](#reentrancy-eth) (1 results) (High)
 - [shadowing-state](#shadowing-state) (1 results) (High)
 - [suicidal](#suicidal) (1 results) (High)
 - [unchecked-transfer](#unchecked-transfer) (2 results) (High)
 - [locked-ether](#locked-ether) (1 results) (Medium)
 - [reentrancy-no-eth](#reentrancy-no-eth) (1 results) (Medium)
 - [empty-functions](#empty-functions) (2 results) (Medium)
 - [reentrancy-benign](#reentrancy-benign) (1 results) (Low)
 - [reentrancy-events](#reentrancy-events) (1 results) (Low)
 - [pragma](#pragma) (1 results) (Informational)
 - [solc-version](#solc-version) (11 results) (Informational)
 - [low-level-calls](#low-level-calls) (1 results) (Informational)
 - [naming-convention](#naming-convention) (7 results) (Informational)
 - [too-many-digits](#too-many-digits) (1 results) (Informational)
 - [unused-state](#unused-state) (2 results) (Informational)
 - [external-function](#external-function) (23 results) (Optimization)
## reentrancy-eth
Impact: High
Confidence: Medium
 - [ ] ID-0
Reentrancy in [PrivateSale.getRefund(uint256)](contracts/Private Sale.sol#L31-L43):
External calls:
- [(refunded) = msg.sender.call{value: quantity * TICKET}()](contracts/Private Sale.sol#L37)
State variables written after the call(s):
- [purchasedTickets[msg.sender] -= quantity](contracts/Private Sale.sol#L41)

contracts/Private Sale.sol#L31-L43


## shadowing-state
Impact: High
Confidence: High
 - [ ] ID-1
[Holborn._balances](contracts/MyToken.sol#L12) shadows:
- [ERC20._balances](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L36)

contracts/MyToken.sol#L12


## suicidal
Impact: High
Confidence: High
 - [ ] ID-2
[Holborn.EmergencyDestroy(address)](contracts/MyToken.sol#L30-L33) allows anyone to destruct the contract

contracts/MyToken.sol#L30-L33


## unchecked-transfer
Impact: High
Confidence: Medium
 - [ ] ID-3
[DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94) ignores return value by [HAL.transferFrom(_sender,address(this),_amount)](contracts/My Pool.sol#L87)

contracts/My Pool.sol#L82-L94


 - [ ] ID-4
[DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119) ignores return value by [HAL.transfer(_user,userBalance[_user])](contracts/My Pool.sol#L117)

contracts/My Pool.sol#L100-L119


## locked-ether
Impact: Medium
Confidence: High
 - [ ] ID-5
Contract locking ether found:
Contract [DefiPool](contracts/My Pool.sol#L20-L134) has payable functions:
- [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94)
- [DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119)
But does not have a function to withdraw the ether

contracts/My Pool.sol#L20-L134


## reentrancy-no-eth
Impact: Medium
Confidence: Medium
 - [ ] ID-6
Reentrancy in [DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119):
External calls:
- [HAL.transfer(_user,userBalance[_user])](contracts/My Pool.sol#L117)
State variables written after the call(s):
- [userBalance[_user] = userBalance[_user] - initialUserBalance](contracts/My Pool.sol#L118)

contracts/My Pool.sol#L100-L119


## empty-functions
Impact: Medium
Confidence: Medium
 - [ ] ID-7
[ERC20._afterTokenTransfer(address,address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L351-L355) contains an empty function body

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L351-L355


 - [ ] ID-8
[ERC20._beforeTokenTransfer(address,address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L331-L335) contains an empty function body

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L331-L335


## reentrancy-benign
Impact: Low
Confidence: Medium
 - [ ] ID-9
Reentrancy in [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94):
External calls:
- [HAL.transferFrom(_sender,address(this),_amount)](contracts/My Pool.sol#L87)
State variables written after the call(s):
- [depositStart[msg.sender] = depositStart[msg.sender] + block.timestamp](contracts/My Pool.sol#L91)
- [userBalance[_sender] = userBalance[_sender] + _amount](contracts/My Pool.sol#L89)

contracts/My Pool.sol#L82-L94


## reentrancy-events
Impact: Low
Confidence: Medium
 - [ ] ID-10
Reentrancy in [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94):
External calls:
- [HAL.transferFrom(_sender,address(this),_amount)](contracts/My Pool.sol#L87)
Event emitted after the call(s):
- [Deposit(msg.sender,msg.value,block.timestamp)](contracts/My Pool.sol#L93)

contracts/My Pool.sol#L82-L94


## pragma
Impact: Informational
Confidence: High
 - [ ] ID-11
Different versions of Solidity is used:
- Version used: ['^0.8.0', '^0.8.2']
- [^0.8.0](node_modules/@openzeppelin/contracts/access/Ownable.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/security/Pausable.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/utils/Context.sol#L4)
- [^0.8.2](contracts/My Pool.sol#L2)
- [^0.8.2](contracts/MyToken.sol#L2)
- [^0.8.2](contracts/Private Sale.sol#L2)

node_modules/@openzeppelin/contracts/access/Ownable.sol#L4


## solc-version
Impact: Informational
Confidence: High
 - [ ] ID-12
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/access/Ownable.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/access/Ownable.sol#L4


 - [ ] ID-13
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/security/Pausable.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/security/Pausable.sol#L4


 - [ ] ID-14
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L4


 - [ ] ID-15
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4


 - [ ] ID-16
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L4


 - [ ] ID-17
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#L4


 - [ ] ID-18
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/utils/Context.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/utils/Context.sol#L4


 - [ ] ID-19
Pragma version[^0.8.2](contracts/My Pool.sol#L2) allows old versions

contracts/My Pool.sol#L2


 - [ ] ID-20
Pragma version[^0.8.2](contracts/MyToken.sol#L2) allows old versions

contracts/MyToken.sol#L2


 - [ ] ID-21
Pragma version[^0.8.2](contracts/Private Sale.sol#L2) allows old versions

contracts/Private Sale.sol#L2


 - [ ] ID-22
solc-0.8.2 is not recommended for deployment

## low-level-calls
Impact: Informational
Confidence: High
 - [ ] ID-23
Low level call in [PrivateSale.getRefund(uint256)](contracts/Private Sale.sol#L31-L43):
- [(refunded) = msg.sender.call{value: quantity * TICKET}()](contracts/Private Sale.sol#L37)

contracts/Private Sale.sol#L31-L43


## naming-convention
Impact: Informational
Confidence: High
 - [ ] ID-24
Parameter [DefiPool.deposit(uint256,address)._amount](contracts/My Pool.sol#L82) is not in mixedCase

contracts/My Pool.sol#L82


 - [ ] ID-25
Parameter [DefiPool.deposit(uint256,address)._sender](contracts/My Pool.sol#L82) is not in mixedCase

contracts/My Pool.sol#L82


 - [ ] ID-26
Parameter [DefiPool.withdraw(address)._user](contracts/My Pool.sol#L100) is not in mixedCase

contracts/My Pool.sol#L100


 - [ ] ID-27
Function [DefiPool.EmergencyWithraw(address,address,uint256)](contracts/My Pool.sol#L131-L133) is not in mixedCase

contracts/My Pool.sol#L131-L133


 - [ ] ID-28
Variable [DefiPool.HAL](contracts/My Pool.sol#L44) is not in mixedCase

contracts/My Pool.sol#L44


 - [ ] ID-29
Function [Holborn.EmergencyDestroy(address)](contracts/MyToken.sol#L30-L33) is not in mixedCase

contracts/MyToken.sol#L30-L33


 - [ ] ID-30
Parameter [Holborn.EmergencyDestroy(address)._to](contracts/MyToken.sol#L30) is not in mixedCase

contracts/MyToken.sol#L30


## too-many-digits
Impact: Informational
Confidence: Medium
 - [ ] ID-31
[Holborn.constructor()](contracts/MyToken.sol#L13-L15) uses literals with too many digits:
- [_mint(msg.sender,10000000000 * 10 ** decimals())](contracts/MyToken.sol#L14)

contracts/MyToken.sol#L13-L15


## unused-state
Impact: Informational
Confidence: High
 - [ ] ID-32
[DefiPool.allowed](contracts/My Pool.sol#L27) is never used in [DefiPool](contracts/My Pool.sol#L20-L134)

contracts/My Pool.sol#L27


 - [ ] ID-33
[Holborn._balances](contracts/MyToken.sol#L12) is never used in [Holborn](contracts/MyToken.sol#L9-L34)

contracts/MyToken.sol#L12


## external-function
Impact: Optimization
Confidence: High
 - [ ] ID-34
renounceOwnership() should be declared external:
- [Ownable.renounceOwnership()](node_modules/@openzeppelin/contracts/access/Ownable.sol#L54-L56)

node_modules/@openzeppelin/contracts/access/Ownable.sol#L54-L56


 - [ ] ID-35
transferOwnership(address) should be declared external:
- [Ownable.transferOwnership(address)](node_modules/@openzeppelin/contracts/access/Ownable.sol#L62-L65)

node_modules/@openzeppelin/contracts/access/Ownable.sol#L62-L65


 - [ ] ID-36
name() should be declared external:
- [ERC20.name()](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L62-L64)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L62-L64


 - [ ] ID-37
symbol() should be declared external:
- [ERC20.symbol()](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L70-L72)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L70-L72


 - [ ] ID-38
totalSupply() should be declared external:
- [ERC20.totalSupply()](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L94-L96)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L94-L96


 - [ ] ID-39
balanceOf(address) should be declared external:
- [ERC20.balanceOf(address)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L101-L103)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L101-L103


 - [ ] ID-40
transfer(address,uint256) should be declared external:
- [ERC20.transfer(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L113-L116)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L113-L116


 - [ ] ID-41
approve(address,uint256) should be declared external:
- [ERC20.approve(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L132-L135)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L132-L135


 - [ ] ID-42
transferFrom(address,address,uint256) should be declared external:
- [ERC20.transferFrom(address,address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L150-L164)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L150-L164


 - [ ] ID-43
increaseAllowance(address,uint256) should be declared external:
- [ERC20.increaseAllowance(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L178-L181)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L178-L181


 - [ ] ID-44
decreaseAllowance(address,uint256) should be declared external:
- [ERC20.decreaseAllowance(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L197-L205)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L197-L205


 - [ ] ID-45
burn(uint256) should be declared external:
- [ERC20Burnable.burn(uint256)](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L20-L22)

node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L20-L22


 - [ ] ID-46
burnFrom(address,uint256) should be declared external:
- [ERC20Burnable.burnFrom(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L35-L42)

node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L35-L42


 - [ ] ID-47
transfer(address,uint256) should be declared external:
- [DefiPool.transfer(address,uint256)](contracts/My Pool.sol#L32-L37)

contracts/My Pool.sol#L32-L37


 - [ ] ID-48
deposit(uint256,address) should be declared external:
- [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94)

contracts/My Pool.sol#L82-L94


 - [ ] ID-49
withdraw(address) should be declared external:
- [DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119)

contracts/My Pool.sol#L100-L119


 - [ ] ID-50
getContractBalance() should be declared external:
- [DefiPool.getContractBalance()](contracts/My Pool.sol#L124-L129)

contracts/My Pool.sol#L124-L129


 - [ ] ID-51
EmergencyWithraw(address,address,uint256) should be declared external:
- [DefiPool.EmergencyWithraw(address,address,uint256)](contracts/My Pool.sol#L131-L133)

contracts/My Pool.sol#L131-L133


 - [ ] ID-52
pause() should be declared external:
- [Holborn.pause()](contracts/MyToken.sol#L16-L18)

contracts/MyToken.sol#L16-L18


 - [ ] ID-53
unpause() should be declared external:
- [Holborn.unpause()](contracts/MyToken.sol#L20-L22)

contracts/MyToken.sol#L20-L22


 - [ ] ID-54
mint(address,uint256) should be declared external:
- [Holborn.mint(address,uint256)](contracts/MyToken.sol#L24-L26)

contracts/MyToken.sol#L24-L26


 - [ ] ID-55
transferbyOwner(address,address,uint256) should be declared external:
- [Holborn.transferbyOwner(address,address,uint256)](contracts/MyToken.sol#L27-L29)

contracts/MyToken.sol#L27-L29


 - [ ] ID-56
EmergencyDestroy(address) should be declared external:
- [Holborn.EmergencyDestroy(address)](contracts/MyToken.sol#L30-L33)

contracts/MyToken.sol#L30-L33

Summary
 - [reentrancy-eth](#reentrancy-eth) (1 results) (High)
 - [shadowing-state](#shadowing-state) (1 results) (High)
 - [suicidal](#suicidal) (1 results) (High)
 - [unchecked-transfer](#unchecked-transfer) (2 results) (High)
 - [locked-ether](#locked-ether) (1 results) (Medium)
 - [reentrancy-no-eth](#reentrancy-no-eth) (1 results) (Medium)
 - [empty-functions](#empty-functions) (2 results) (Medium)
 - [reentrancy-benign](#reentrancy-benign) (1 results) (Low)
 - [reentrancy-events](#reentrancy-events) (1 results) (Low)
 - [pragma](#pragma) (1 results) (Informational)
 - [solc-version](#solc-version) (11 results) (Informational)
 - [low-level-calls](#low-level-calls) (1 results) (Informational)
 - [naming-convention](#naming-convention) (7 results) (Informational)
 - [too-many-digits](#too-many-digits) (1 results) (Informational)
 - [unused-state](#unused-state) (2 results) (Informational)
 - [external-function](#external-function) (23 results) (Optimization)
## reentrancy-eth
Impact: High
Confidence: Medium
 - [ ] ID-0
Reentrancy in [PrivateSale.getRefund(uint256)](contracts/Private Sale.sol#L31-L43):
External calls:
- [(refunded) = msg.sender.call{value: quantity * TICKET}()](contracts/Private Sale.sol#L37)
State variables written after the call(s):
- [purchasedTickets[msg.sender] -= quantity](contracts/Private Sale.sol#L41)

contracts/Private Sale.sol#L31-L43


## shadowing-state
Impact: High
Confidence: High
 - [ ] ID-1
[Holborn._balances](contracts/MyToken.sol#L12) shadows:
- [ERC20._balances](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L36)

contracts/MyToken.sol#L12


## suicidal
Impact: High
Confidence: High
 - [ ] ID-2
[Holborn.EmergencyDestroy(address)](contracts/MyToken.sol#L30-L33) allows anyone to destruct the contract

contracts/MyToken.sol#L30-L33


## unchecked-transfer
Impact: High
Confidence: Medium
 - [ ] ID-3
[DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94) ignores return value by [HAL.transferFrom(_sender,address(this),_amount)](contracts/My Pool.sol#L87)

contracts/My Pool.sol#L82-L94


 - [ ] ID-4
[DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119) ignores return value by [HAL.transfer(_user,userBalance[_user])](contracts/My Pool.sol#L117)

contracts/My Pool.sol#L100-L119


## locked-ether
Impact: Medium
Confidence: High
 - [ ] ID-5
Contract locking ether found:
Contract [DefiPool](contracts/My Pool.sol#L20-L134) has payable functions:
- [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94)
- [DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119)
But does not have a function to withdraw the ether

contracts/My Pool.sol#L20-L134


## reentrancy-no-eth
Impact: Medium
Confidence: Medium
 - [ ] ID-6
Reentrancy in [DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119):
External calls:
- [HAL.transfer(_user,userBalance[_user])](contracts/My Pool.sol#L117)
State variables written after the call(s):
- [userBalance[_user] = userBalance[_user] - initialUserBalance](contracts/My Pool.sol#L118)

contracts/My Pool.sol#L100-L119


## empty-functions
Impact: Medium
Confidence: Medium
 - [ ] ID-7
[ERC20._afterTokenTransfer(address,address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L351-L355) contains an empty function body

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L351-L355


 - [ ] ID-8
[ERC20._beforeTokenTransfer(address,address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L331-L335) contains an empty function body

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L331-L335


## reentrancy-benign
Impact: Low
Confidence: Medium
 - [ ] ID-9
Reentrancy in [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94):
External calls:
- [HAL.transferFrom(_sender,address(this),_amount)](contracts/My Pool.sol#L87)
State variables written after the call(s):
- [depositStart[msg.sender] = depositStart[msg.sender] + block.timestamp](contracts/My Pool.sol#L91)
- [userBalance[_sender] = userBalance[_sender] + _amount](contracts/My Pool.sol#L89)

contracts/My Pool.sol#L82-L94


## reentrancy-events
Impact: Low
Confidence: Medium
 - [ ] ID-10
Reentrancy in [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94):
External calls:
- [HAL.transferFrom(_sender,address(this),_amount)](contracts/My Pool.sol#L87)
Event emitted after the call(s):
- [Deposit(msg.sender,msg.value,block.timestamp)](contracts/My Pool.sol#L93)

contracts/My Pool.sol#L82-L94


## pragma
Impact: Informational
Confidence: High
 - [ ] ID-11
Different versions of Solidity is used:
- Version used: ['^0.8.0', '^0.8.2']
- [^0.8.0](node_modules/@openzeppelin/contracts/access/Ownable.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/security/Pausable.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#L4)
- [^0.8.0](node_modules/@openzeppelin/contracts/utils/Context.sol#L4)
- [^0.8.2](contracts/My Pool.sol#L2)
- [^0.8.2](contracts/MyToken.sol#L2)
- [^0.8.2](contracts/Private Sale.sol#L2)

node_modules/@openzeppelin/contracts/access/Ownable.sol#L4


## solc-version
Impact: Informational
Confidence: High
 - [ ] ID-12
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/access/Ownable.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/access/Ownable.sol#L4


 - [ ] ID-13
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/security/Pausable.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/security/Pausable.sol#L4


 - [ ] ID-14
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L4


 - [ ] ID-15
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4


 - [ ] ID-16
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L4


 - [ ] ID-17
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol#L4


 - [ ] ID-18
Pragma version[^0.8.0](node_modules/@openzeppelin/contracts/utils/Context.sol#L4) allows old versions

node_modules/@openzeppelin/contracts/utils/Context.sol#L4


 - [ ] ID-19
Pragma version[^0.8.2](contracts/My Pool.sol#L2) allows old versions

contracts/My Pool.sol#L2


 - [ ] ID-20
Pragma version[^0.8.2](contracts/MyToken.sol#L2) allows old versions

contracts/MyToken.sol#L2


 - [ ] ID-21
Pragma version[^0.8.2](contracts/Private Sale.sol#L2) allows old versions

contracts/Private Sale.sol#L2


 - [ ] ID-22
solc-0.8.2 is not recommended for deployment

## low-level-calls
Impact: Informational
Confidence: High
 - [ ] ID-23
Low level call in [PrivateSale.getRefund(uint256)](contracts/Private Sale.sol#L31-L43):
- [(refunded) = msg.sender.call{value: quantity * TICKET}()](contracts/Private Sale.sol#L37)

contracts/Private Sale.sol#L31-L43


## naming-convention
Impact: Informational
Confidence: High
 - [ ] ID-24
Parameter [DefiPool.deposit(uint256,address)._amount](contracts/My Pool.sol#L82) is not in mixedCase

contracts/My Pool.sol#L82


 - [ ] ID-25
Parameter [DefiPool.deposit(uint256,address)._sender](contracts/My Pool.sol#L82) is not in mixedCase

contracts/My Pool.sol#L82


 - [ ] ID-26
Parameter [DefiPool.withdraw(address)._user](contracts/My Pool.sol#L100) is not in mixedCase

contracts/My Pool.sol#L100


 - [ ] ID-27
Function [DefiPool.EmergencyWithraw(address,address,uint256)](contracts/My Pool.sol#L131-L133) is not in mixedCase

contracts/My Pool.sol#L131-L133


 - [ ] ID-28
Variable [DefiPool.HAL](contracts/My Pool.sol#L44) is not in mixedCase

contracts/My Pool.sol#L44


 - [ ] ID-29
Function [Holborn.EmergencyDestroy(address)](contracts/MyToken.sol#L30-L33) is not in mixedCase

contracts/MyToken.sol#L30-L33


 - [ ] ID-30
Parameter [Holborn.EmergencyDestroy(address)._to](contracts/MyToken.sol#L30) is not in mixedCase

contracts/MyToken.sol#L30


## too-many-digits
Impact: Informational
Confidence: Medium
 - [ ] ID-31
[Holborn.constructor()](contracts/MyToken.sol#L13-L15) uses literals with too many digits:
- [_mint(msg.sender,10000000000 * 10 ** decimals())](contracts/MyToken.sol#L14)

contracts/MyToken.sol#L13-L15


## unused-state
Impact: Informational
Confidence: High
 - [ ] ID-32
[DefiPool.allowed](contracts/My Pool.sol#L27) is never used in [DefiPool](contracts/My Pool.sol#L20-L134)

contracts/My Pool.sol#L27


 - [ ] ID-33
[Holborn._balances](contracts/MyToken.sol#L12) is never used in [Holborn](contracts/MyToken.sol#L9-L34)

contracts/MyToken.sol#L12


## external-function
Impact: Optimization
Confidence: High
 - [ ] ID-34
renounceOwnership() should be declared external:
- [Ownable.renounceOwnership()](node_modules/@openzeppelin/contracts/access/Ownable.sol#L54-L56)

node_modules/@openzeppelin/contracts/access/Ownable.sol#L54-L56


 - [ ] ID-35
transferOwnership(address) should be declared external:
- [Ownable.transferOwnership(address)](node_modules/@openzeppelin/contracts/access/Ownable.sol#L62-L65)

node_modules/@openzeppelin/contracts/access/Ownable.sol#L62-L65


 - [ ] ID-36
name() should be declared external:
- [ERC20.name()](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L62-L64)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L62-L64


 - [ ] ID-37
symbol() should be declared external:
- [ERC20.symbol()](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L70-L72)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L70-L72


 - [ ] ID-38
totalSupply() should be declared external:
- [ERC20.totalSupply()](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L94-L96)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L94-L96


 - [ ] ID-39
balanceOf(address) should be declared external:
- [ERC20.balanceOf(address)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L101-L103)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L101-L103


 - [ ] ID-40
transfer(address,uint256) should be declared external:
- [ERC20.transfer(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L113-L116)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L113-L116


 - [ ] ID-41
approve(address,uint256) should be declared external:
- [ERC20.approve(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L132-L135)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L132-L135


 - [ ] ID-42
transferFrom(address,address,uint256) should be declared external:
- [ERC20.transferFrom(address,address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L150-L164)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L150-L164


 - [ ] ID-43
increaseAllowance(address,uint256) should be declared external:
- [ERC20.increaseAllowance(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L178-L181)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L178-L181


 - [ ] ID-44
decreaseAllowance(address,uint256) should be declared external:
- [ERC20.decreaseAllowance(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L197-L205)

node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol#L197-L205


 - [ ] ID-45
burn(uint256) should be declared external:
- [ERC20Burnable.burn(uint256)](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L20-L22)

node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L20-L22


 - [ ] ID-46
burnFrom(address,uint256) should be declared external:
- [ERC20Burnable.burnFrom(address,uint256)](node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L35-L42)

node_modules/@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol#L35-L42


 - [ ] ID-47
transfer(address,uint256) should be declared external:
- [DefiPool.transfer(address,uint256)](contracts/My Pool.sol#L32-L37)

contracts/My Pool.sol#L32-L37


 - [ ] ID-48
deposit(uint256,address) should be declared external:
- [DefiPool.deposit(uint256,address)](contracts/My Pool.sol#L82-L94)

contracts/My Pool.sol#L82-L94


 - [ ] ID-49
withdraw(address) should be declared external:
- [DefiPool.withdraw(address)](contracts/My Pool.sol#L100-L119)

contracts/My Pool.sol#L100-L119


 - [ ] ID-50
getContractBalance() should be declared external:
- [DefiPool.getContractBalance()](contracts/My Pool.sol#L124-L129)

contracts/My Pool.sol#L124-L129


 - [ ] ID-51
EmergencyWithraw(address,address,uint256) should be declared external:
- [DefiPool.EmergencyWithraw(address,address,uint256)](contracts/My Pool.sol#L131-L133)

contracts/My Pool.sol#L131-L133


 - [ ] ID-52
pause() should be declared external:
- [Holborn.pause()](contracts/MyToken.sol#L16-L18)

contracts/MyToken.sol#L16-L18


 - [ ] ID-53
unpause() should be declared external:
- [Holborn.unpause()](contracts/MyToken.sol#L20-L22)

contracts/MyToken.sol#L20-L22


 - [ ] ID-54
mint(address,uint256) should be declared external:
- [Holborn.mint(address,uint256)](contracts/MyToken.sol#L24-L26)

contracts/MyToken.sol#L24-L26


 - [ ] ID-55
transferbyOwner(address,address,uint256) should be declared external:
- [Holborn.transferbyOwner(address,address,uint256)](contracts/MyToken.sol#L27-L29)

contracts/MyToken.sol#L27-L29


 - [ ] ID-56
EmergencyDestroy(address) should be declared external:
- [Holborn.EmergencyDestroy(address)](contracts/MyToken.sol#L30-L33)

contracts/MyToken.sol#L30-L33
