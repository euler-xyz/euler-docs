# swapAndRepay Work-Flows

swapAndRepay is a flexible primitive in the swap and swap-hub modules that allows us to implement several advanced work-flows in a gas-efficient way. It works by using a uniswap "exact output" swap. This output is determined when the transaction is actually mined, so it will not leave any extra dust due to interest that was accrued while the transaction was pending. Some dust may be left in case of tokens with special handling of the balances, like rebasing or fee-on-transfer tokens.


## Un-short, single collateral

In this case, a user has setup a long/short position. Their account contains only a collateral asset A and a loan in asset B. Typically this is setup by depositing some A, minting B, and then swapping B->A.

This is the canonical example for swapAndRepay. It simply performs the reverse operation.

Steps:

- swapAndRepay A -> B


## Un-short, multiple collaterals

If the user has multiple collaterals, is possible that any one collateral asset could be insufficient to repay the full debt. This is the case where a user first deposits a *different* collateral asset C, and then mints B and swaps B->A.

Here we are assuming that the B liability is larger than the A asset, because of interest accruals (if not, the single collateral method is sufficient, and any remaining A can be swapped into C, if desired).

Steps:

- swap max A -> B
- burn max B
- swapAndRepay C -> B



## Un-mine, fully self-collateralised

"Mining" in this case means a self-collateralised loan, for the purpose of earning EUL tokens. This method is very similar to un-shorting, except that all self-collateralising collateral should be burned first, to minimise swapping fees.

In this case, the additional collateral that is topping up the self-collateralised loan is in the same asset as the loan, B.

Steps:

- max burn B


## Un-mine, different collateral

In this case, the additional collateral A that is topping up the loan is different than the loan itself, B.

First we burn to reduce swapping costs. This ensures the swapAndRepay step sees the smallest possible debt outstanding.

Steps:

- max burn B
- swapAndRepay A -> B


## Un-mine multiple different collaterals

If the user has multiple different collaterals then it is possible that any one collateral asset could be insufficient to repay the full debt. Suppose there is one extra collateral C, in addition to collateral A (and self-collateralised asset B).

Steps:

- swap C -> B (amount calculated off-chain)
- max burn B (burns both self-collateralised amount and swapped amount from previous step)
- swapAndRepay A -> B

Notes:

* A and C are interchangeable here, although the one used in the final step will be the one left with an indeterminate amount after subtracting swapping fees and interest.



## Swap debt asset

In this case, a user has collateral A backing a loan in B. The user wishes to convert this loan B to a loan in a new asset C.

Steps:

- mint "large" amount of C
- swapAndRepay C -> B
- burn max C

Notes:

* The "large" amount of C must be larger than required to pay off the loan in B, including accrued interest while the transaction is pending, and swap fees and slippage. There is no harm in minting a very large amount because any excess will be burned off at no cost. The amount could be the full pool (or maybe 90% in case there are withdrawals while transaction is pending), or could be the value of B adjusted upwards to account for the estimated costs of the above (plus some padding).
* If B is self-collateralised, then "burn max B" should be executed first to reduce the cost of the swap.
* If the user wishes to reduce the size of the debt, then beforehand:
  - swap A -> B (amount calculated off-chain)
  - burn max B
* If the user wishes to increase the size of the debt, then afterwards:
  - borrow C (amount calculated off-chain)
