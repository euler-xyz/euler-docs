---
description: Subgraph
---

# Subgraph

## Links

- Querying the subgraph: https://thegraph.com/docs/en/developer/query-the-graph/

### Mainnet

- The Graph: https://thegraph.com/hosted-service/subgraph/euler-xyz/euler-mainnet
- API: https://api.thegraph.com/subgraphs/name/euler-xyz/euler-mainnet

## About

- All amounts have a fixed decimal precision of 1e18.
- Are timestamps are represented as [unix timestamps](https://en.wikipedia.org/wiki/Unix_time).
- USD and ETH exchange rates of all assets are pulled through Euler directly

## Entities

### Asset

Contains information about all Euler markets, pulled from EulerGeneralView contract.

```GraphQL
type Asset @entity {
  "asset_address"
  id: ID!
  "Block hash at which asset was created"
  blockHash: Bytes!
  "Block number at which asset was created"
  blockNumber: Int!
  "Timestamp at which asset was created"
  timestamp: Int!
  "Block hash at which asset was last updated"
  updatedBlockHash: Bytes!
  "Block number at which asset was last updated"
  updatedBlockNumber: Int!
  "Timestamp at which asset was last updated"
  updatedTimestamp: Int!
  "Tx hash at which asset was created"
  transactionHash: Bytes!
  "Tx origin at which asset was created"
  transactionOrigin: Bytes!
  dTokenAddress: Bytes!
  eTokenAddress: Bytes!
  pTokenAddress: Bytes!
  symbol: String!
  name: String!
  decimals: BigInt!
  totalSupply: BigInt!
  totalBalances: BigInt!
  totalBalancesUsd: BigInt!
  totalBalancesEth: BigInt!
  totalBorrows: BigInt!
  totalBorrowsUsd: BigInt!
  totalBorrowsEth: BigInt!
  reserveBalance: BigInt!
  reserveBalanceEth: BigInt!
  reserveBalanceUsd: BigInt!
  reserveFee: BigInt!
  borrowAPY: BigInt!
  supplyAPY: BigInt!
  twap: BigInt!
  twapUsd: BigDecimal!
  "Deprecated in favor of twapUsd. Do not use."
  twapPrice: BigDecimal!
  twapPeriod: BigInt!
  currPrice: BigInt!
  currPriceUsd: BigInt!
  pricingType: Int!
  pricingParameters: BigInt!
  pricingForwarded: Bytes!
  collateralValue: BigInt!
  liabilityValue: BigInt!
  numBorrows: BigInt!
  borrowIsolated: Boolean!
  poolSize: BigInt!
  interestRate: BigInt!
  interestAccumulator: BigInt!
  config: AssetConfig
}
```

Sometimes, gouvernance will manually set asset configuration, it is displayed in the AssetConfig entity. If an asset has a null AssetConfig, it is safe to assume that it was never explicitly set and is isolated.

For further tier information, refer to [Tier Methodology](../risk-framework/tiers.md).

`borrowFactor` and `collateralFactor` can be transformed in a decimal fraction by dividing by `4e9`.

```GraphQL
type AssetConfig @entity {
  "asset_address"
  id: ID!
  twapWindowInSeconds: Int!
  borrowFactor: BigInt!
  borrowIsolated: Boolean!
  collateralFactor: BigInt!
  tier: String!
}
```

### Account

Account that transacts on Euler. Could be a sub-account or a main account.

```GraphQL
type Account @entity {
  "account_address"
  id: ID!
  createdTimestamp: Int!
  topLevelAccount: TopLevelAccount!
  balances: [Balance!]
  balanceChanges: [BalanceChange!]
  balanceChangesCount: Int!
}
```

A Balance represents the current amount of each assets held by an account.

```GraphQL
type Balance @entity {
  "account_address:underlying"
  id: ID!
  account: Account!
  amount: BigInt!
  asset: Asset!
}
```

A BalanceChange is a transaction within the platform. `type` can be one of the following values: 

 - borrow
 - deposit
 - withdraw
 - repay

```GraphQL
type BalanceChange @entity {
  "transaction_hash:event_log_index"
  id: ID!
  transactionHash: Bytes!
  type: String!
  account: Account!
  topLevelAccount: TopLevelAccount!
  amount: BigInt!
  amountUsd: BigDecimal!
  timestamp: Int!
  asset: Asset!
```

### TopLevelAccount

Aggregate of the sub-accounts associated with a wallet.
TopLevelAccount id corresponds to main sub-account id.

```GraphQL
type TopLevelAccount @entity {
  "account_address"
  id: ID!
  createdTimestamp: Int!
  accounts: [Account!]
  balances: [TopLevelAccountBalance!]
  balanceChanges: [BalanceChange!]
  balanceChangesCount: Int!
}
```

```GraphQL
type TopLevelAccountBalance @entity {
  "top_level_account_address:underlying"
  id: ID!
  topLevelAccount: TopLevelAccount!
  amount: BigInt!
  asset: Asset!
}
```

### EulerMarketStore

Contains list of all active markets on Euler.

```GraphQL
type EulerMarketStore @entity {
  id: ID!
  markets: [Asset!]
}
```

### EulerOverview

Aggregated metrics for all markets as a whole.

```GraphQL
type EulerOverview @entity {
  id: ID!
  reserveBalanceUsd: BigInt!
  reserveBalanceEth: BigInt!
  totalBalancesUsd: BigInt!
  totalBalancesEth: BigInt!
  totalBorrowsUsd: BigInt!
  totalBorrowsEth: BigInt!
}
```

### Liquidation

Contains all liquidation transactions.

`liquidator` and `violator` fields correspond to account addresses.

```GraphQL
type Liquidation @entity {
  "transaction_hash:event_log_index"
  id: ID!
  timestamp: Int!
  transactionHash: Bytes!
  liquidator: Bytes!
  violator: Bytes!
  asset: Asset!
  collateralAsset: Asset!
  repay: BigInt!
  repayUsd: BigDecimal!
  harvest: BigInt!
  yieldUsd: BigDecimal!
  healthScore: BigInt!
  discount: BigInt!
  baseDiscount: BigInt!
}
```

### Governance

GovConvertReserve and GovSetReserveFee contain all on-chain information about governance.

```GraphQL
type GovConvertReserve @entity {
  "transaction_hash:event_log_index"
  id: ID!
  timestamp: Int!
  blockNumber: Int!
  transactionHash: Bytes!
  amount: BigInt!
  amountUsd: BigDecimal!
  asset: Asset!
  recipient: Bytes!
}
```

```GraphQL
type GovSetReserveFee @entity {
  "transaction_hash:event_log_index"
  id: ID!
  timestamp: Int!
  blockNumber: Int!
  transactionHash: Bytes!
  reserveFee: Int!
  asset: Asset!
}
```

### Hourly/Daily/MonthlyAssetSnapshot
Snapshot of Asset entity at the end of every hour, day and month.

Useful for querying historical data on markets.

```GraphQL
type HourlyAssetSnapshot @entity {
  "start_of_hour_timestamp:asset_address"
  id: ID!
  asset: Asset!
  "Block number at which snapshot was created"
  blockHash: Bytes!
  "Block hash at which snapshot was created"
  blockNumber: Int!
  "Timestamp at which snapshot was created"
  timestamp: Int!
  "Tx hash at which asset was created"
  transactionHash: Bytes!
  "Tx origin at which asset was created"
  transactionOrigin: Bytes!
  totalSupply: BigInt!
  totalBalances: BigInt!
  totalBalancesUsd: BigInt!
  totalBalancesEth: BigInt!
  totalBorrows: BigInt!
  totalBorrowsUsd: BigInt!
  totalBorrowsEth: BigInt!
  reserveBalance: BigInt!
  reserveBalanceEth: BigInt!
  reserveBalanceUsd: BigInt!
  reserveFee: BigInt!
  borrowAPY: BigInt!
  supplyAPY: BigInt!
  twap: BigInt!
  twapUsd: BigDecimal!
  twapPeriod: BigInt!
  currPrice: BigInt!
  currPriceUsd: BigInt!
  pricingType: Int!
  pricingParameters: BigInt!
  pricingForwarded: Bytes!
  collateralValue: BigInt!
  liabilityValue: BigInt!
  numBorrows: BigInt!
  borrowIsolated: Boolean!
  poolSize: BigInt!
  interestAccumulator: BigInt!
  interestRate: BigInt!
}
```

### Hourly/Daily/MonthlyAssetStatus

> This entity has been deprecated in favor of Hourly/Daily/MonthlyAssetSnapshot

Aggregated metrics of a specific market over hourly, daily and monthly time period.

```GraphQL
type HourlyAssetStatus @entity {
  "start_of_hour_timestamp:asset_address"
  id: ID!
  timestamp: Int!
  totalBalances: BigInt!
  totalBorrows: BigInt!
  reserveBalance: BigInt!
  poolSize: BigInt!
  interestAccumulator: BigInt!
  interestRate: BigInt!
  twapPrice: BigDecimal!
  twapUsd: BigDecimal!
  asset: Asset!
}
```

### Hourly/Daily/MonthlyRepay

Aggregated metrics for repay transactions over hourly, daily and monthly time period.

```GraphQL
type HourlyRepay @entity {
  "start_of_hour_timestamp"
  id: ID!
  timestamp: Int!
  count: Int!
  totalAmount: BigInt!
  totalUsdAmount: BigDecimal!
}
```

### Hourly/Daily/MonthlyDeposit

Aggregated metrics for deposits over hourly, daily and monthly time period.

```GraphQL
type HourlyDeposit @entity {
  "start_of_hour_timestamp"
  id: ID!
  timestamp: Int!
  count: Int!
  totalAmount: BigInt!
  totalUsdAmount: BigDecimal!
}
```

### Hourly/Daily/MonthlyWithdraw

Aggregated metrics for withdrawals over hourly, daily and monthly time period.

```GraphQL
type HourlyWithdraw @entity {
  "start_of_hour_timestamp"
  id: ID!
  timestamp: Int!
  count: Int!
  totalAmount: BigInt!
  totalUsdAmount: BigDecimal!
}
```

### Hourly/Daily/MonthlyBorrow

Aggregated for borrow transactions over hourly, daily and monthly time period.

```GraphQL
type HourlyBorrow @entity {
  "start_of_hour_timestamp"
  id: ID!
  timestamp: Int!
  count: Int!
  totalAmount: BigInt!
  totalUsdAmount: BigDecimal!
}
```

## Querying time based aggregates

Every entity that has `hourly`, `daily` or `monthly` in its name can be queried by its ID. The documentation for those is located within each entity. Below lies the rules used to create the required timestamps.

| Parameter                | Value                                                      |
| :----------------------- | :--------------------------------------------------------- |
| start_of_hour_timestamp  | unix timestamp at minute 0                                 |
| start_of_day_timestamp   | unix timestamp at hour 0, minute 0                         |
| start_of_month_timestamp | unix timestamp at first day of the month, hour 0, minute 0 |

## Examples

### Fetch the 5 biggest markets by total borrowed in USD

```GraphQL
{
  assets(first: 5, orderBy: totalBorrowsUsd, orderDirection: desc) {
    symbol
    totalBorrows
    totalBorrowsUsd
    currPriceUsd
  }
}
```

### Fetch historical interest rate, supply and borrow balances of a given market

```GraphQL
{
  hourlyAssetSnapshots(where: {asset: "0x03ab458634910aad20ef5f1c8ee96f1d6ac54919"}, orderBy: timestamp, orderDirection: desc, first: 1000) {
    id
    supplyAPY
    borrowAPY
    totalBorrowsUsd
    totalBalancesUsd
  }
}
```

### Get the current balances of an account

```GraphQL
{
  account(id: "0x0000000002732779240fe05873611dc4203dfb71") {
    balances {
      amount
      asset {
        symbol
      }
    }
  }
}
```

### Get the transaction history of an account

```GraphQL
{
  account(id: "0x0000000002732779240fe05873611dc4203dfb71") {
    balanceChanges {
      type
      timestamp
      amount
      amountUsd
      asset {
        symbol
      }
    }
  }
}
```

### Get USD amount borrowed on February 10th 2022

First we need to create our ID using the parameters define in the [Querying time based aggregates](#querying-time-based-aggregates) section. In this case, February 10th 2020 = 1644451200.

```GraphQL
{
  dailyBorrow(id: "1644451200") {
  	count
    totalUsdAmount
  }
}
```

### Last 30 days of deposit amounts

```GraphQL
{
  dailyDeposits(first: 30, orderBy: timestamp, orderDirection: desc) {
    id
    timestamp
    totalUsdAmount
  }
}
```

### All transactions between February 1st 2022 and February 3rd 2022 

```GraphQL
{
  balanceChanges(orderBy: timestamp, orderDirection: asc, where: {timestamp_gte: 1643673600, timestamp_lte: 1643932799}) {
    timestamp
    type
    amount
    amountUsd
  	account {
      id
    }
    asset {
      symbol
    }
  }
}
```

## Querying time based aggregates

Every entity that has `hourly`, `daily` or `monthly` in its name can be queried by its ID. The documentation for those is located within each entity. Below lies the rules used to create the required timestamps.

| Parameter                | Value                                                      |
| :----------------------- | :--------------------------------------------------------- |
| start_of_hour_timestamp  | unix timestamp at minute 0                                 |
| start_of_day_timestamp   | unix timestamp at hour 0, minute 0                         |
| start_of_month_timestamp | unix timestamp at first day of the month, hour 0, minute 0 |

## Examples

### Fetch the 5 biggest markets by total borrowed in USD

```GraphQL
{
  assets(first: 5, orderBy: totalBorrowsUsd, orderDirection: desc) {
    symbol
    totalBorrows
    totalBorrowsUsd
    currPriceUsd
  }
}
```

### Get the current balances of an account

```GraphQL
{
  account(id: "0x0000000002732779240fe05873611dc4203dfb71") {
    balances {
      amount
      asset {
        symbol
      }
    }
  }
}
```

### Get the transaction history of an account

```GraphQL
{
  account(id: "0x0000000002732779240fe05873611dc4203dfb71") {
    balanceChanges {
      type
      timestamp
      amount
      amountUsd
      asset {
        symbol
      }
    }
  }
}
```

### Get USD amount borrowed on February 10th 2022

First we need to create our ID using the parameters define in the [Querying time based aggregates](#querying-time-based-aggregates) section. In this case, February 10th 2020 = 1644451200.

```GraphQL
{
  dailyBorrow(id: "1644451200") {
  	count
    totalUsdAmount
  }
}
```

### Last 30 days of deposit amounts

```GraphQL
{
  dailyDeposits(first: 30, orderBy: timestamp, orderDirection: desc) {
    id
    timestamp
    totalUsdAmount
  }
}
```

### All transactions between February 1st 2022 and February 3rd 2022 

```GraphQL
{
  balanceChanges(orderBy: timestamp, orderDirection: asc, where: {timestamp_gte: 1643673600, timestamp_lte: 1643932799}) {
    timestamp
    type
    amount
    amountUsd
  	account {
      id
    }
    asset {
      symbol
    }
  }
}
```