---
description: >-
  Learn about how Euler rewards different assets with lending incentives 
---

# Staking on Euler

  

Staking on Euler is based on Synthetix’s staking contracts. This is an overhaul to Euler’s gauge system, which thanks to [eIP 24](https://snapshot.org/#/eulerdao.eth/proposal/0x7e65ffa930507d9116ebc83663000ade6ff93fc452f437a3e95d755ccc324f93) is modified from its previous iteration coming into effect with the arrival of [Epoch 18.](https://docs.euler.finance/eul/distribution-1)

  

For the duration of the three month trial, 5000 EUL a month (for a total of 15000 EUL) will be distributed to users staking these assets: USDT, USDC and WETH. To stake an asset and receive some of the EUL being distributed, users should stake their [eTokens](https://docs.euler.finance/developers/getting-started/architecture#etoken-less-than-greater-than-dtoken-symmetry) into the staking contract.

  

Should you please, you can immediately unstake your tokens at any time and the accrued EUL earnings will be instantly claimable. There is no lockup period for this staking process.

## Considerations

  

While these eTokens are held in the staking contract, users should be aware that they cannot collateralise loans. You cannot borrow against tokens that are earning these EUL in the staking contract.

  

Make sure when depositing assets into the staking contract that if you have any outstanding liabilities, they are adequately collateralised AFTER you have deposited your USDC/USDT/WETH. Your account will be flagged for [liquidation](https://docs.euler.finance/getting-started/white-paper#liquidations) otherwise.

  
