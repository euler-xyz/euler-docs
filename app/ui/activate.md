---
description: Learn how to activate a market in Euler
---

# Activate

## About

Users can activate new lending markets for assets on Euler in a permissionless way. Assets must have a Uniswap V3 WETH paired pool and should be listed on [CoinGecko](https://coingecko.com/) in order to appear in the asset's table. Since Euler uses Uniswap's V3 pools for the market's oracle, it's highly recommended to only activate pools with sufficient and wide range liquidity. Check out an asset's oracle risk [here](https://oracle.euler.finance/).

## Step-by-step

1. Search and select an unlisted asset.
2. Click `Activate` to create a market for the token.
   * Unlisted tokens come from community token lists, contact support if the desired token does not appear in the list.
   * Borrowing will not be available right away, somebody has to lend the asset first.

## FAQ

**Where can I Activate a market?**\
****Search for an asset in the search bar on the [Euler app](https://app.euler.finance/).&#x20;

**I've activated a market, how come I cannot use it as collateral?**\
****Newly activated markets are automatically set as isolated tier assets. Create a proposal to make it a collateral tier asset if it has sufficient liquidity in its oracle.
