# Contract Reference

## IEuler

Main storage contract for the Euler system

### moduleIdToProxy

Lookup a proxy that can be used to interact with a module

```text
function moduleIdToProxy(uint moduleId) external view returns (address);
```

Parameters:

* **moduleId**: Fixed constant that refers to a module type \(ie MODULEID\_\_MARKETS\)

Returns:

* An address that should be cast to the appropriate module interface, ie IEulerMarkets\(moduleIdToProxy\(2\)\)

### AssetConfig

Euler-related configuration for an asset

```text
struct AssetConfig {
    address eTokenAddress;
    bool borrowIsolated;
    uint32 collateralFactor;
    uint32 borrowFactor;
    uint24 twapWindow;
}
```

## IEulerMarkets

Activating and querying markets, and maintaining entered markets lists

### activateMarket

Create an Euler pool and associated EToken and DToken addresses.

```text
function activateMarket(address underlying) external returns (address);
```

Parameters:

* **underlying**: The address of an ERC20-compliant token. There must be an initialised uniswap3 pool for the underlying/reference asset pair.

Returns:

* The created EToken, or the existing EToken if already activated.

### activatePToken

Create a pToken and activate it on Euler. pTokens are protected wrappers around assets that prevent borrowing.

```text
function activatePToken(address underlying) external returns (address);
```

Parameters:

* **underlying**: The address of an ERC20-compliant token. There must already be an activated market on Euler for this underlying, and it must have a non-zero collateral factor.

Returns:

* The created pToken, or an existing one if already activated.

### underlyingToEToken

Given an underlying, lookup the associated EToken

```text
function underlyingToEToken(address underlying) external view returns (address);
```

Parameters:

* **underlying**: Token address

Returns:

* EToken address, or address\(0\) if not activated

### underlyingToDToken

Given an underlying, lookup the associated DToken

```text
function underlyingToDToken(address underlying) external view returns (address);
```

Parameters:

* **underlying**: Token address

Returns:

* DToken address, or address\(0\) if not activated

### underlyingToPToken

Given an underlying, lookup the associated PToken

```text
function underlyingToPToken(address underlying) external view returns (address);
```

Parameters:

* **underlying**: Token address

Returns:

* PToken address, or address\(0\) if it doesn't exist

### underlyingToAssetConfig

Looks up the Euler-related configuration for a token, and resolves all default-value placeholders to their currently configured values.

```text
function underlyingToAssetConfig(address underlying) external view returns (IEuler.AssetConfig memory);
```

Parameters:

* **underlying**: Token address

Returns:

* Configuration struct

### underlyingToAssetConfigUnresolved

Looks up the Euler-related configuration for a token, and returns it unresolved \(with default-value placeholders\)

```text
function underlyingToAssetConfigUnresolved(address underlying) external view returns (IEuler.AssetConfig memory);
```

Parameters:

* **underlying**: Token address

Returns:

* Configuration struct

### eTokenToUnderlying

Given an EToken address, looks up the associated underlying

```text
function eTokenToUnderlying(address eToken) external view returns (address);
```

Parameters:

* **eToken**: EToken address

Returns:

* Token address

### eTokenToDToken

Given an EToken address, looks up the associated DToken

```text
function eTokenToDToken(address eToken) external view returns (address);
```

Parameters:

* **eToken**: EToken address

Returns:

* DToken address

### interestRateModel

Looks up an asset's currently configured interest rate model

```text
function interestRateModel(address underlying) external view returns (uint);
```

Parameters:

* **underlying**: Token address

Returns:

* Module ID that represents the interest rate model \(IRM\)

### interestRate

Retrieves the current interest rate for an asset

```text
function interestRate(address underlying) external view returns (int96);
```

Parameters:

* **underlying**: Token address

Returns:

* The interest rate in yield-per-second, scaled by 10\*\*27

### interestAccumulator

Retrieves the current interest rate accumulator for an asset

```text
function interestAccumulator(address underlying) external view returns (uint);
```

Parameters:

* **underlying**: Token address

Returns:

* An opaque accumulator that increases as interest is accrued

### reserveFee

Retrieves the reserve fee in effect for an asset

