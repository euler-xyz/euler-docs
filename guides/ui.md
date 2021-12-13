---
description: Find out how to lend and borrow crypto assets using the Euler app at https://app.euler.finance/
---

# User Interface Guide

## How to connect to metamask

* Click the Connect button at the top right of the page.
* Select metamask from the list.
* Enter your password into the metamask popup to unlock your metamask.
* Ensure you have selected the correct wallet; and your network is set to the correct one.

## Primary Transactions

#### Deposit
* If you have not already, you will need to Approve transactions against this asset.
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Select the Euler sub-account that you want to deposit your tokens into.
3. Select the asset you are interested in.
4. Enter the amount you wish to deposit (or hit Max to send the full available balance in your wallet) and this will add it to our batch transaction slip.

#### Withdraw
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have funds deposited in the relevant sub-account you are trying to withdraw from.
3. Select the Euler sub-account that you want to withdraw your tokens from.
4. Select the asset you are interested in.
5. Enter the amount you wish to withdraw:
* Select max to withdraw either your full balance or the most that the pool will allow if the pool has less available liquidity than you deposited.
* Select safe max to withdraw enough such that your Euler sub-account will result in having a health score of 1.25.
* Select liquidation to withdraw enough such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

#### Borrow
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient collateral deposited in the relevant sub-account you are trying to borrow on and on the account page, the asset is entered into the market.
3. Select the Euler sub-account that you want to borrow on.
4. Select the asset you are interested in.
5. Enter the amount you wish to borrow:
* Max here is representative of Liquidation x 2 to give a better UI experience, but we do not recommend you borrow more than safe max.
* Select safe max to borrow enough such that your Euler sub-account will result in having a health score of 1.25.
* Select liquidation to borrow enough such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

#### Repay
* If you have not already, you will need to Approve transactions against this asset.
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient funds in your wallet to repay a loan.
3. Select the Euler sub-account that you want to repay the loan on.
4. Select the asset you are interested in.
5. Enter the amount you wish to repay:
* Select Max to repay your full loan.

#### Mint
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient collateral in the sub-account you are minting to.
3. Select the Euler sub-account that you want to mint from.
4. Select the asset you are interested in.
5. Enter the amount you wish to mint:
* Max here is representative of Liquidation x 2 to give a better UI experience, but we do not recommend you mint more than safe max.
* Select safe max to mint enough such that your Euler sub-account will result in having a health score of 1.25.
* Select liquidation to mint enough such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

#### Burn
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient supply & debt tokens in the sub-account you are burning on.
3. Select the Euler sub-account that you want to burn on.
4. Select the asset you are interested in.
5. Enter the amount you wish to burn:
* Select Max to burn all available of selected asset.

#### Transfer ETokens
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient supply tokens in the sub-account you are transferring from.
3. Select the Euler sub-account that you want to transfer from.
4. Select the Euler sub-account that you want to transfer to.
5. Select the asset you are interested in.
6. Enter the amount you wish to transfer:
* Select Max to transfer all the selected asset.

### Transfer DTokens
1. Ensure that the asset you are interested in is already activated; if it is not you can do this from the Markets table on the homepage (https://app.euler.finance/).
2. Ensure that you have sufficient debt tokens in the sub-account you are transferring from.
3. Select the Euler sub-account that you want to transfer from.
4. Select the Euler sub-account that you want to transfer to.
5. Select the asset you are interested in.
6. Enter the amount you wish to transfer:
* Select Max to transfer all the selected asset.

### Toggle Collateral
* Ensure that you have no outstanding borrows on the account.
* Click the toggle collateral button to add a collateral toggle to the transaction slip.

### Transaction slip
* This can be expanded out from the right side of the UI at any point.
* Everytime you alter your transaction slip it automatically checks how much gas you will spend and tries to figure out if there are any going to be any errors.
* Transactions are executed in the order you have specified and the order of the transactions can be re-arranged in a drag and drop fashion.
* You are able to send transactions from different accounts (more on that later) at the same time.

### Accounts
* Part of opening up ourselves to lending on every market means that we have to protect the system against volatile and potentially malicious tokens. To do this we have categorised assets as isolated, cross and collateral. <- Check
* If the asset is isolated then you are only able to borrow and lend on one single asset per sub account.
* To create a new account is free and simple, you just have to press the plus button in the top right navigation and you will automatically add a new subaccount and simulateonously switch to it.