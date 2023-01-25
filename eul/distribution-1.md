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

Epochs 1-96 cover the 4 year period from 21/03/2022 to 11/03/2026 during which Euler will progressively decentralise.

### Initial Implementation

**Borrowers** using the protocol during this period will be allocated EUL via a rolling merkle distribution. The amount distributed each epoch will follow a non-linear schedule (see below).

Within each market, borrowers will receive an EUL distribution proportional to their time-weighted borrowing on that market. The amount of EUL allocated to each market every epoch will be determined by EUL token holders (see [Gauges](https://app.gitbook.com/o/-MJloiaY-UMc3SjaxzA6/s/-MJlqpE4apPrZurt7BNr/\~/changes/8TZLu5aIjb41difegSzr/governance/gauges)).

Users will be able to claim their EUL governance tokens after an epoch has completed by using the 'Claim' button at [https://app.euler.finance/](https://app.euler.finance/).

### Updates&#x20;

#### eIP 24

The DAO voted to alter the initial EUL Distribution Programme. Beginning epoch 18, the DAO began allocating a fixed amount of 40,000 EUL each epoch to the [Gauges](https://app.gitbook.com/o/-MJloiaY-UMc3SjaxzA6/s/-MJlqpE4apPrZurt7BNr/\~/changes/8TZLu5aIjb41difegSzr/governance/gauges) to be voted on each epoch by existing EUL token holders, with an additional 15,000 EUL allocated evenly to lenders of USDC, USDT, and WETH for a trial period of 6 epochs.

### Schedule

The following table outlines the (approximate) dates and block numbers for previous and forthcoming epochs. Dates are approximate because the schedule is determined by the pace at which blocks are mined on the Ethereum network.

| Epoch | Approx Date | EUL Distribution | % Total Supply |
| ----- | ----------- | ---------------- | -------------- |
| 0     | 26/11/2022  | 271,828.18       | 1.00%          |
| 1     | 21/03/2022  | 36,915.69        | 1.14%          |
| 2     | 21/03/2022  | 37,673.39        | 1.27%          |
| 3     | 21/03/2022  | 38,531.30        | 1.42%          |
| 4     | 21/03/2022  | 39,501.78        | 1.56%          |
| 5     | 21/03/2022  | 40,598.43        | 1.71%          |
| 6     | 21/03/2022  | 41,836.14        | 1.86%          |
| 7     | 21/03/2022  | 43,231.14        | 2.02%          |
| 8     | 21/03/2022  | 44,800.97        | 2.19%          |
| 9     | 21/03/2022  | 46,564.39        | 2.36%          |
| 10    | 21/03/2022  | 48,541.27        | 2.54%          |
| 11    | 21/03/2022  | 50,752.38        | 2.73%          |
| 12    | 21/03/2022  | 53,219.03        | 2.92%          |
| 13    | 21/03/2022  | 55,962.62        | 3.13%          |
| 14    | 21/03/2022  | 59,004.03        | 3.34%          |
| 15    | 21/03/2022  | 62,362.78        | 3.57%          |
| 16    | 21/03/2022  | 66,056.03        | 3.82%          |
| 17    | 21/03/2022  | 70,097.30        | 4.07%          |
| 18    | 21/03/2022  | 55000            | 4.28%          |
| 19    | 21/03/2022  | 55000            | 4.48%          |
| 20    | 21/03/2022  | 55000            | 4.68%          |
| 21    | 21/03/2022  | 55000            | 4.88%          |
| 22    | 21/03/2022  | 55000            | 5.09%          |
| 23    | 21/03/2022  | 55000            | 5.29%          |
| 24    | 21/03/2022  | 40000            | 5.44%          |
| 25    | 21/03/2022  | 40000            | 5.58%          |
| 26    | 21/03/2022  | 40000            | 5.73%          |
| 27    | 21/03/2022  | 40000            | 5.88%          |
| 28    | 21/03/2022  | 40000            | 6.02%          |
| 29    | 21/03/2022  | 40000            | 6.17%          |
| 30    | 21/03/2022  | 40000            | 6.32%          |
| 31    | 21/03/2022  | 40000            | 6.47%          |
| 32    | 21/03/2022  | 40000            | 6.61%          |
| 33    | 21/03/2022  | 40000            | 6.76%          |
| 34    | 21/03/2022  | 40000            | 6.91%          |
| 35    | 21/03/2022  | 40000            | 7.05%          |
| 36    | 21/03/2022  | 40000            | 7.20%          |
| 37    | 21/03/2022  | 40000            | 7.35%          |
| 38    | 21/03/2022  | 40000            | 7.50%          |
| 39    | 21/03/2022  | 40000            | 7.64%          |
| 40    | 21/03/2022  | 40000            | 7.79%          |
| 41    | 21/03/2022  | 40000            | 7.94%          |
| 42    | 21/03/2022  | 40000            | 8.08%          |
| 43    | 21/03/2022  | 40000            | 8.23%          |
| 44    | 21/03/2022  | 40000            | 8.38%          |
| 45    | 21/03/2022  | 40000            | 8.53%          |
| 46    | 21/03/2022  | 40000            | 8.67%          |
| 47    | 21/03/2022  | 40000            | 8.82%          |
| 48    | 21/03/2022  | 40000            | 8.97%          |
| 49    | 21/03/2022  | 40000            | 9.11%          |
| 50    | 21/03/2022  | 40000            | 9.26%          |
| 51    | 21/03/2022  | 40000            | 9.41%          |
| 52    | 21/03/2022  | 40000            | 9.56%          |
| 53    | 21/03/2022  | 40000            | 9.70%          |
| 54    | 21/03/2022  | 40000            | 9.85%          |
| 55    | 21/03/2022  | 40000            | 10.00%         |
| 56    | 21/03/2022  | 40000            | 10.14%         |
| 57    | 21/03/2022  | 40000            | 10.29%         |
| 58    | 21/03/2022  | 40000            | 10.44%         |
| 59    | 21/03/2022  | 40000            | 10.59%         |
| 60    | 21/03/2022  | 40000            | 10.73%         |
| 61    | 21/03/2022  | 40000            | 10.88%         |
| 62    | 21/03/2022  | 40000            | 11.03%         |
| 63    | 21/03/2022  | 40000            | 11.17%         |
| 64    | 21/03/2022  | 40000            | 11.32%         |
| 65    | 21/03/2022  | 40000            | 11.47%         |
| 66    | 21/03/2022  | 40000            | 11.62%         |
| 67    | 21/03/2022  | 40000            | 11.76%         |
| 68    | 21/03/2022  | 40000            | 11.91%         |
| 69    | 21/03/2022  | 40000            | 12.06%         |
| 70    | 21/03/2022  | 40000            | 12.20%         |
| 71    | 21/03/2022  | 40000            | 12.35%         |
| 72    | 21/03/2022  | 40000            | 12.50%         |
| 73    | 21/03/2022  | 40000            | 12.65%         |
| 74    | 21/03/2022  | 40000            | 12.79%         |
| 75    | 21/03/2022  | 40000            | 12.94%         |
| 76    | 21/03/2022  | 40000            | 13.09%         |
| 77    | 21/03/2022  | 40000            | 13.23%         |
| 78    | 21/03/2022  | 40000            | 13.38%         |
| 79    | 21/03/2022  | 40000            | 13.53%         |
| 80    | 21/03/2022  | 40000            | 13.68%         |
| 81    | 21/03/2022  | 40000            | 13.82%         |
| 82    | 21/03/2022  | 40000            | 13.97%         |
| 83    | 21/03/2022  | 40000            | 14.12%         |
| 84    | 21/03/2022  | 40000            | 14.26%         |
| 85    | 21/03/2022  | 40000            | 14.41%         |
| 86    | 21/03/2022  | 40000            | 14.56%         |
| 87    | 21/03/2022  | 40000            | 14.71%         |
| 88    | 21/03/2022  | 40000            | 14.85%         |
| 89    | 21/03/2022  | 40000            | 15.00%         |
| 90    | 21/03/2022  | 40000            | 15.15%         |
| 91    | 21/03/2022  | 40000            | 15.29%         |
| 92    | 21/03/2022  | 40000            | 15.44%         |
| 93    | 21/03/2022  | 40000            | 15.59%         |
| 94    | 21/03/2022  | 40000            | 15.74%         |
| 95    | 21/03/2022  | 40000            | 15.88%         |
| 96    | 21/03/2022  | 40000            | 16.03%         |
