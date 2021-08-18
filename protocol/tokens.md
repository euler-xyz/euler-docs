---
description: Learn about the system of tokens used on Euler
---

# Tokens

A variety of token types are used on Euler to give users maximum flexibility in how they manage their positions. The token types are described briefly below. You can find more information about each token type in the white paper [here](tokens.md).

## eTokens

Every market has an EToken. This is the primary interface for the tokenisation of **assets** in the Euler protocol:

* **deposit**: Transfer tokens from your wallet into Euler, and receive interest earning tokens in return.
* **withdraw**: Redeem your ETokens for the underlying tokens, which are transfered from Euler to your wallet, along with any interest accrued.

Additionally, ETokens provide an ERC-20 compliant interface which allows you to transfer and approve transfers of your ETokens, as is typical.

Like Compound, but unlike AAVE, these tokens have static balances. That is, accrued interest will not cause the value returned from `balanceOf` to increase. Rather, that fixed balance entitles you to reclaim more and more of the underlying asset as time progresses. Although the AAVE model is conceptually nicer, experience has shown that increasing balance tokens causes a lot of pain to integrators. In particular, if you transfer X ETokens into a pool contract and later withdraw that same X, you have not earned any interest and the pool has some left over dust ETokens that typically aren't allocated to anyone.

A downside of the Compound model is that the values returned from `balanceOf` are in internal bookkeeping units and don't really have any meaning to external users. There is of course a `balanceOfUnderlying` method \(named the same as Compound's method, which may become a defacto standard\) that returns the amount in terms of the underlying and _does_ increase block to block.

## dTokens

Every market also has a DToken. This is the primary interface for the tokenisation of **debts** in the Euler protocol:

* **borrow**: If you have sufficient collateral, Euler sends you the underlying tokens and issues you a corresponding amount of debt tokens.
* **repay**: Transfer tokens from your wallet in order to burn the DTokens, which reduces your debt obligation.

DTokens also implement an ERC-20 compliant interface. Unlike AAVE, where these are non-transferrable, DTokens _can_ be transferred. The permissioning logic is the opposite of ETokens: While you can send your ETokens to anyone without their permission, with DTokens you can "take" anybody else's DTokens without their permission \(assuming you have sufficient collateral\). Similarly, just as you can approve another address to take some amount of your ETokens, you can approve another account permission to send you an amount of DTokens.

As well as providing a flexible platform for debt trading and assignment, this system also permits easy transferring of debt positions between sub-accounts \(see below\).

Unlike ETokens, DToken balances _do_ increase block-to-block as interest is accrued. This means that in order to pay off a loan in full, you should specify MAX\_UINT256 as the amount to pay off, so that all interest accrued at the point the repay transaction is mined gets repaid. Note that most Euler methods accept this MAX\_UINT256 value to indicate that the contract should determine the maximum amount you can deposit/withdraw/borrow/repay at the time the transaction is mined.

In the code you will also see `INTERNAL_DEBT_PRECISION`. This is because DTokens are tracked at a greater precision versus ETokens \(27 decimals versus 18\) so that interest compounding is more accurate. However, to present a common external decimals amount, this internal precision is hidden from external users of the contract. Note that these decimal place amounts remain the same even if the underlying token uses fewer decimal places than 18 \(see the Decimals Normalisation section below\).


## pTokens

"Protected" tokens exist to provide users the option to deposit tokens and use them as collateral, while not permitting them to be loaned out. PTokens provide users with additional safety, at the expense of not earning any interest on the deposited asset. PToken depositors don't need to worry about a pool becoming insolvent, or that their assets will be loaned out when they wish to retrieve them.

Rather than applying this as universal setting on an asset, it is up to the user to decide whether they want to protect their collateral. Since Euler only supports one eToken per underlying asset, a token wrapper contract is used. Users first wrap their underlying tokens into pTokens, and then deposit these pTokens into Euler, receiving "epTokens" which can then be used for collateral.

Another use-case of pTokens is to prevent tokens from being borrowed to perform governance-related attacks. Because the borrowing-prevention check happens inside `increaseBorrow()` \(and not in `checkLiquidity()`\), pTokens cannot even be flash borrowed.


## sTokens

Coming soon.

## rTokens

Coming soon.

