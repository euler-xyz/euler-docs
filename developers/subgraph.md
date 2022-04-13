---
description: Subgraph
---

### TODO

- GitBook
  - Add examples
  - Change subgraph link for prod once deployed
- Subgraph
  - Make sure we are linking to entity when possible instead of referring to id (i.e Liquidation entity => use Account type instead of Bytes for liquidator and violator fields)

# Subgraph

## Links

- The Graph: https://thegraph.com/hosted-service/subgraph/hboisselle/euler-mainnet-dev?selected=playground
- API: https://api.thegraph.com/subgraphs/name/hboisselle/euler-mainnet-dev
- GitHub: https://github.com/euler-xyz/euler-subgraph

## About

- All amounts have a fixed decimal precision of 1e18.
- Are timestamps are represented as [unix timestamps](https://en.wikipedia.org/wiki/Unix_time).
- USD and ETH exchange rates of all assets are pulled through Euler directly

## Entities

### Asset

Contains information about all Euler markets, pulled from EulerGeneralView contract.

```
type Asset @entity {
  "asset_address"
  id: ID!
  blockHash: Bytes!
  blockNumber: Int!
  timestamp: Int!
  transactionHash: Bytes!
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
  twapPeriod: BigInt!
  currPrice: BigInt!
  currPriceUsd: BigInt!
  pricingType: Int!
  pricingParameters: BigInt!
  pricingForwarded: Bytes!
  underlyingBalance: BigInt!
  eulerAllowance: BigInt!
  eTokenBalance: BigInt!
  eTokenBalanceUnderlying: BigInt!
  dTokenBalance: BigInt!
  collateralValue: BigInt!
  liabilityValue: BigInt!
  numBorrows: BigInt!
  borrowIsolated: Boolean!
  poolSize: BigInt!
  interestAccumulator: BigInt!
  interestRate: BigInt!
  twapPrice: BigDecimal!
  config: AssetConfig
}
```

```
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

```
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

```
type Balance @entity {
  "account_address:underlying"
  id: ID!
  account: Account!
  amount: BigInt!
  asset: Asset!
}

```

```
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

```
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

```
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

```
type EulerMarketStore @entity {
  id: ID!
  markets: [Asset!]
}
```

### EulerOverview

Aggregated metrics for all markets as a whole.

```
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

```
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

```
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

```
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

### Hourly/Daily/MonthlyAssetStatus

Aggregated metrics of a specific market over hourly, daily and monthly time period.

```
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
}
```

### Hourly/Daily/MonthlyRepay

Aggregated metrics for repay transactions over hourly, daily and monthly time period.

```
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

```
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

```
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

```
type HourlyBorrow @entity {
  "start_of_hour_timestamp"
  id: ID!
  timestamp: Int!
  count: Int!
  totalAmount: BigInt!
  totalUsdAmount: BigDecimal!
}

```
