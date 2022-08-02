---
description: Learn more about the phases of the EUL Distribution programme
---

# Epochs

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

### Implementation

**Borrowers** using the protocol during this period will be allocated a share of 25% of the total supply of EUL via a rolling merkle distribution. The amount distributed each epoch will follow a non-linear schedule (see below).

Within each market, borrowers will receive an EUL distribution proportional to their time-weighted borrowing on that market. The amount of EUL allocated to each market every epoch will be determined by EUL token holders (see [Gauges](https://app.gitbook.com/o/-MJloiaY-UMc3SjaxzA6/s/-MJlqpE4apPrZurt7BNr/\~/changes/8TZLu5aIjb41difegSzr/governance/gauges)).

Users will be able to claim their EUL governance tokens after an epoch has completed by using the 'Claim' button at [https://app.euler.finance/](https://app.euler.finance/).

## Schedule

The amount of EUL distributed in each epoch has been determined in advance according to a non-linear schedule (see below). The schedule tries to match increasing protocol user numbers after launch with a concomitant increase in the EUL distribution, which should help to decentralise supply of the token rather than allocating a disproportionate amount to early users.

The following table outlines the (approximate) dates and block numbers for previous and forthcoming epochs. Dates are approximate because the schedule is determined by the pace at which blocks are mined on the Ethereum network.

| Epoch |    Block | Approx Date |   EUL Dist | % Total Supply |
| ----: | -------: | ----------: | ---------: | -------------: |
|     0 | 13687582 |  26/11/2021 | 271,828.18 |          1.00% |
|     1 | 14430000 |  21/03/2022 |  36,915.69 |          0.14% |
|     2 | 14530000 |  05/04/2022 |  37,673.39 |          0.14% |
|     3 | 14630000 |  20/04/2022 |  38,531.30 |          0.14% |
|     4 | 14730000 |  05/05/2022 |  39,501.78 |          0.15% |
|     5 | 14830000 |  21/05/2022 |  40,598.43 |          0.15% |
|     6 | 14930000 |  05/06/2022 |  41,836.14 |          0.15% |
|     7 | 15030000 |  20/06/2022 |  43,231.14 |          0.16% |
|     8 | 15130000 |  05/07/2022 |  44,800.97 |          0.16% |
|     9 | 15230000 |  21/07/2022 |  46,564.39 |          0.17% |
|    10 | 15330000 |  05/08/2022 |  48,541.27 |          0.18% |
|    11 | 15430000 |  20/08/2022 |  50,752.38 |          0.19% |
|    12 | 15530000 |  05/09/2022 |  53,219.03 |          0.20% |
|    13 | 15630000 |  20/09/2022 |  55,962.62 |          0.21% |
|    14 | 15730000 |  05/10/2022 |  59,004.03 |          0.22% |
|    15 | 15830000 |  20/10/2022 |  62,362.78 |          0.23% |
|    16 | 15930000 |  05/11/2022 |  66,056.03 |          0.24% |
|    17 | 16030000 |  20/11/2022 |  70,097.30 |          0.26% |
|    18 | 16130000 |  05/12/2022 |  74,494.98 |          0.27% |
|    19 | 16230000 |  21/12/2022 |  79,250.60 |          0.29% |
|    20 | 16330000 |  05/01/2023 |  84,356.92 |          0.31% |
|    21 | 16430000 |  20/01/2023 |  89,795.88 |          0.33% |
|    22 | 16530000 |  04/02/2023 |  95,536.50 |          0.35% |
|    23 | 16630000 |  20/02/2023 | 101,533.06 |          0.37% |
|    24 | 16730000 |  07/03/2023 | 107,723.40 |          0.40% |
|    25 | 16830000 |  22/03/2023 | 114,028.05 |          0.42% |
|    26 | 16930000 |  06/04/2023 | 120,350.07 |          0.44% |
|    27 | 17030000 |  22/04/2023 | 126,576.02 |          0.47% |
|    28 | 17130000 |  07/05/2023 | 132,578.40 |          0.49% |
|    29 | 17230000 |  22/05/2023 | 138,219.39 |          0.51% |
|    30 | 17330000 |  07/06/2023 | 143,356.23 |          0.53% |
|    31 | 17430000 |  22/06/2023 | 147,847.72 |          0.54% |
|    32 | 17530000 |  07/07/2023 | 151,561.68 |          0.56% |
|    33 | 17630000 |  22/07/2023 | 154,382.67 |          0.57% |
|    34 | 17730000 |  07/08/2023 | 156,219.30 |          0.57% |
|    35 | 17830000 |  22/08/2023 | 157,010.35 |          0.58% |
|    36 | 17930000 |  06/09/2023 | 156,729.02 |          0.58% |
|    37 | 18030000 |  22/09/2023 | 155,384.87 |          0.57% |
|    38 | 18130000 |  07/10/2023 | 153,023.12 |          0.56% |
|    39 | 18230000 |  22/10/2023 | 149,721.46 |          0.55% |
|    40 | 18330000 |  06/11/2023 | 145,584.72 |          0.54% |
|    41 | 18430000 |  22/11/2023 | 140,738.06 |          0.52% |
|    42 | 18530000 |  07/12/2023 | 135,319.35 |          0.50% |
|    43 | 18630000 |  22/12/2023 | 129,471.49 |          0.48% |
|    44 | 18730000 |  06/01/2024 | 123,335.40 |          0.45% |
|    45 | 18830000 |  22/01/2024 | 117,044.06 |          0.43% |
|    46 | 18930000 |  06/02/2024 | 110,718.00 |          0.41% |
|    47 | 19030000 |  21/02/2024 | 104,462.21 |          0.38% |
|    48 | 19130000 |  08/03/2024 |  98,364.54 |          0.36% |
|    49 | 19230000 |  23/03/2024 |  92,495.32 |          0.34% |
|    50 | 19330000 |  07/04/2024 |  86,907.93 |          0.32% |
|    51 | 19430000 |  22/04/2024 |  81,640.16 |          0.30% |
|    52 | 19530000 |  08/05/2024 |  76,715.96 |          0.28% |
|    53 | 19630000 |  23/05/2024 |  72,147.47 |          0.27% |
|    54 | 19730000 |  07/06/2024 |  67,937.09 |          0.25% |
|    55 | 19830000 |  23/06/2024 |  64,079.46 |          0.24% |
|    56 | 19930000 |  08/07/2024 |  60,563.32 |          0.22% |
|    57 | 20030000 |  23/07/2024 |  57,373.05 |          0.21% |
|    58 | 20130000 |  07/08/2024 |  54,490.13 |          0.20% |
|    59 | 20230000 |  23/08/2024 |  51,894.21 |          0.19% |
|    60 | 20330000 |  07/09/2024 |  49,564.05 |          0.18% |
|    61 | 20430000 |  22/09/2024 |  47,478.22 |          0.17% |
|    62 | 20530000 |  07/10/2024 |  45,615.66 |          0.17% |
|    63 | 20630000 |  23/10/2024 |  43,956.02 |          0.16% |
|    64 | 20730000 |  07/11/2024 |  42,480.00 |          0.16% |
|    65 | 20830000 |  22/11/2024 |  41,169.47 |          0.15% |
|    66 | 20930000 |  08/12/2024 |  40,007.56 |          0.15% |
|    67 | 21030000 |  23/12/2024 |  38,978.76 |          0.14% |
|    68 | 21130000 |  07/01/2025 |  38,068.84 |          0.14% |
|    69 | 21230000 |  22/01/2025 |  37,264.86 |          0.14% |
|    70 | 21330000 |  07/02/2025 |  36,555.12 |          0.13% |
|    71 | 21430000 |  22/02/2025 |  35,929.04 |          0.13% |
|    72 | 21530000 |  09/03/2025 |  35,377.14 |          0.13% |
|    73 | 21630000 |  25/03/2025 |  34,890.91 |          0.13% |
|    74 | 21730000 |  09/04/2025 |  34,462.77 |          0.13% |
|    75 | 21830000 |  24/04/2025 |  34,085.94 |          0.13% |
|    76 | 21930000 |  09/05/2025 |  33,754.42 |          0.12% |
|    77 | 22030000 |  25/05/2025 |  33,462.85 |          0.12% |
|    78 | 22130000 |  09/06/2025 |  33,206.50 |          0.12% |
|    79 | 22230000 |  24/06/2025 |  32,981.18 |          0.12% |
|    80 | 22330000 |  09/07/2025 |  32,783.18 |          0.12% |
|    81 | 22430000 |  25/07/2025 |  32,609.22 |          0.12% |
|    82 | 22530000 |  09/08/2025 |  32,456.41 |          0.12% |
|    83 | 22630000 |  24/08/2025 |  32,322.20 |          0.12% |
|    84 | 22730000 |  09/09/2025 |  32,204.35 |          0.12% |
|    85 | 22830000 |  24/09/2025 |  32,100.87 |          0.12% |
|    86 | 22930000 |  09/10/2025 |  32,010.02 |          0.12% |
|    87 | 23030000 |  24/10/2025 |  31,930.27 |          0.12% |
|    88 | 23130000 |  09/11/2025 |  31,860.26 |          0.12% |
|    89 | 23230000 |  24/11/2025 |  31,798.82 |          0.12% |
|    90 | 23330000 |  09/12/2025 |  31,744.89 |          0.12% |
|    91 | 23430000 |  25/12/2025 |  31,697.56 |          0.12% |
|    92 | 23530000 |  09/01/2026 |  31,656.03 |          0.12% |
|    93 | 23630000 |  24/01/2026 |  31,619.58 |          0.12% |
|    94 | 23730000 |  08/02/2026 |  31,587.60 |          0.12% |
|    95 | 23830000 |  24/02/2026 |  31,559.53 |          0.12% |
|    96 | 23930000 |  11/03/2026 |  17,864.18 |          0.07% |
