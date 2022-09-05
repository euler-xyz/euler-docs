---
description: Learn how to deposit assets on Euler and begin earning interest
---

# Deposit

## About

Depositing into Euler allows users to supply assets to borrowers and earn the Supply APY for an asset. Depositing collateral is also the first step in being able to borrow assets on Euler.&#x20;

## Step-by-step

1. Click the `Quick Action` button in the navigation bar.
2. From the menu, choose `Deposit`.
3. Select the sub-account you wish to deposit into and the asset you wish to deposit.
   * **Note**: if you have not yet approved Euler to be able to use this asset, you will need to `Enable` it first. In some cases you can achieve this with `Sign Permit` which is a type of gasless approval (free).&#x20;
4. If you wish to use the asset as collateral to take out loans, check the `Enter market` box.
   * **Note**: you can only borrow against 'Collateral' tier assets. You will not be able to borrow against assets listed as 'Cross' or 'Isolated'. Entering the market for these type of assets will  make them available to liquidators during liquidation events, but will not increase your borrowing power.
5. Enter the amount you wish to deposit (or hit `Max` to send the full available balance in your wallet).
6. Click `Deposit`. Your transaction will move to the `Transaction Builder`, which is a kind of shopping trolley for transactions. From here you have two options:
   1. Click `Send txs` to immediately submit the deposit.
   2. Add more transactions by revisiting the `Quick Action` button. You can then submit them all at once by clicking `Send txs`. This approach generally saves gas over submitting multiple individual transactions.

## FAQ

**I deposited, but the asset does not show up in my account.**\
****Make sure the deposit transactions did not fail, otherwise please create a support ticket in [Discord](https://discord.gg/CdG97VSYGk).
