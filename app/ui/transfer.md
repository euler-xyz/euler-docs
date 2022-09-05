---
description: Learn how to transfer assets between sub-accounts on Euler
---

# Transfer

## About

Transfer allows users to move deposited and debt assets between sub-account in Euler. User should ensure any borrow positions will have enough collateral assets in the related sub-accounts prior to transferring any assets.

## Step-by-step

#### Transfer ETokens

1. Ensure that you have sufficient deposits in the sub-account you are transferring from.
2. Select the Euler sub-account that you want to transfer from.
3. Select the Euler sub-account that you want to transfer to.
4. Select the asset you are interested in.
5. Enter the amount you wish to transfer:
   * Select `Max` to transfer all the selected asset deposits (or maximum amount possible based on your 'from' sub-account positions).
   * Select `Safe Max` to transfer enough such that your 'from' Euler sub-account will result in having a health score of 1.25.

#### Transfer DTokens

1. Ensure that you have sufficient debt tokens in the sub-account you are transferring from.
2. Select the Euler sub-account that you want to transfer from.
3. Select the Euler sub-account that you want to transfer to.
4. Select the asset you are interested in.
5. Enter the amount you wish to transfer:
   * Select `Max` to transfer all the selected asset debt (or maximum amount possible based on your 'to' sub-account positions).
   * Select `Safe Max` to transfer enough such that your 'to' Euler sub-account will result in having a health score of 1.25 (not supported for self-collateralized loans).

## FAQ

**Can I transfer multiple assets?**\
****Yes, you will need to make multiple actions sent to the transaction builder.
