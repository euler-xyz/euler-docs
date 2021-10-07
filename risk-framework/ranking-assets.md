# Ranking Assets

## **Scale** 

Each risk parameter goes from 0 \(highest risk\) to 1 \(lowest risk\). The combination of risk parameters results in a comprehensive index for a given digital asset, which also goes from 0 to 1.

## **Risk Parameters**

### **Smart Contract Risk** 

Smart contract risk parameter can either be 0, 0.5 or 1.

It is arguably the biggest tail risk, as a badly written smart contract can result in hacks and stolen money, leading to catastrophic collapse in price.

We assess this by checking **whether the protocol was audited**, the **number of days the protocol has been functioning without hacks** and deeper research if needed \(for promoting up the tiers\).

### **Centralisation** 

Centralisation parameter can go from 0 to 1.

It measures whether a small number of holders have undue influence over the token. For example, a founder with 70% ownership of the tokenomics pie and flexible vesting period can oversupply the market with tokens, leading to an abrupt selloff. Alternatively, a whale holding a large chunk of tokens can easily pass deleterious changes through governance.

This risk can be measured by estimating the **median size of token amount per holder**. When the ownership structure isn’t transparent, we will employ forensic due diligence.

### **Volatility** 

Volatility parameter can go from 0 to 1.

All other things equal, an asset with 100% realised volatility is more likely to cause a liquidation than an asset with a 10% realised volatility. Hence, less volatile assets should have more favourable borrowing and collateral factors.

This parameter can be measured via **realised** \(and implied, if available\) **volatility**, with emphasis on downside risk for collaterals and upside risk for borrowed assets.

### **Liquidity** 

Liquidity parameter can go from 0 to 1.

An asset with 100 mio USD daily turnover is easier to buy and sell versus an asset with only 1 mio USD turnover, all other things being equal.

This is particularly important for liquidators that receive collateral assets at discount for repaying borrowed tokens, as they typically immediately sell that collateral. If they’re unable to sell that collateral and/or buy the borrowed asset at a decent price given a liquidator discount, then they do not have the incentive to liquidate. This leads to bad debts, which we need to minimise.

Measuring liquidity can be done by **estimating historical slippage** caused by a certain amount of volume. 

It's important to note that we are estimating the liquidity **vs ETH on Uniswap v3**, as an existing ETH market on Uniswap v3 is a prerequisite to being activated on Euler and our oracles are based on Uniswap v3 TWAPs. 

This means that even if a token has very high liquidity on Uniswap v2, it wouldn't have a high borrow factor if liquidity is low on Uniswap v3.

