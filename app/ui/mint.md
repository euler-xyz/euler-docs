---
description: Learn how to mint assets on Euler for self-collateralised positions
---

# Mint

## About

Mint is a unique function on Euler that enables users to simulate a recursive borrowing strategy. Mint creates equal amounts of deposits and debts for the same asset. It is often the starting point for creating a multiplied long/short position or used for liquidity mining (when lending/borrowing on a particular market is incentivised).

### **Example**&#x20;

A user first does a `Deposit` of $1000 of USDC. They then `Mint` $5000 USDC. Their account now has a total of $6000 USDC deposits, and $5000 USDC debts. This gives them a multiplied position, since they hold more debt than their initial deposit would allow for.

The `Mint` function mimics what would happen if a user deposited $1000 USDC, then borrowed $900 USDC, then redeposited that $900 USDC, to borrow $810 more USDC, and so on.&#x20;

## Step-by-step

1. Ensure that you have sufficient collateral in the sub-account you are minting to.
2. Select the Euler sub-account that you want to mint from.
3. Select the asset you are interested in.
4. Enter the amount you wish to have upon completion.
   * `Max` here is representative of 19x multiplier (right on the edge of a liquidation), and hence we do not recommend you mint more than safe max.
   * Select `Safe Max` to mint enough deposits and debt such that your Euler sub-account will result in having a multiplier of 15x.
   * Select 0 or the Burn button to burn a previously minted position (burn removes an equal amount of deposits and debts from an account).
   * While entering the amount, observe the Multiplier and Time to Liquidation to make a decision.

## FAQ

**Can I be liquidated if I use mint?**\
****Mint creates a multiplier position which poses liquidation risk when Mint an asset different from the user's collateral. Additionally, the interest rates also present risk of loss as they're variable and dependent on the market.
