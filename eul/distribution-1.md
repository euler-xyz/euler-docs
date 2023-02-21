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

The following table outlines the (approximate) dates and block numbers for previous and forthcoming epochs. The % Total Supply is a cumulative sum. Dates are approximate because the schedule is determined by the pace at which blocks are mined on the Ethereum network.

| Epoch | Approx Date | EUL Distribution | % Total Supply |
| ----- | ----------- | ---------------- | -------------- |
| 0     | 21/03/2022  | 271,828.18       | 1.00%          |
| 1     | 04/04/2022  | 36,915.69        | 1.14%          |
| 2     | 18/04/2022  | 37,673.39        | 1.27%          |
| 3     | 02/05/2022  | 38,531.30        | 1.42%          |
| 4     | 16/05/2022  | 39,501.78        | 1.56%          |
| 5     | 30/05/2022  | 40,598.43        | 1.71%          |
| 6     | 13/06/2022  | 41,836.14        | 1.86%          |
| 7     | 27/06/2022  | 43,231.14        | 2.02%          |
| 8     | 11/07/2022  | 44,800.97        | 2.19%          |
| 9     | 25/07/2022  | 46,564.39        | 2.36%          |
| 10    | 08/08/2022  | 48,541.27        | 2.54%          |
| 11    | 22/08/2022  | 50,752.38        | 2.73%          |
| 12    | 05/09/2022  | 53,219.03        | 2.92%          |
| 13    | 19/09/2022  | 55,962.62        | 3.13%          |
| 14    | 03/10/2022  | 59,004.03        | 3.34%          |
| 15    | 17/10/2022  | 62,362.78        | 3.57%          |
| 16    | 31/10/2022  | 66,056.03        | 3.82%          |
| 17    | 14/11/2022  | 70,097.30        | 4.07%          |
| 18    | 28/11/2022  | 55000            | 4.28%          |
| 19    | 12/12/2022  | 55000            | 4.48%          |
| 20    | 26/12/2022  | 55000            | 4.68%          |
| 21    | 09/01/2023  | 55000            | 4.88%          |
| 22    | 23/01/2023  | 55000            | 5.09%          |
| 23    | 06/02/2023  | 55000            | 5.29%          |
| 24    | 20/02/2023  | 52000            | 5.48%          |
| 25    | 06/03/2023  | 52000            | 5.67%          |
| 26    | 20/03/2023  | 52000            | 5.86%          |
| 27    | 03/04/2023  | 52000            | 6.05%          |
| 28    | 17/04/2023  | 52000            | 6.24%          |
| 29    | 01/05/2023  | 52000            | 6.44%          |
| 30    | 15/05/2023  | 47000            | 6.61%          |
| 31    | 29/05/2023  | 47000            | 6.78%          |
| 32    | 12/06/2023  | 47000            | 6.95%          |
| 33    | 26/06/2023  | 47000            | 7.13%          |
| 34    | 10/07/2023  | 47000            | 7.30%          |
| 35    | 24/07/2023  | 47000            | 7.47%          |
| 36    | 07/08/2023  | 47000            | 7.65%          |
| 37    | 21/08/2023  | 47000            | 7.82%          |
| 38    | 04/09/2023  | 47000            | 7.99%          |
| 39    | 18/09/2023  | 47000            | 8.16%          |
| 40    | 02/10/2023  | 47000            | 8.34%          |
| 41    | 16/10/2023  | 47000            | 8.51%          |
| 42    | 30/10/2023  | 47000            | 8.68%          |
| 43    | 13/11/2023  | 47000            | 8.86%          |
| 44    | 27/11/2023  | 47000            | 9.03%          |
| 45    | 11/12/2023  | 47000            | 9.20%          |
| 46    | 25/12/2023  | 47000            | 9.38%          |
| 47    | 08/01/2024  | 47000            | 9.55%          |
| 48    | 22/01/2024  | 47000            | 9.72%          |
| 49    | 05/02/2024  | 47000            | 9.89%          |
| 50    | 19/02/2024  | 47000            | 10.07%         |
| 51    | 04/03/2024  | 47000            | 10.24%         |
| 52    | 18/03/2024  | 47000            | 10.41%         |
| 53    | 01/04/2024  | 47000            | 10.59%         |
| 54    | 15/04/2024  | 47000            | 10.76%         |
| 55    | 29/04/2024  | 47000            | 10.93%         |
| 56    | 13/05/2024  | 47000            | 11.10%         |
| 57    | 27/05/2024  | 47000            | 11.28%         |
| 58    | 10/06/2024  | 47000            | 11.45%         |
| 59    | 24/06/2024  | 47000            | 11.62%         |
| 60    | 08/07/2024  | 47000            | 11.80%         |
| 61    | 22/07/2024  | 47000            | 11.97%         |
| 62    | 05/08/2024  | 47000            | 12.14%         |
| 63    | 19/08/2024  | 47000            | 12.31%         |
| 64    | 02/09/2024  | 47000            | 12.49%         |
| 65    | 16/09/2024  | 47000            | 12.66%         |
| 66    | 30/09/2024  | 47000            | 12.83%         |
| 67    | 14/10/2024  | 47000            | 13.01%         |
| 68    | 28/10/2024  | 47000            | 13.18%         |
| 69    | 11/11/2024  | 47000            | 13.35%         |
| 70    | 25/11/2024  | 47000            | 13.53%         |
| 71    | 09/12/2024  | 47000            | 13.70%         |
| 72    | 23/12/2024  | 47000            | 13.87%         |
| 73    | 06/01/2025  | 47000            | 14.04%         |
| 74    | 20/01/2025  | 47000            | 14.22%         |
| 75    | 03/02/2025  | 47000            | 14.39%         |
| 76    | 17/02/2025  | 47000            | 14.56%         |
| 77    | 03/03/2025  | 47000            | 14.74%         |
| 78    | 17/03/2025  | 47000            | 14.91%         |
| 79    | 31/03/2025  | 47000            | 15.08%         |
| 80    | 14/04/2025  | 47000            | 15.25%         |
| 81    | 28/04/2025  | 47000            | 15.43%         |
| 82    | 12/05/2025  | 47000            | 15.60%         |
| 83    | 26/05/2025  | 47000            | 15.77%         |
| 84    | 09/06/2025  | 47000            | 15.95%         |
| 85    | 23/06/2025  | 47000            | 16.12%         |
| 86    | 07/07/2025  | 47000            | 16.29%         |
| 87    | 21/07/2025  | 47000            | 16.46%         |
| 88    | 04/08/2025  | 47000            | 16.64%         |
| 89    | 18/08/2025  | 47000            | 16.81%         |
| 90    | 01/09/2025  | 47000            | 16.98%         |
| 91    | 15/09/2025  | 47000            | 17.16%         |
| 92    | 29/09/2025  | 47000            | 17.33%         |
| 93    | 13/10/2025  | 47000            | 17.50%         |
| 94    | 27/10/2025  | 47000            | 17.67%         |
| 95    | 10/11/2025  | 47000            | 17.85%         |
| 96    | 24/11/2025  | 47000            | 18.02%         |