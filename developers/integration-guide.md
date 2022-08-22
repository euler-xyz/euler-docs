---
description: Find out how to start working with the Euler smart contracts
---

# Contract Integration Guide

## Modules

The Euler protocol is a collection of smart contracts connected together with a module system. Each module handles specific areas of the protocol, so depending on what you want to do, you will interact with several different contract addresses.

Some modules are global, for example:

* [markets](https://docs.euler.finance/developers/contract-reference#ieulermarkets): Activating markets, enter/exiting markets, and querying various market-related information.
* [exec](https://docs.euler.finance/developers/contract-reference#ieulerexec): Batch requests, liquidity deferrals (ie, flash loans)
* [liquidation](https://docs.euler.finance/developers/contract-reference#ieulerliquidation): Seizure of assets for users in violation

Other modules are asset-specific:

* [eTokens](https://docs.euler.finance/developers/contract-reference#ieuleretoken): ERC20-compatible tokens that represent assets
* [dTokens](https://docs.euler.finance/developers/contract-reference#ieulerdtoken): ERC20-compatible tokens that represent liabilities

## Deposit and withdraw

In order to invest an asset to earn interest, you need to `deposit` into an eToken.

```javascript
// Approve the main euler contract to pull your tokens:
IERC20(underlying).approve(EULER_MAINNET, type(uint).max);

// Use the markets module:
IEulerMarkets markets = IEulerMarkets(EULER_MAINNET_MARKETS);

// Get the eToken address using the markets module:
IEulerEToken eToken = IEulerEToken(markets.underlyingToEToken(underlying));

// Deposit 5.25 underlying tokens (assuming 18 decimal places)
// The "0" argument refers to the sub-account you are depositing to.
eToken.deposit(0, 5.25e18);

eToken.balanceOf(address(this));
// -> internal book-keeping value that doesn't increase over time

eToken.balanceOfUnderlying(address(this));
// -> 5.25e18
// ... but check back next block to see it go up (assuming there are borrowers)

// Later on, withdraw your initial deposit and all earned interest:
eToken.withdraw(0, type(uint).max);
```

## Borrow and repay

If you would like to borrow an asset, you must have sufficient collateral, and be "entered" into the collateral's market.

```javascript
// Use the markets module:
IEulerMarkets markets = IEulerMarkets(EULER_MAINNET_MARKETS);

// Approve, get eToken addr, and deposit:
IERC20(collateral).approve(EULER_MAINNET, type(uint).max);
IEulerEToken collateralEToken = IEulerEToken(markets.underlyingToEToken(collateral));
collateralEToken.deposit(0, 100e18);

// Enter the collateral market (collateral's address, *not* the eToken address):
markets.enterMarket(0, collateral);

// Get the dToken address of the borrowed asset:
IEulerDToken borrowedDToken = IEulerDToken(markets.underlyingToDToken(borrowed));

// Borrow 2 tokens (assuming 18 decimal places).
// The 2 tokens will be sent to your wallet (ie, address(this)).
// This automatically enters you into the borrowed market.
borrowedDToken.borrow(0, 2e18);

borrowedDToken.balanceOf(address(this));
// -> 2e18
// ... but check back next block to see it go up

// Later on, to repay the 2 tokens plus interest:
IERC20(borrowed).approve(EULER_MAINNET, type(uint).max);
borrowedDToken.repay(0, type(uint).max);
```

## Flash loans

Euler has flash loans built-in as an integral component of the protocol. There are three ways to take a flash loan, a low-level Euler-specific way, a way that uses an [EIP-3156](https://eips.ethereum.org/EIPS/eip-3156) compatible flash-loan adaptor, and a gas-efficient direct interface.

### Low-level Flash Loans

The low-level way to take a flash loan is to defer the liquidity check for your account. The Euler contract will call back into your contract, where you can perform operations like `borrow()` without worrying about liquidity violations. As long as your callback leaves the account in a non-violating state, the transaction will complete successfully.

Since Euler only charges interest for a loan when it is held for a non-zero amount of time, this results in fee-less flash loans.

Here is an example contract that demonstrates this:

```javascript
contract MyFlashLoanContract {
    struct MyCallbackData {
        uint whatever;
    }

    function somethingThatNeedsFlashLoan() {
        // Setup whatever data you need
        MyCallbackData memory data;
        data.whatever = 1234;

        // Disable the liquidity check for "this" and call-back into onDeferredLiquidityCheck:
        IExec(exec).deferLiquidityCheck(address(this), abi.encode(data));
    }

    function onDeferredLiquidityCheck(bytes memory encodedData) external override {
        MyCallbackData memory data = abi.decode(encodedData, (MyCallbackData));

        // Borrow 10 tokens (assuming 18 decimals):

        IEulerDToken(borrowedDToken).borrow(0, 10e18);

        // ... do whatever you need with the borrowed tokens ...

        // Repay the 10 tokens:

        IERC20(borrowed).approve(EULER_MAINNET, type(uint).max);
        IEulerDToken(borrowedDToken).repay(0, 10e18);
    }
}
```

`encodedData` is a pass-through parameter that lets you transfer data to your callback without requiring storage writes.

### EIP-3156 Flash Loans

There is also an adaptor smart contract that exposes Euler's flash loan functionality as an [EIP-3156](https://eips.ethereum.org/EIPS/eip-3156) compatible API.

The smart contract addresses are: [mainnet](https://etherscan.io/address/0x07df2ad9878F8797B4055230bbAE5C808b8259b3), [ropsten](https://ropsten.etherscan.io/address/0x0e60a8406a94787842f07221d2Fb5Bf19856CeA5).

Examples of how to use the adaptor can be found in the EIP documentation, as well as the [Euler test suite](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/test/FlashLoanAdaptorTest.sol). The fee value is always 0.

### Gas-Efficient Direct Flash Loans

As of [eIP-14](https://forum.euler.finance/t/eip-14-contract-upgrades/305), DTokens also support a `flashLoan` method. In most cases, this is now the recommended way to perform a pure flash loan. It is simpler and consumes less gas than either of the above methods. 

To use this, your contract should implement the `IFlashLoan` interface:

    interface IFlashLoan {
        function onFlashLoan(bytes memory data) external;
    }

When you wish to perform a flash loan, your contract should invoke the `flashLoan` function on the DToken that corresponds to the asset you wish to borrow:

    function flashLoan(uint amount, bytes calldata data) external;

The DToken contract will transfer the requested `amount` of tokens (decimals are the same as in the external token contract -- no normalisation needed), and then invoke your contract's `onFlashLoan` function. The `data` parameter you specify is passed to the callback unchanged, which allows you to pass extra data to your contract without requiring expensive storage writes.

Note that any address could call `onFlashLoan` on your contract at any time. You may want to ensure that `msg.sender` is the Euler contract's address, or use some other kind of authentication scheme.

Here is an example:

    import "IEuler.sol";

    contract MyContract {
        function myFunction() external {
            IEulerDToken dToken = IEulerDToken(markets.underlyingToDToken(underlying));
            dToken.flashLoan(amount, abi.encode(underlying, amount));
        }

        function onFlashLoan(bytes memory data) external {
            require(msg.sender == EulerAddrsMainnet.euler, "not allowed");
            (address underlying, uint amount) = abi.decode(data, (uint));

            // ...

            IERC20(underlying).transfer(EulerAddrsMainnet.euler, amount);
        }
    }