```text
function reserveFee(address underlying) external view returns (uint32);
```

Parameters:

* **underlying**: Token address

Returns:

* Amount of interest that is redirected to the reserves, as a fraction scaled by RESERVE\_FEE\_SCALE \(4e9\)

### getPricingConfig

Retrieves the pricing config for an asset

```text
function getPricingConfig(address underlying) external view returns (uint16 pricingType, uint32 pricingParameters, address pricingForwarded);
```

Parameters:

* **underlying**: Token address

Returns:

* **pricingType**: \(1=pegged, 2=uniswap3, 3=forwarded\)
* **pricingParameters**: If uniswap3 pricingType then this represents the uniswap pool fee used, otherwise unused
* **pricingForwarded**: If forwarded pricingType then this is the address prices are forwarded to, otherwise address\(0\)

### getEnteredMarkets

Retrieves the list of entered markets for an account \(assets enabled for collateral or borrowing\)

```text
function getEnteredMarkets(address account) external view returns (address[] memory);
```

Parameters:

* **account**: User account

Returns:

* List of underlying token addresses

### enterMarket

Add an asset to the entered market list, or do nothing if already entered

```text
function enterMarket(uint subAccountId, address newMarket) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **newMarket**: Underlying token address

### exitMarket

Remove an asset from the entered market list, or do nothing if not already present

```text
function exitMarket(uint subAccountId, address oldMarket) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **oldMarket**: Underlying token address

## IEulerExec

Batch executions, liquidity check deferrals, and interfaces to fetch prices and account liquidity

### LiquidityStatus

Liquidity status for an account, either in aggregate or for a particular asset

```text
struct LiquidityStatus {
    uint collateralValue;
    uint liabilityValue;
    uint numBorrows;
    bool borrowIsolated;
}
```

### AssetLiquidity

Aggregate struct for reporting detailed \(per-asset\) liquidity for an account

```text
struct AssetLiquidity {
    address underlying;
    LiquidityStatus status;
}
```

### EulerBatchItem

Single item in a batch request

```text
struct EulerBatchItem {
    bool allowError;
    address proxyAddr;
    bytes data;
}
```

### EulerBatchItemResponse

Single item in a batch response

```text
struct EulerBatchItemResponse {
    bool success;
    bytes result;
}
```

### liquidity

Compute aggregate liquidity for an account

```text
function liquidity(address account) external returns (LiquidityStatus memory status);
```

Parameters:

* **account**: User address

Returns:

* **status**: Aggregate liquidity \(sum of all entered assets\)

### detailedLiquidity

Compute detailed liquidity for an account, broken down by asset

```text
function detailedLiquidity(address account) external returns (AssetLiquidity[] memory assets);
```

Parameters:

* **account**: User address

Returns:

* **assets**: List of user's entered assets and each asset's corresponding liquidity

### getPrice

Retrieve Euler's view of an asset's price

```text
function getPrice(address underlying) external returns (uint twap, uint twapPeriod);
```

Parameters:

* **underlying**: Token address

Returns:

* **twap**: Time-weighted average price
* **twapPeriod**: TWAP duration, either the twapWindow value in AssetConfig, or less if that duration not available

### getPriceFull

Retrieve Euler's view of an asset's price, as well as the current marginal price on uniswap

```text
function getPriceFull(address underlying) external returns (uint twap, uint twapPeriod, uint currPrice);
```

Parameters:

* **underlying**: Token address

Returns:

* **twap**: Time-weighted average price
* **twapPeriod**: TWAP duration, either the twapWindow value in AssetConfig, or less if that duration not available
* **currPrice**: The current marginal price on uniswap3 \(informational: not used anywhere in the Euler protocol\)

### deferLiquidityCheck

Defer liquidity checking for an account, to perform rebalancing, flash loans, etc. msg.sender must implement IDeferredLiquidityCheck

```text
function deferLiquidityCheck(address account, bytes memory data) external;
```

Parameters:

* **account**: The account to defer liquidity for. Usually address\(this\), although not always
* **data**: Passed through to the onDeferredLiquidityCheck\(\) callback, so contracts don't need to store transient data in storage

