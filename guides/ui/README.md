---
description: >-
  Find out how to use the Euler Protocol through the interface at
  https://app.euler.finance/
---

# How To

## How to connect to metamask

* Click the Connect button at the top right of the page.
* Select your wallet from the list and unlock it.
* Ensure you have selected the correct wallet, and your network is set to the correct one.

## Primary Transactions

#### Deposit

* If you have not already, you will need to Approve transactions against this asset.

1. Ensure that the asset you are interested in is already activated; if it is not, you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Select the Euler sub-account that you want to deposit your tokens into.
3. Select the asset you are interested in.
4. Enter the amount you wish to deposit (or hit Max to send the full available balance in your wallet) and this will add it to our batch transaction slip.

#### Withdraw

1. Select the Euler sub-account that you want to withdraw your tokens from and ensure that you have funds deposited.
2. Select the asset you are interested in.
3. Enter the amount you wish to withdraw:

* Select max to withdraw either your full balance or the most that the pool will allow if the pool has less available liquidity than you deposited.
* Select safe max to withdraw enough such that your Euler sub-account will result in having a health score of 1.25.
* Select liquidation to withdraw enough such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

#### Borrow

1. Ensure that the asset you are interested in is already activated; if it is not, you can do this from the Markets table on the homepage (https://app.euler.finance/). If you are activating a new market remember that borrowing will not be available right away, somebody has to lend the asset first.
2. Ensure that you have sufficient collateral deposited in the relevant sub-account you are trying to borrow on and on the account page, the sub-account is entered into the market.
3. Select the Euler sub-account that you want to borrow on.
4. Select the asset you are interested in.
5. Enter the amount you wish to borrow:

* Max here is representative of Liquidation x 1.5 to give a better UI experience, but we do not recommend you borrow more than safe max (unless it is self-collateralized loan).
* Select safe max to borrow enough such that your Euler sub-account will result in having a health score of 1.25 (not supported for self-collateralized loans).
* Select liquidation to borrow enough such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

#### Repay

* If you have not already, you will need to Approve transactions against this asset if they are to be taken from your wallet.

1. Ensure that you have sufficient funds in your wallet or sufficient Euler deposits to repay a loan.
2. Select the Euler sub-account that you want to repay the loan on.
3. Select the source of the assets used to repay the loan.
4. Select the asset you have a loan in.
5. If repaying the loan using Euler deposits, select the asset you are using to repay.
6. If repaying the loan using Euler deposits, appropriate swap on external exchange will be made if necessary. If that is the case, set the slippage to desired value.
7. Enter the amount you wish to repay:

* Select Max to repay your full loan (or maximum amount possible based on your wallet balance/Euler deposits).

1. If swap necessary, wait for a quote and click the Swap and Repay button.

#### Mint

Mint creates a self-collateralized loan position, which is a loan collateralized by the same asset. It is efficient way to create leveraged positions and mine EUL token.

1. Ensure that the asset you are interested in is already activated; if it is not, you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient collateral in the sub-account you are minting to.
3. Select the Euler sub-account that you want to mint/burn from.
4. Select the asset you are interested in.
5. Enter the amount you wish to end up with after transaction execution:

* Max here is representative of 19x leverage (right on the edge of a liquidation), hence we do not recommend you mint more than safe max.
* Select safe max to mint enough such that your Euler sub-account will result in having a leverage of 15x.
* Select 0 to burn previously minted position (burn removes an equal amount of deposits and debts from an account)
* While entering amount, observe the Multiplier and Time to Liquidation to make a decision.

#### Burn

Burn creates a self-collateralized loan position, which is a loan collateralized by the same asset.

1. Ensure that you have sufficient supply & debt tokens in the sub-account you are burning on.
2. Select the Euler sub-account that you want to burn on.
3. Select the asset you are interested in.
4. Enter the amount you wish to burn:

* Select Max to burn all available of selected asset.
* While entering amount, observe the Multiplier to make a decision.

#### Transfer ETokens

1. Ensure that you have sufficient deposits in the sub-account you are transferring from.
2. Select the Euler sub-account that you want to transfer from.
3. Select the Euler sub-account that you want to transfer to.
4. Select the asset you are interested in.
5. Enter the amount you wish to transfer:

* Select Max to transfer all the selected asset deposits (or maximum amount possible based on your 'from' sub-account positions)
* Select safe max to transfer enough such that your 'from' Euler sub-account will result in having a health score of 1.25.

#### Transfer DTokens

1. Ensure that you have sufficient debt tokens in the sub-account you are transferring from.
2. Select the Euler sub-account that you want to transfer from.
3. Select the Euler sub-account that you want to transfer to.
4. Select the asset you are interested in.
5. Enter the amount you wish to transfer:

* Select Max to transfer all the selected asset debt (or maximum amount possible based on your 'to' sub-account positions).
* Select safe max to transfer enough such that your 'to' Euler sub-account will result in having a health score of 1.25 (not supported for self-collateralized loans).

#### Swap

1. Ensure you have sufficient supply tokens in the sub-account you want to swap from.
2. Select the Euler sub-account that you want to swap from.
3. Select the Euler sub-account that you want to swap to.
4. Select the asset you wish to sell.
5. Select the asset you wish to buy.
6. Enter the amount you wish to sell:

* Select safe max to sell the amount such that your Euler sub-account will result in having a health score of 1.25.
* Select liquidation to sell the amount such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).
* Select max to sell all the selected asset.

1. Wait for a quote and click the Swap button.

#### Short

1. Ensure that you have sufficient collateral in the sub-account you are shorting on.
2. Select the Euler sub-account that you want to short on.
3. Select the asset you wish to short on.
4. Select the asset you wish to use as the collateral.
5. Enter the amount you wish to short:

* Select safe max to short the amount such that your Euler sub-account will result in having a health score of 1.25.
* Select liquidation to short the amount such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

1. Wait for a quote and click the Short button

#### Wrap

1. Ensure that you have sufficient amount of ETH or WETH in your account.
2. Click on swap icon to change the mode to wrap-unwrap or unwrap-wrap.
3. Enter the amount you wish to wrap or unwrap.
4. Enter ETH value to wrap ETH into WETH.
5. Enter WETH value to unwrap into ETH.

### Toggle Collateral
* Ensure that you have no outstanding borrows on the account that are collateralized by given asset.
* Click the toggle button in the Entered column in the Account view to enter/exit market.

### Transaction Slip

* This can be expanded out from the right side of the UI by clicking 'OPEN' button.
* Every time you alter your transaction slip, it automatically checks how much gas you will spend and tries to figure out if there are going to be any errors.
* Transactions are executed in the order you have specified, and the order of the transactions can be re-arranged in a drag and drop fashion.
* You are able to send transactions from different sub-accounts (more on that later) at the same time.

#### Errors

* COMING SOON

### Accounts

* Part of opening up ourselves to lending on every market means that we have to protect the system against volatile and potentially malicious tokens. To do this we have categorised assets as isolated, cross and collateral.&#x20;
* If the asset is isolated then you are only able to borrow and lend on one single asset per sub-account.
* To create a new sub-account is free and simple, you just have to press the Create New button in the top right navigation, and you will automatically add a new sub-account and simultaneously switch to it.
