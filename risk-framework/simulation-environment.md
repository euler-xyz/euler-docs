# Simulation Environment

To make sure we minimise bad debts whilst maximising activity, we stress-test liquidation scenarios by simulating tail risk events on individual assets as well as on portfolios of assets to estimate protocol risk.   


For instance, if our index list shows that a token jumped from 250th to 30th place and was able to maintain that position for a sufficient amount of time, we may simulate activity versus bad liquidations as a share of total loans given different borrow factors. As a result, we may improve the borrow factor from 0.15 to 0.35.   


Alternatively, we can simulate a more complicated environment with 50 tokens from the lower quartile as borrowed assets backed uniformly by 4 collateral assets \(3 of them time-tested and 1 proposed new collateral\) in high volatility situations. By simulating tail risk scenarios, we can assess the worst case scenario for the protocol and decide whether inclusion of the collateral asset is appropriate.  