### batchDispatch

Execute several operations in a single transaction

```text
function batchDispatch(EulerBatchItem[] calldata items, address[] calldata deferLiquidityChecks) external returns (EulerBatchItemResponse[] memory);
```

Parameters:

* **items**: List of operations to execute
* **deferLiquidityChecks**: List of user accounts to defer liquidity checks for

Returns:

* List of operation results

### EulerBatchExtra

Results of a batchDispatch, but with extra information

```text
struct EulerBatchExtra {
    EulerBatchItemResponse[] responses;
    uint gasUsed;
    AssetLiquidity[][] liquidities;
}
```

### batchDispatchExtra

Call batchDispatch, but return extra information. Only intended to be used with callStatic.

```text
function batchDispatchExtra(EulerBatchItem[] calldata items, address[] calldata deferLiquidityChecks, address[] calldata queryLiquidity) external returns (EulerBatchExtra memory output);
```

Parameters:

* **items**: List of operations to execute
* **deferLiquidityChecks**: List of user accounts to defer liquidity checks for
* **queryLiquidity**: List of user accounts to return detailed liquidity information for

Returns:

* **output**: Structure with extra information

### trackAverageLiquidity

Enable average liquidity tracking for your account. Operations will cost more gas, but you may get additional benefits when performing liquidations

```text
function trackAverageLiquidity(uint subAccountId) external;
```

Parameters:

* **subAccountId**: subAccountId 0 for primary, 1-255 for a sub-account

### unTrackAverageLiquidity

Disable average liquidity tracking for your account

```text
function unTrackAverageLiquidity(uint subAccountId) external;
```

Parameters:

* **subAccountId**: subAccountId 0 for primary, 1-255 for a sub-account

### getAverageLiquidity

Retrieve the average liquidity for an account

```text
function getAverageLiquidity(address account) external returns (uint);
```

Parameters:

* **account**: User account \(xor in subAccountId, if applicable\)

Returns:

* The average liquidity, in terms of the reference asset, and post risk-adjustment

### pTokenWrap

Transfer underlying tokens from sender's wallet into the pToken wrapper. Allowance should be set for the euler address.

```text
function pTokenWrap(address underlying, uint amount) external;
```

Parameters:

* **underlying**: Token address
* **amount**: The amount to wrap in underlying units

### pTokenUnWrap

Transfer underlying tokens from the pToken wrapper to the sender's wallet.

```text
function pTokenUnWrap(address underlying, uint amount) external;
```

Parameters:

* **underlying**: Token address
* **amount**: The amount to unwrap in underlying units

## IEulerEToken

Tokenised representation of assets

### name

Pool name, ie "Euler Pool: DAI"

```text
function name() external view returns (string memory);
```

### symbol

Pool symbol, ie "eDAI"

```text
function symbol() external view returns (string memory);
```

### decimals

Decimals, always normalised to 18.

```text
function decimals() external pure returns (uint8);
```

### totalSupply

Sum of all balances, in internal book-keeping units \(non-increasing\)

```text
function totalSupply() external view returns (uint);
```

### totalSupplyUnderlying

Sum of all balances, in underlying units \(increases as interest is earned\)

```text
function totalSupplyUnderlying() external view returns (uint);
```

### balanceOf

Balance of a particular account, in internal book-keeping units \(non-increasing\)

```text
function balanceOf(address account) external view returns (uint);
```

### balanceOfUnderlying

Balance of a particular account, in underlying units \(increases as interest is earned\)

```text
function balanceOfUnderlying(address account) external view returns (uint);
```

### reserveBalance

Balance of the reserves, in internal book-keeping units \(non-increasing\)

```text
function reserveBalance() external view returns (uint);
```

### reserveBalanceUnderlying

Balance of the reserves, in underlying units \(increases as interest is earned\)

```text
function reserveBalanceUnderlying() external view returns (uint);
```

### deposit

Transfer underlying tokens from sender to the Euler pool, and increase account's eTokens

