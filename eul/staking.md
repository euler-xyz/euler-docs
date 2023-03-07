---
description: >-
  Learn about how Euler rewards different assets with lending incentives 
---

# Staking on Euler

  

Staking on Euler is based on Synthetix’s staking contracts. This is an overhaul to Euler’s gauge system, which thanks to [eIP51](https://snapshot.org/#/eulerdao.eth/proposal/0x551f9e6f3fba50a0fc2c69e361f7a81979189aa7f0ed923a1873bd578896942b) is modified from its previous iteration coming into effect with the arrival of [Epoch 24.](https://docs.euler.finance/eul/distribution-1)

  
According to [eIP51](https://snapshot.org/#/eulerdao.eth/proposal/0x551f9e6f3fba50a0fc2c69e361f7a81979189aa7f0ed923a1873bd578896942b), the DAO has made the decision to keep the staking rewards program running indefinitely, unless another vote is held to terminate the program. The distribution of EUL tokens for staking contracts is as follows:

* 9,000 EUL per epoch to stakers of WETH market.
* 5,000 EUL per epoch to stakers of USDC market.
* 1,000 EUL per epoch to stakers of USDT market.

  

Should you please, you can immediately unstake your tokens at any time and the accrued EUL earnings will be instantly claimable. There is no lockup period for this staking process.

## Considerations

  

While these eTokens are held in the staking contract, users should be aware that they cannot collateralise loans. You cannot borrow against tokens that are earning these EUL in the staking contract.

  

Make sure when depositing assets into the staking contract that if you have any outstanding liabilities, they are adequately collateralised AFTER you have deposited your USDC/USDT/WETH. Your account will be flagged for [liquidation](https://docs.euler.finance/getting-started/white-paper#liquidations) otherwise.

  
