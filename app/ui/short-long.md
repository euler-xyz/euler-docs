---
description: Learn how to create short or long positions in Euler
---

# Short/Long

## About

Short allows users to build a leveraged short position by borrowing and then immediately selling an asset using external exchange (1inch or Uniswap).&#x20;

## Step-by-step

1. Ensure that you have sufficient collateral in the sub-account you are shorting on.
2. Select the Euler sub-account that you want to short on.
3. Select the asset you wish to short on.
4. Select the asset you wish to use as the collateral.
5. Enter the amount you wish to short:
   * Select `Safe Max` to short the amount such that your Euler sub-account will result in having a health score of 1.25.
   * Select `Liquidation` to short the amount such that your Euler sub-account will end up at health score 1 (right on the edge of a liquidation).
   * Users can set the `slippage` to the desired value by clicking the `gear icon` in the top-right corner.
6. Wait for a quote and click the `Short` button.

## FAQ

**I'm creating a Short/Long position, so why do I see the asset in a Self Collateral and Self Liability row?**\
****The asset is sold and redeposited on Euler, which creates the self collateral/liability row, but your intended position is there.