```text
function deposit(uint subAccountId, uint amount) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **amount**: In underlying units \(use max uint256 for full underlying token balance\)

### withdraw

Transfer underlying tokens from Euler pool to sender, and decrease account's eTokens

```text
function withdraw(uint subAccountId, uint amount) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **amount**: In underlying units \(use max uint256 for full pool balance\)

### mint

Mint eTokens and a corresponding amount of dTokens \("self-borrow"\)

```text
function mint(uint subAccountId, uint amount) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **amount**: In underlying units

### burn

Pay off dToken liability with eTokens \("self-repay"\)

```text
function burn(uint subAccountId, uint amount) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **amount**: In underlying units \(use max uint256 to repay full dToken balance\)

### approve

Allow spender to access an amount of your eTokens in sub-account 0

```text
function approve(address spender, uint amount) external returns (bool);
```

Parameters:

* **spender**: Trusted address
* **amount**: Use max uint256 for "infinite" allowance

### approveSubAccount

Allow spender to access an amount of your eTokens in a particular sub-account

```text
function approveSubAccount(uint subAccountId, address spender, uint amount) external returns (bool);
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **spender**: Trusted address
* **amount**: Use max uint256 for "infinite" allowance

### allowance

Retrieve the current allowance

```text
function allowance(address holder, address spender) external view returns (uint);
```

Parameters:

* **holder**: Xor with the desired sub-account ID \(if applicable\)
* **spender**: Trusted address

### transfer

Transfer eTokens to another address \(from sub-account 0\)

```text
function transfer(address to, uint amount) external returns (bool);
```

Parameters:

* **to**: Xor with the desired sub-account ID \(if applicable\)
* **amount**: In internal book-keeping units \(as returned from balanceOf\). Use max uint256 for full balance.

### transferFrom

Transfer eTokens from one address to another

```text
function transferFrom(address from, address to, uint amount) external returns (bool);
```

Parameters:

* **from**: This address must've approved the to address, or be a sub-account of msg.sender
* **to**: Xor with the desired sub-account ID \(if applicable\)
* **amount**: In internal book-keeping units \(as returned from balanceOf\). Use max uint256 for full balance.

## IEulerDToken

Tokenised representation of debts

### name

Debt token name, ie "Euler Debt: DAI"

```text
function name() external view returns (string memory);
```

### symbol

Debt token symbol, ie "dDAI"

```text
function symbol() external view returns (string memory);
```

### decimals

Decimals, always normalised to 18.

```text
function decimals() external pure returns (uint8);
```

### totalSupply

Sum of all outstanding debts, in underlying units \(increases as interest is accrued\)

```text
function totalSupply() external view returns (uint);
```

### totalSupplyExact

Sum of all outstanding debts, in underlying units with extra precision \(increases as interest is accrued\)

```text
function totalSupplyExact() external view returns (uint);
```

### balanceOf

Debt owed by a particular account, in underlying units

```text
function balanceOf(address account) external view returns (uint);
```

### balanceOfExact

Debt owed by a particular account, in underlying units with extra precision

```text
function balanceOfExact(address account) external view returns (uint);
```

### borrow

Transfer underlying tokens from the Euler pool to the sender, and increase sender's dTokens

```text
function borrow(uint subAccountId, uint amount) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **amount**: In underlying units \(use max uint256 for all available tokens\)

### repay

Transfer underlying tokens from the sender to the Euler pool, and decrease sender's dTokens

```text
function repay(uint subAccountId, uint amount) external;
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **amount**: In underlying units \(use max uint256 for full debt owed\)

### approveDebt

Allow spender to send an amount of dTokens to a particular sub-account

```text
function approveDebt(uint subAccountId, address spender, uint amount) external returns (bool);
```

Parameters:

* **subAccountId**: 0 for primary, 1-255 for a sub-account
* **spender**: Trusted address
* **amount**: Use max uint256 for "infinite" allowance

### debtAllowance

Retrieve the current debt allowance

```text
function debtAllowance(address holder, address spender) external view returns (uint);
```

Parameters:

* **holder**: Xor with the desired sub-account ID \(if applicable\)
* **spender**: Trusted address

### transfer

Transfer dTokens to another address \(from sub-account 0\)

```text
function transfer(address to, uint amount) external returns (bool);
```

Parameters:

* **to**: Xor with the desired sub-account ID \(if applicable\)
* **amount**: In underlying units. Use max uint256 for full balance.

### transferFrom

Transfer dTokens from one address to another

```text
function transferFrom(address from, address to, uint amount) external returns (bool);
```

Parameters:

* **from**: Xor with the desired sub-account ID \(if applicable\)
* **to**: This address must've approved the from address, or be a sub-account of msg.sender
* **amount**: In underlying. Use max uint256 for full balance.

## IEulerLiquidation

Liquidate users who are in collateral violation to protect lenders

### LiquidationOpportunity

Information about a prospective liquidation opportunity

```text
struct LiquidationOpportunity {
    uint repay;
    uint yield;
    uint healthScore;

