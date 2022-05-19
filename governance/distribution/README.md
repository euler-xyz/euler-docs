---
description: >-
  Learn more about how EUL is distributed to protocol users to decentralise
  governance
---

# Distribution

## Introduction&#x20;

In order to progressively decentralise governance of the Euler Protocol, EUL will be distibuted to protocol users over a period of (at least) 4 years. The distribution programme is broken down into cycles called [epochs](distribution.md). Every epoch EUL gets distributed to borrowers on a subset of community-selected markets. The markets eligible for a distribution are determined by an EUL staking [gauge ](gauges.md)system.

## How it Works

The amount of EUL each borrower receives is proportional to the time-weighted amount of debt they held of an asset within the epoch. For example, if 50 EUL are to be distributed to the DAI market in epoch 3, and if Alice borrows 10 DAI for 1 day, and Bob borrows 5 DAI for 2 days, then at the end of the epoch they will both be able to claim an equal share of 25 EUL.

## Recursive Borrowing

All systems for distributing tokens to users are vulnerable to being gamed. On other lending protocols, professional yield farmers will often try to game token distributions by recursively lending and borrowing the same asset over and over again. Whilst gaming the distribution in this way does no harm to a protocol _per se,_ it does limit decentralisation of its token supply.&#x20;

This is because recursive borrowing is difficult strategy to employ for most ordinary users, requiring large amounts of starting capital, as well as knowledge of flash loans and the ability to write smart contract-based yield farming strategies. Ultimately this knowledge gap means that a subset of well-capitalised professional yield farmers are able to claim a disproportionate share of the distribution.&#x20;

Attempting to ban or otherwise regulate recursive borrowing, as some have suggested, is a poor solution to this problem. In general, regulations make such things worse, rather than better. Well-capitalised professionals are often placed at an even better advantage than if no regulations existed at all. Banning recursive borrowing can easily be sidestepped by professionals using smart contracts by routing borrowing through multiple Ethereum address, for example. In any case, recursive borrowing is a legitimate strategy many users employ whilst setting up a leveraged long/short postion.&#x20;

Instead of try to regulate recursive borrowing, therefore, Euler instead makes recursive borrowing easier. The logic behind this approach may seem a little strange at first, but this approach follows the principle of free and fair markets, democratising the process by which users can game the distribution. It enables users of any asset, with any amount of starting capital, to deploy the same strategy as the professionals. Any user can recursively borrow any asset on Euler by using the Mint function.&#x20;

### Using Mint

A user with $1000 RBN in their wallet can recursively borrow using the following approach:

* Deposit $1000 RBN&#x20;
* Mint $10,000 RBN&#x20;

Mint is a function that creates equal amounts of deposits and debts for an asset on Euler. It is often used whilst setting up a leveraged long/short position. However, it can also be used to do a form of recusrive borrowing. In particular, note that the end result in the above example is that the user has $11,000 RBN deposits, and $10,000 RBN debts. Exactly the same as if they had deposited and borrowed over and over again many times.&#x20;

Note that if they had simply borrowed RBN without using Mint, they would have been able to borrow <$1,000 worth of RBN (because of the over-collateralisation requirement). Thus, the user has increased their borrowing power by 10x using this approach.&#x20;

### Risks&#x20;

Users taking the approach above, depositing and borrowing the same asset, will have a health score of exactly 1 (sometimes slightly higher sometimes if they do it with a collateral asset). This is because RBN can self-collateralise a loan of itself, but does not add any more borrowing power than is strictly needed to a user's account.&#x20;

Changes in price of RBN will have no effect on a user's health score, because their collateral deposits rise and fall at the same rate as their debts. So, is a user at risk of liquidation? This depends on how much more interest they are paying on their debts than they are earning on their deposits.&#x20;

The excess interest paid on debts will eventually eat into their initial $1,000 RBN deposit. How long the user has until liquidation depends how high the excess interest rate is. This is measure on the Euler as the estimated time to liquidation (TTL). It is important to recognise that this estimate assumes fixed interest rates though, when in reality the interest rates are variable. A TTL estimate of 1 year today, might be reduced to 6 months tomorrow, if the cost of borrown rises dramatically.

## How to Claim

Users with an EUL distribution allocation can navigate to the rop right of the UI and click the 'Claim' button. That will open a dialogue box, showing a user's projected EUL distribution after the current epoch has completed. This will tick up second-by-second as a user accrues more time-weighted borrowing. The pending balance below that shows EUL tokens already distributed to the user but which remain in the distribution smart contract unclaimed. Users can click the Claim button in the bottom right of the dialogue to transfer those tokens to their wallet.&#x20;

![](<../../.gitbook/assets/claim2 (1).png>)
