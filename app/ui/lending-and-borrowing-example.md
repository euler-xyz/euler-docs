---
description: >-
  Below is a basic example of lending and borrowing on Euler protocol. This is
  not financial advice and only serves as an educational example on using the
  protocol.
---

# Lending and Borrowing

Let’s say you want to borrow XYZ token. XYZ token ranks high in the index list, and therefore has a borrow factor of 0.80.

### **Lending**

Since the loan is collateralised, you first need to deposit (lend) one or more collateral assets. You deposit ABC, which is a stable coin with a collateral factor of 0.90.

You lend 1000 ABC (1000 USD worth), receive eABC (claim on deposited ABC and interest accrued from utilisation). Note that the more users borrow your ABC tokens, the more interest you accrue and hence the higher value of your collateral.

### Borrowing

To calculate the maximum amount of XYZ you can borrow, multiply the borrow and collateral factors: 0.80 x 0.90 = 0.72. Consequently, you can borrow up to 720 USD worth of XYZ against 1000 ABC (0.72 x 1000 ABC).

If you decide to borrow 700 USD worth of XYZ, Euler will mint an equivalent amount of dXYZ (debt token equal to principal amount owed and accrued borrowing costs). Note that if borrowing rates rise, your debt levels will increase as well.

### Liquidation Risks

If XYZ token rose in price and/or borrowing interest rose significantly so that the value of your dXYZ rose above 720 USD, you are subject to liquidation and your claim on the collateral (eABC) will be given to a liquidator at a discount as well as your debts (dXYZ) in exchange for repaying the debt.

Similarly, should the value of ABC plummet, your eABC won’t be enough to maintain the 0.72 factor, and you will be subject to the same liquidation procedure.

### Return Potential

Alternatively, if you borrowed XYZ, sold it and XYZ price plummeted, you’d be able to repay your debts at a lower level and make a profit. You could also utilize your position by selling XYZ, buying more collateral, borrowing more XYZ etc. until you reach the borrowing limit. This way, you’d have a multiplied short XYZ/ABC position. More on the mechanics of multiplied positions [here](https://medium.com/@Hoytech/82402529c51b).

_Note: we have implemented the swap module that allows users to utilize their positions easily without incurring additional gas fees._
