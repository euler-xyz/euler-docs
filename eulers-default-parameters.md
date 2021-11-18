---
description: All of these parameters may be amended by governance
---

# Euler's Default Parameters

## Borrow Factor

When someone activates a lending market on Euler for an asset XYZ, it is by default an isolated tier asset and its **borrow factor is 0.28**.

This means that if you lend USDC (Collateral Factor of 0.90) and borrow XYZ at Default Borrow Factor (Borrow Factor of 0.28), your effective factor is approximately 0.25 (0.90 x 0.28).

Consequently, when borrowing default assets, you are required to be at minimum 4x overcollateralised. The factor is even more conservative if you borrow against an asset with a lower collateral factor.

Conservative overcollateralisation is intended to prevent bad debts.

For eg, suppose the borrowed asset XYZ sharply skyrockets in price, causing a user's health factor to dip below 1, which means he is subject to liquidation. For the liquidator to be incentivised to liquidate the user, he needs to receive an attractive liquidation bonus in terms of violator's lent assets. If there are simply not enough lent assets to back the bonus, a liquidator will choose not to liquidate. This leads to bad debts.

Alternatively, someone could manipulate XYZ pricing lower to be able to borrow a lot more XYZ than normally possible. Eventually, the price gets arbed and normalises, which leads to the health factor dipping below 1. Since the position is heavily overcollateralised, there is still enough collateral backing the loan and hence liquidators are incentivised to repay the debts.

