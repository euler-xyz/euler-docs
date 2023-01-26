---
description: >-
  Learn more about how EUL is distributed to protocol users to decentralise
  governance
---

# Distribution

## Introduction

In order to progressively decentralise governance of the Euler Protocol, EUL will be distibuted to protocol users over a period of (at least) 4 years. See how much EUL is being distributed today [here](https://app.euler.finance/gauges).&#x20;

The distribution programme is broken down into cycles called [epochs](distribution-1.md). Every epoch EUL gets distributed to borrowers on a subset of community-selected markets. The markets eligible for a distribution are determined by an EUL staking [gauge ](gauges.md)system.

## How it Works

The amount of EUL each borrower receives is proportional to the time-weighted amount of debt they held of an asset within the epoch. For example, if 50 EUL are to be distributed to the DAI market in epoch 3, and if Alice borrows 10 DAI for 1 day, and Bob borrows 5 DAI for 2 days, then at the end of the epoch, and after the merkle-root update (typically takes a few hours), they will both be able to claim an equal share of 25 EUL.

## How to Claim

Users with an EUL distribution allocation can navigate to the rop right of the UI and click the 'Claim' button. That will open a dialogue box, showing a user's projected EUL distribution after the current epoch has completed. This will tick up second-by-second as a user accrues more time-weighted borrowing. The pending balance below that shows EUL tokens already distributed to the user but which remain in the distribution smart contract unclaimed. Users can click the Claim button in the bottom right of the dialogue to transfer those tokens to their wallet.

![](<../../.gitbook/assets/claim2 (1).png>)

