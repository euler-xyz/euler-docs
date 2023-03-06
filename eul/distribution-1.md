---
description: Learn more about the phases of the EUL Distribution Programme
---

# Epochs

## Introduction

The EUL Distribution Programme has two phases. Epoch 0, in which governance tokens were distributed to early protocol users retroactively; and Epoch 1-96, in which governance tokens are distributed on an ongoing basis to active users of the protocol.

## Epoch 0

Epoch 0 covers the 3 month period from 26/11/2021 to 21/03/2022 during which Euler protocol was in a soft-launch mode. Users were experimenting with the protocol in a risk-minimised manner.

### Implementation

**Lenders** and **borrowers** using the protocol during this period were allocated a share of 1% of the total supply of EUL as a one-off retroactive distribution.

The distribution took place as follows:

1. A snapshot of all users on the protocol was taken at block 14,430,000.
2. A total of 271,828 EUL (1% of the total supply) was distributed to anyone interacting with the protocol upto that point.
3. The distribution amount per address was calculated as follows:
   * 2/3 of the issuance was distributed proportionally based on the time-weighted\* average USD value of the deposits and borrows in the mentioned time frame.
   * 1/3 of the total issuance is distributed evenly amongst all the unique addresses that interacted with the protocol in the mentioned time frame.

_\*For simplicity, the accrued interest on deposits and borrows was neglected._