For more info on collateral and borrow factors, check out our risk docs: [https://docs.euler.finance/risk-framework/collateral-and-borrow-factors](https://docs.euler.finance/risk-framework/collateral-and-borrow-factors)

## Reserve Factor

The **default reserve factor is set at 23%**.&#x20;

This means that for every $1 of interest paid by borrowers on an XYZ asset, 23c is paid into the reserve pool of XYZ while the remaining 77c are paid to lenders of XYZ. These reserves may later be used to repay the bad debts that accrue in the pool.

While a higher reserve factor would in theory help accumulate more substantial reserves to backstop the Euler lending pools, at some point it would discourage lenders as they'll receive too little interest.

Alternatively, a reserve factor that's too low is a lost opportunity to build reserves and hence trust with lenders.

We think a reserve factor of 23% is a perfect balance between building reserves and encouraging lending, especially given our generous EUL distribution scheme that will run in the first few years of Euler protocol's existence.

## Interest Rate Model

The **default interest rate model may be found in the interest rate docs.**

While we eventually plan to move to a reactive interest rate model that will optimise for utilisation, we start off with a standard kink model. The default kink model is the "small cap" model and its parameters are:

1. Base IR: **0%** (APR when utilisation is 0%)
2. Kink IR: **25%** (APR when utilisation is exactly Kink%)
3. Max IR: **500% **(APR when utilisation is 100%)
4. Kink%: **50%** (Percent utilisation where kink occurs)

Given the default assets and their respective utilisation can be extremely volatile, it's important the lenders aren't constantly exposed to withdrawal risk.

To that end, should utilisation sharply rise beyond the Kink%, high Max IR makes borrowing too expensive to maintain. This helps bring utilisation below 100% and hence lowers withdrawal risk for lenders.

## Pricing Parameters

### Uniswap3 Pool Fee-Level

The default uniswap3 pool fee-level is the **first existing of 0.3%, 0.05%, 1%**.

In order to retrieve asset prices, Euler uses Uniswap3's Time-Weighted Average Price (TWAP) for the pair XYZ/WETH, where XYZ is the asset in question and WETH is the reference asset. Since Uniswap3 supports multiple pools for the same pair which differ by fee-level, which pool to actually query needs to be configured on a per-asset basis.

Although in theory pools should converge to similar prices due to arbitrage, this is not always the case. For example when a pool has insufficient liquidity to be profitable for arbitrage bots. Additionally, the amount of liquidity has an impact on the cost of price manipulation.

In order to be promoted up a tier, a review of the configured pool fee must be conducted. In some cases, extra "full-range liquidity" must be added to increase the cost of price manipulation.

### TWAP Length

The **default TWAP length is set at 30 minutes.**

Euler uses Uniswap v3 TWAPs as the pricing oracle for all assets and debts on Euler.

As explained in our [whitepaper](https://docs.euler.finance/getting-started/white-paper#twap), a TWAP is essentially a moving average of trades that occurred in a given Uniswap v3 pool. The intention for using TWAPs is that it makes price manipulations prohibitively expensive the longer the TWAP window is.

However, a TWAP that's too long causes a significant lag between last-traded price on Uniswap and the TWAP, leading to risks of bad debt.

For eg, a user deposits ETH as collateral and borrows XYZ token. Imagine that the user's XYZ debt swells to $70 worth and he's subject to liquidation. A liquidator would have to take on some of that XYZ debt and repay it.

However, recall that while the debt is priced in TWAP terms, a liquidator would need to buy XYZ on the market to repay that debt. If the market price of his debt is $120, the liquidator would be buying high on the market to receive a smaller amount of TWAP-priced assets of the violator plus liquidation bonus.

Hence, when the TWAP - Market Price spread become significantly large due to the TWAP lag, a liquidation may be uneconomical.

Alternatively, a TWAP that's too short means it becomes a lot cheaper to manipulate asset prices. For eg, one could artificially pump a collateral asset's price to be able to borrow disproportionate amount of XYZ tokens and run away with them.

Check out this paper written by Michael Bentley on cost of attacking TWAP pricing: [https://github.com/euler-xyz/uni-v3-twap-manipulation/blob/master/cost-of-attack.pdf](https://github.com/euler-xyz/uni-v3-twap-manipulation/blob/master/cost-of-attack.pdf)

Additionally, have a look at this blog post by Seraphim on possible attacks involving oracle manipulation and how Euler is preventing them: [https://blog.euler.finance/risks-in-crypto-a-lending-protocol-perspective-376e19c1d01a](https://blog.euler.finance/risks-in-crypto-a-lending-protocol-perspective-376e19c1d01a)

### Uniswap Observation Cardinality

The **minimum uniswap3 cardinality is 10**. When a market is activated, the cardinality of the uniswap3 pool that will be used for pricing is increased to this value, if it is currently below it.

In order to maintain the TWAP, each Uniswap3 pool needs to keep a historical record of accumulated prices at previous points in time. Each record is called an observation, and their number is called the observation cardinality. Unfortunately, reserving the storage for these records costs gas.

The larger the cardinality, the longer the possible TWAP window. If a swap is executed every block, the longest TWAP that is possible is the cardinality times the average block time over the last N blocks.

On Euler, if it is not possible to retrieve a TWAP of the configured length, then the oldest available price is used instead. This means that the protocol can always be interacted with, and prevents some types of attacks that aim to prevent liquidation. However, it also means that the cardinality is an important security parameter for a pool.

This low minimum value ensures that activating a market is not too expensive. However, since a larger cardinality is required to ensure a longer TWAP window, in order for an asset to be promoted to a higher tier, a larger value cardinality will be required, typically 144 or higher.

## Liquidation Parameters

### Target Health Factor

The **default target health factor is 1.25**.&#x20;

When a user is in violation due to his risk-adjusted liabilities exceeding his risk-adjusted collateral, his health factor dips below 1. However, should a liquidator come in, he may only take enough debt and assets from the violator to shift his health factor to 1.25.

This is feature is called \*\*soft liquidating \*\*someone [as described in the whitepaper](https://docs.euler.finance/getting-started/white-paper#soft-liquidations), and it creates a much better borrowing experience than on other protocols, where 50% of your debt is liquidated.

Nevertheless, had we set the target health factor to 1.00, we would have ran into the risk of making liquidations uneconomic. Namely, the size of debt being repaid and the consequent reward may be too small to incentivise a liquidator.

Similarly, in a volatile market, being restored to 1.00 means a user may quickly dip below 1.00 again and again, which implied higher gas fees for liquidators and ever-decreasing rewards.

We think 1.25 is a good trade-off between a good borrowing experience and well-incentivised liquidations.

### Maximum Liquidation Discount

The **default maximum liquidation discount is set at 20%.**

When a user is subject to liquidation, some of his debt (dTokens) and assets (eTokens) are transferred to the liquidator, which leads to the health score shifting to 1.25.

However, to incentivise the liquidator to do this work, he receives the eTokens at a discount. Another way of thinking about the discount is receiving a bonus on top of the asset value.

Let's imagine a simple example without liquidation surcharges and boosters (explained in this page below): assume a user's health factor is 0.90. This implies a liquidation discount of 10% (1 - 0.90). Hence, for taking on $100 worth of dTokens, a liquidator receives $110 worth of eTokens.

If the discount is too low, a liquidator may be discouraged from conducting the liquidation. Alternatively, a discount that's too high means borrowers are giving away too much of their assets to liquidators. This also creates a risk of never going back to 1.25 health score, as every liquidation decreases the amount of assets a user has.

Hence, a liquidation discount has an upper ceiling of 20% to improve the borrowers' experience.

### Liquidation Surcharge

The **default liquidation surcharge is set at 2%.**

Whenever a liquidator takes on someone's debt, they need to repay 2% more than originally taken from the violator. To compensate him for that, the violator pays the liquidator an additional 2% of his lent assets.

This is intended to do two things:

1. The surcharge accumulates in the reserve pool, hence every liquidation makes the pool healthier. The more volatile an asset, the more often liquidations occur, and the bigger the pool is.
2. Discourage malicious self-liquidation strategies. Due to the surcharge, every self-liquidation ends up being net negative.

### Liquidation Booster Ceiling and Slope

The **default liquidation booster is ceiling and slope are set at 2.5% and 2x respectively.**

To incentivise liquidators to lend, they may be more competitive than their peers should they lend through Euler.

For eg, if a user's health score is at 0.90 and value of risk-adjusted debt is $1000, the implied liquidation discount is 10% (1 - Health Score). However, due to slippage and gas fees, liquidators are only profitable at a 11% discount.

At the same time, a liquidator that supplied $1000 risk-adjusted collateral can be 2x more competitive than the rest of the market with a ceiling of 2.5%. Should he take on the user's debt at a 10% discount, he will actually receive a more generous 12.5% discount (2.5% booster + 10% liquidation discount).

How did we arrive at that number? The **total liquidation discount** is calculated the following way:

$$
TotalLiqDiscount = (1-HealthFactor)*LiqBooster + LiqSurcharge
$$

$$
LiqBooster = 2 * \frac{min(RADV, RASAL)}{RADV}
$$

RASAL = Risk-adjusted supplied assets by the liquidator

RADV = Risk-adjusted debt by the violator

_LiqSurcharge is explained above in this page and in this example is assumed to be 0 for simplicity's sake._

**2x is the liquidation booster slope**.

**The Liquidation Booster is subject to a 2.5% ceiling.**

The reasoning behind setting the ceiling at 2.5% is the same as the 20% maximum liquidation discount: preventing the borrowers from overpaying when being liquidated. The 2x slope, on the other hand, is intended to make the liquidators gradually more competitive the more assets they deposit, but not outrageously more competitive to avoid the creation of monopolies.
