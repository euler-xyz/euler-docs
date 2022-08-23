---
description: Learn how to borrow assets on Euler
---

# Borrow

## About

Borrowing assets on Euler creates a loan that users can repay at any time. Borrowers pay the Borrow APY rate to lenders. Note that users must first deposit collateral before they can borrow. All loans are over-collateralised, which means that users must deposit more value into the protocol than they can borrow.

## Step-by-step

1. Select `Borrow` in the `Quick Action` menu.
2. Select the Euler sub-account that you want to borrow on.
   * Ensure that you have sufficient collateral deposited in the sub-account, and the sub-account is entered into the market.
3. Select the asset you are interested in.
4. Enter the amount you wish to borrow:
   * The `Max` button is representative of Liquidation x 1.5 to give a better UI experience, but we do not recommend you borrow more than `Safe Max` (unless it is a self-collateralized loan).
   * Select `Safe Max` to borrow enough such that your Euler sub-account will result in having a health score of 1.25 (not supported for self-collateralized loans).
   * Select `Liquidation` to borrow enough such that your Euler sub-account will end up at a health score of 1 (right on the edge of a liquidation).

## FAQ

**I've deposited an asset, but cannot borrow.**\
****Make your transactions were completed successfully. You can only borrow using approved collateral-tier assets, unless you're borrowing the same asset you've deposited. Make sure your collateral is sufficient for the amount you're trying to borrow. Otherwise, please create a support ticket in [Discord](https://discord.gg/CdG97VSYGk).

**How come I can't borrow with an isolated asset?**\
****Note that isolated and Cross assets cannot be used as collateral, but Cross assets can be borrowed alongside other assets, while Isolated assets cannot. Euler aims to curb risk by limiting collateral tier assets to certain tokens with lower risk profiles.