In conclusion, 3407 unique addresses received at least 26.59 EUL tokens plus an individual amount proportional to the time-weighted average USD value of their deposits and borrows. See [here](https://docs.google.com/spreadsheets/d/1jTECkKiMDMvj1UdaU0AEFfhW8IN0SiBfkNFYpTdWIfo/edit#gid=0) for the final allocations.

## Epochs 1-96

Epochs 1-96 cover the period from 21/03/2022 to 17/12/2025 during which Euler will progressively decentralise.

### Initial Implementation

**Borrowers** using the protocol during this period will be allocated EUL via a rolling merkle distribution. The amount distributed each epoch will follow a non-linear schedule (see below).

Within each market, borrowers will receive an EUL distribution proportional to their time-weighted borrowing on that market. The amount of EUL allocated to each market every epoch will be determined by EUL token holders (see [Gauges](https://app.gitbook.com/o/-MJloiaY-UMc3SjaxzA6/s/-MJlqpE4apPrZurt7BNr/\~/changes/8TZLu5aIjb41difegSzr/governance/gauges)).

Users will be able to claim their EUL governance tokens after an epoch has completed by using the 'Claim' button at [https://app.euler.finance/](https://app.euler.finance/).

### Updates&#x20;

#### [eIP 24](https://snapshot.org/#/eulerdao.eth/proposal/0x7e65ffa930507d9116ebc83663000ade6ff93fc452f437a3e95d755ccc324f93)

The DAO voted to alter the initial EUL Distribution Programme. Beginning epoch 18, the DAO began allocating a fixed amount of 40,000 EUL each epoch to the [Gauges](https://app.gitbook.com/o/-MJloiaY-UMc3SjaxzA6/s/-MJlqpE4apPrZurt7BNr/\~/changes/8TZLu5aIjb41difegSzr/governance/gauges) to be voted on each epoch by existing EUL token holders, with an additional 15,000 EUL allocated evenly to lenders of USDC, USDT, and WETH for a trial period of 6 epochs.

#### [eIP29](https://snapshot.org/#/eulerdao.eth/proposal/0x8f046317b789af0de687334356a63005c2e213beb446ff620e43e5f356020c3e)

Creation of an Euler boosted USDC/DAI/USDT pool that is allocated 5,000 EUL as voting incentives every two weeks. This would run for a trial period of three months.

#### [eIP51](https://snapshot.org/#/eulerdao.eth/proposal/0x551f9e6f3fba50a0fc2c69e361f7a81979189aa7f0ed923a1873bd578896942b)

Proposal to change distribution as follows:

* 9,000 EUL per epoch to stakers of WETH market.
* 5,000 EUL per epoch to stakers of USDC market.
* 1,000 EUL per epoch to stakers of USDT market.
* 8,000 EUL per epoch via gauges to borrowers on each of USDC, WETH, and WStETH
* 8,000 EUL per epoch shared proportionally among assets with Chainlink oracle

### Schedule

The following table outlines the block numbers for previous and forthcoming epochs. 

| Epoch | Block Number   | EUL Distribution | 
| ----- | -------------- | ---------------- | 
| 0     | 14,430,000     | 271,828.18       | 
| 1     | 14,530,000     | 36,915.69        | 
| 2     | 14,630,000     | 37,673.39        | 
| 3     | 14,730,000     | 38,531.30        | 
| 4     | 14,830,000     | 39,501.78        | 
| 5     | 14,930,000     | 40,598.43        | 
| 6     | 15,030,000     | 41,836.14        | 
| 7     | 15,130,000     | 43,231.14        | 
| 8     | 15,230,000     | 44,800.97        | 
| 9     | 15,330,000     | 46,564.39        | 
| 10    | 15,430,000     | 48,541.27        | 
| 11    | 15,530,000     | 50,752.38        | 
| 12    | 15,630,000     | 53,219.03        | 
| 13    | 15,730,000     | 55,962.62        | 
| 14    | 15,830,000     | 59,004.03        | 
| 15    | 15,930,000     | 62,362.78        | 
| 16    | 16,030,000     | 66,056.03        | 
| 17    | 16,130,000     | 70,097.30        | 
| 18    | 16,230,000     | eIP24            | 
| 19    | 16,330,000     | 55000            | 
| 20    | 16,430,000     | 55000            | 
| 21    | 16,530,000     | 55000            | 
| 22    | 16,630,000     | 55000            | 
| 23    | 16,730,000     | 55000            | 
| 24    | 16,830,000     | eIP29 & eIP51    | 
| 25    | 16,930,000     | 52000            | 
| 26    | 17,030,000     | 52000            | 
| 27    | 17,130,000     | 52000            | 
| 28    | 17,230,000     | 52000            | 
| 29    | 17,330,000     | 47000            | 
| 30    | 17,430,000     | 47000            | 
| 31    | 17,530,000     | 47000            | 
| 32    | 17,630,000     | 47000            | 
| 33    | 17,730,000     | 47000            | 
| 34    | 17,830,000     | 47000            | 
| 35    | 17,930,000     | 47000            | 
| 36    | 18,030,000     | 47000            | 
| 37    | 18,130,000     | 47000            | 
| 38    | 18,230,000     | 47000            | 
| 39    | 18,330,000     | 47000            | 
| 40    | 18,430,000     | 47000            | 
| 41    | 18,530,000     | 47000            | 
| 42    | 18,630,000     | 47000            | 
| 43    | 18,730,000     | 47000            | 
| 44    | 18,830,000     | 47000            | 
| 45    | 18,930,000     | 47000            | 
| 46    | 19,030,000     | 47000            | 
| 47    | 19,130,000     | 47000            | 
| 48    | 19,230,000     | 47000            | 
| 49    | 19,330,000     | 47000            | 
| 50    | 19,430,000     | 47000            | 
| 51    | 19,530,000     | 47000            | 
| 52    | 19,630,000     | 47000            | 
| 53    | 19,730,000     | 47000            | 
| 54    | 19,830,000     | 47000            | 
| 55    | 19,930,000     | 47000            | 
| 56    | 20,030,000     | 47000            | 
| 57    | 20,130,000     | 47000            | 
| 58    | 20,230,000     | 47000            | 
| 59    | 20,330,000     | 47000            | 
| 60    | 20,430,000     | 47000            | 
| 61    | 20,530,000     | 47000            | 
| 62    | 20,630,000     | 47000            | 
| 63    | 20,730,000     | 47000            | 
| 64    | 20,830,000     | 47000            | 
| 65    | 20,930,000     | 47000            | 
| 66    | 21,030,000     | 47000            | 
| 67    | 21,130,000     | 47000            | 
| 68    | 21,230,000     | 47000            | 
| 69    | 21,330,000     | 47000            | 
| 70    | 21,430,000     | 47000            | 
| 71    | 21,530,000     | 47000            | 
| 72    | 21,630,000     | 47000            | 
| 73    | 21,730,000     | 47000            | 
| 74    | 21,830,000     | 47000            | 
| 75    | 21,930,000     | 47000            | 
| 76    | 22,030,000     | 47000            | 
| 77    | 22,130,000     | 47000            | 
| 78    | 22,230,000     | 47000            | 
| 79    | 22,330,000     | 47000            | 
| 80    | 22,430,000     | 47000            | 
| 81    | 22,530,000     | 47000            | 
| 82    | 22,630,000     | 47000            | 
| 83    | 22,730,000     | 47000            | 
| 84    | 22,830,000     | 47000            | 
| 85    | 22,930,000     | 47000            | 
| 86    | 23,030,000     | 47000            | 
| 87    | 23,130,000     | 47000            | 
| 88    | 23,230,000     | 47000            | 
| 89    | 23,330,000     | 47000            | 
| 90    | 23,430,000     | 47000            | 
| 91    | 23,530,000     | 47000            | 
| 92    | 23,630,000     | 47000            | 
| 93    | 23,730,000     | 47000            | 
| 94    | 23,830,000     | 47000            | 
| 95    | 23,930,000     | 47000            | 
| 96    | 24,030,000     | 47000            | 
