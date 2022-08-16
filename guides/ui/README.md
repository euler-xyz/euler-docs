---
description: >-
  Find out how to use the Euler Protocol through the interface at
  https://app.euler.finance/
---

# How To

## How to connect to MetaMask

* Click the Connect button at the top right of the page.
* Select your wallet provider in the blocknative window.
* Select your wallet from the list and unlock it.
* Ensure you have selected the correct wallet, and your network is set to the correct one.

## Primary Transactions

Most of these primary transactions can be accessed through the Quick Action menu in the top navbar while several actions will appear as buttons throughout the site for convenience.

#### Withdraw

1. Click on Withdraw and select the Euler sub-account that you want to withdraw your tokens from and ensure that you have funds deposited.
2. Select the asset you are interested in.
3. Enter the amount you wish to withdraw:
   * Select max to withdraw either your full balance or the most that the pool will allow if the pool has less available liquidity than you deposited.
   * Select safe max to withdraw enough such that your Euler sub-account will result in having a health score of 1.25.
   * Select liquidation to withdraw enough such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).

#### Borrow

1. Ensure that the asset of interest is activated, if not, please activate it in the Markets' table on the [homepage](https://app.euler.finance/). If you are activating a new market, remember that borrowing will not be available right away, somebody has to lend the asset first.
2. Select Borrow in the Quick Action menu.
3. Select the Euler sub-account that you want to borrow on.
   * Ensure that you have sufficient collateral deposited in the sub-account, and the sub-account is entered into the market.
4. Select the asset you are interested in.
5. Enter the amount you wish to borrow:
   * The Max button is representative of Liquidation x 1.5 to give a better UI experience, but we do not recommend you borrow more than safe max (unless it is self-collateralized loan).
   * Select Safe Max to borrow enough such that your Euler sub-account will result in having a health score of 1.25 (not supported for self-collateralized loans).
   * Select liquidation to borrow enough such that your Euler sub-account will end up at a health score of 1 (right on the edge of a liquidation).

#### Repay

* If you have not already, you will need to Approve transactions against this asset if they are to be taken from your wallet.

1. Ensure that you have sufficient funds in your wallet or sufficient Euler deposits to repay a loan.
2. Select the Euler sub-account that you want to repay the loan on.
3. If repaying the loan using your Wallet Balance, select the liability asset (loaned asset) then the amount you want to repay.
4. If repaying the loan using Euler deposits, select the liability asset then the amount to repay.
5. Continue by selecting the swapped asset used to repay the loan and the amount.
   * If necessary, an appropriate swap will be made on an external exchange.
   * Users can set the slippage to the desired value by clicking the gear icon in the top-right corner.
6. Select Max to repay your full loan (or maximum amount possible based on your wallet balance/Euler deposits).
7. If a swap is necessary, wait for a quote and click the Swap and Repay button.

#### Mint

Mint creates a self-collateralised loan position, which is a loan collateralised by the same asset. It is an efficient way to create leveraged positions and to mine EUL token.

1. Ensure that the asset you are interested in is already activated; if it is not, you can do this from the Markets' table on the [homepage](https://app.euler.finance/).
2. Ensure that you have sufficient collateral in the sub-account you are minting to.
3. Select the Euler sub-account that you want to mint from.
4. Select the asset you are interested in.
5. Enter the amount you wish to have upon completion.
   * Max here is representative of 19x leverage (right on the edge of a liquidation), and hence we do not recommend you mint more than safe max.
   * Select safe max to mint enough such that your Euler sub-account will result in having a leverage of 15x.
   * Select 0 or the Burn button to burn previously minted position (burn removes an equal amount of deposits and debts from an account).
   * While entering the amount, observe the Multiplier and Time to Liquidation to make a decision.

#### Burn

Burn closes self-collateralised loan positions by removing an equal amount of deposits and debts from an account.

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
   * Select Max to transfer all the selected asset deposits (or maximum amount possible based on your 'from' sub-account positions).
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
6. Enter the amount you wish to sell.
   * Select safe max to sell the amount such that your Euler sub-account will result in having a health score of 1.25.
   * Select liquidation to sell the amount such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).
   * Select max to sell all the selected asset.
   * Users can set the slippage to the desired value by clicking the gear icon in the top-right corner.
7. Wait for a quote and click the Swap button.

#### Short/Long

1. Ensure that you have sufficient collateral in the sub-account you are shorting on.
2. Select the Euler sub-account that you want to short on.
3. Select the asset you wish to short on.
4. Select the asset you wish to use as the collateral.
5. Enter the amount you wish to short:
   * Select safe max to short the amount such that your Euler sub-account will result in having a health score of 1.25.
   * Select liquidation to short the amount such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).
   * Users can set the slippage to the desired value by clicking the gear icon in the top-right corner.
6. Wait for a quote and click the Short button.

#### Wrap

1. Ensure that you have sufficient amount of ETH, WETH, stETH, or WSTETH in your account.
2. Select the assets you want to wrap or unwrap to/from.
3. Enter the amount you wish to wrap or unwrap.
4. Click the wrap/unwrap button.

#### Activate

1. Search and select an unlisted asset.
2. Click Activate to create a market for the token.
   * Unlisted tokens come from community token lists, contact support if the desired token does not appear in the list.
   * Borrowing will not be available right away, somebody has to lend the asset first.

#### Allowances

1. Select an asset from the list.
2. Enter the amount you wish to allow the protocol to approve for use and click Update.
   * Max will allow the protocol to use the total supply of that token, not just what the user owns.
   * Enter 0 (zero) to restrict the protocol from using any more than zero tokens.
3. If listed, change the pre-approved amounts by entering a new amount and clicking Update or by selecting Max.
4. To completely revoke allowance, select the Revoke button.

### Toggle Collateral

1. At the desired sub-account page, find the asset under the supply column.
2. Click the toggle button in the Entered column in the Account view to enter/exit market.
   * Ensure that you have no outstanding borrows on the account that are collateralised by a given asset.

### Transaction Slip

1. The transaction slip can be expanded out from the right side of the UI by clicking the 'OPEN' button.
   * Every time you alter your transaction slip, it automatically checks how much gas you will spend and tries to figure out if there will be any errors.
   * Transactions are executed in the order you have specified, and the order of the transactions can be re-arranged in a drag and drop fashion.
   * You are able to send transactions from different sub-accounts at the same time.

### Accounts

1. In the top right navigation, hover over the icon and click on the Create New button, which will automatically add a new sub-account and simultaneously switch to it.
   * There is no cost to create sub-accounts.
   * Part of opening up ourselves to lending on every market means that we have to protect the system against volatile and potentially malicious tokens. To do this we have categorised assets as isolated, cross and collateral.
   * If the asset is isolated, then you can only borrow and lend on one single asset per sub-account.

### Errors

{% content-ref url="../common-errors.md" %}
[common-errors.md](../common-errors.md)
{% endcontent-ref %}