    // Only populated if repay > 0:
    uint baseDiscount;
    uint discount;
    uint conversionRate;
}
```

### checkLiquidation

Checks to see if a liquidation would be profitable, without actually doing anything

```text
function checkLiquidation(address liquidator, address violator, address underlying, address collateral) external returns (LiquidationOpportunity memory liqOpp);
```

Parameters:

* **liquidator**: Address that will initiate the liquidation
* **violator**: Address that may be in collateral violation
* **underlying**: Token that is to be repayed
* **collateral**: Token that is to be seized

Returns:

* **liqOpp**: The details about the liquidation opportunity

### liquidate

Attempts to perform a liquidation

```text
function liquidate(address violator, address underlying, address collateral, uint repay, uint minYield) external;
```

Parameters:

* **violator**: Address that may be in collateral violation
* **underlying**: Token that is to be repayed
* **collateral**: Token that is to be seized
* **repay**: The amount of underlying DTokens to be transferred from violator to sender, in units of underlying
* **minYield**: The minimum acceptable amount of collateral ETokens to be transferred from violator to sender, in units of collateral

## IEulerPToken

Protected Tokens are simple wrappers for tokens, allowing you to use tokens as collateral without permitting borrowing

### name

PToken name, ie "Euler Protected DAI"

```text
function name() external view returns (string memory);
```

### symbol

PToken symbol, ie "pDAI"

```text
function symbol() external view returns (string memory);
```

### decimals

Number of decimals, which is same as the underlying's

```text
function decimals() external view returns (uint8);
```

### underlying

Address of the underlying asset

```text
function underlying() external view returns (address);
```

### balanceOf

Balance of an account's wrapped tokens

```text
function balanceOf(address who) external view returns (uint);
```

### totalSupply

Sum of all wrapped token balances

```text
function totalSupply() external view returns (uint);
```

### allowance

Retrieve the current allowance

```text
function allowance(address holder, address spender) external view returns (uint);
```

Parameters:

* **holder**: Address giving permission to access tokens
* **spender**: Trusted address

### transfer

Transfer your own pTokens to another address

```text
function transfer(address recipient, uint amount) external returns (bool);
```

Parameters:

* **recipient**: Recipient address
* **amount**: Amount of wrapped token to transfer

### transferFrom

Transfer pTokens from one address to another. The euler address is automatically granted approval.

```text
function transferFrom(address from, address recipient, uint amount) external returns (bool);
```

Parameters:

* **from**: This address must've approved the to address
* **recipient**: Recipient address
* **amount**: Amount to transfer

### approve

Allow spender to access an amount of your pTokens. It is not necessary to approve the euler address.

```text
function approve(address spender, uint amount) external returns (bool);
```

Parameters:

* **spender**: Trusted address
* **amount**: Use max uint256 for "infinite" allowance

### wrap

Convert underlying tokens to pTokens

```text
function wrap(uint amount) external;
```

Parameters:

* **amount**: In underlying units \(which are equivalent to pToken units\)

### unwrap

Convert pTokens to underlying tokens

```text
function unwrap(uint amount) external;
```

Parameters:

* **amount**: In pToken units \(which are equivalent to underlying units\)

### claimSurplus

Claim any surplus tokens held by the PToken contract. This should only be used by contracts.

```text
function claimSurplus(address who) external;
```

Parameters:

* **who**: Beneficiary to be credited for the surplus token amount

