---
description: Find information about the risk factors for each asset on Euler
---

# Risk Factors

## Introduction&#x20;

This page outlines the main risk parameters on Euler, as determined by [governance](../../governance/governance.md). All parameters are displayed in Table 1 below.

**Table 1** | Collateral, borrow, and reserve factor parameter settings on Euler_._

| Token     | collateralFactor | borrowFactor | reserveFactor | borrowIsolated | crossBorrow | InterestRateModel | Uniswap V3 fee tier (%) |
| --------- | ---------------- | ------------ | ------------- | -------------- | ----------- | ----------------- | ----------------------- |
| WSTETH    | 0.85             | 0.89         | 0.1           | false          | true        | Mega              | 0.05                    |
| FLX       | 0                | 2.5e-10      | 0.23          | true           | false       | Default           | 0.3                     |
| SOS       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| SNX       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| OGN       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| WOO       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| TCR       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| RPL       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| ILV       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| MTA       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| REQ       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| TRDL      | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| MVI       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| UBI       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| RENDOGE   | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| FLOAT     | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| BED       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| RAD       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| FNT       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| DYDX      | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| ETH2X-FLI | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| MPL       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| MIM       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| RAI       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| GTC       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| WILD      | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| LRC       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| INDEX     | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| DPX       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| DPI       | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| IDLE      | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| BRIGHT    | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| YFI       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| EXRD      | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| WNXM      | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| ANT       | 0                | 0.28         | 0.23          | true           | false       | Default           | 1                       |
| BANK      | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| BABL      | 0                | 0.28         | 0.23          | true           | false       | Default           | 0.3                     |
| USDT      | 0                | 0.5          | 0.23          | false          | true        | Major             | 0.3                     |
| 1INCH     | 0                | 0.5          | 0.23          | true           | false       | Major             | 0.3                     |
| SHIB      | 0                | 0.5          | 0.23          | false          | true        | Major             | 1                       |
| CVX       | 0                | 0.5          | 0.23          | false          | true        | Major             | 1                       |
| PERP      | 0                | 0.5          | 0.23          | false          | true        | Major             | 0.3                     |
| RBN       | 0                | 0.5          | 0.23          | false          | true        | Major             | 1                       |
| AGEUR     | 0                | 0.5          | 0.23          | false          | true        | Stable            | 0.05                    |
| oSQTH     | 0                | 0.56         | 0.23          | false          | true        | Major             | 0.3                     |
| AXS       | 0                | 0.66         | 0.23          | false          | true        | Major             | 0.3                     |
| MATIC     | 0                | 0.66         | 0.23          | false          | true        | Major             | 0.3                     |
| ENS       | 0                | 0.66         | 0.23          | false          | true        | Major             | 0.3                     |
| MKR       | 0                | 0.66         | 0.23          | false          | true        | Major             | 0.3                     |
| LINK      | 0.66             | 0.76         | 0.23          | false          | true        | Major             | 0.3                     |
| UNI       | 0.66             | 0.76         | 0.23          | false          | true        | Major             | 0.3                     |
| DAI       | 0.85             | 0.88         | 0.23          | false          | true        | Stable            | 0.3                     |
| WBTC      | 0.88             | 0.91         | 0.23          | false          | true        | 2000503           | 0.3                     |
| WETH      | 0.88             | 0.91         | 0.23          | false          | true        | Default           | Pegged                  |
| USDC      | 0.9              | 0.94         | 0.23          | false          | true        | Stable            | 0.3                     |

_Note: the Collateral Factor of the lent asset(s) is multiplied by the Borrow Factor of the borrowed asset(s) to arrive at the final factor._

_For example, if you lend 1,000 USD worth of USDC, you can borrow UNI in line with a final factor of 0.648 (0.90 x 0.72). Hence, 648 USD worth of UNI._

_Alternatively, if you lend 500 USD worth of USDC and 500 USD worth of WETH, your risk-adjusted collateral value is (500 x 0.90) + (500 x 0.88) = 890 USD. If you were to borrow UNI, you could borrow 890 x 0.72 = 640.8 USD worth of UNI._

_Note that if you borrowed less UNI, for example 500 USD worth, you could still borrow additional UNI or a cross tier asset like LINK against your risk-adjusted collateral before hitting the threshold._

_Lastly, please note that the risk factors list will be periodically updated. If a token/market is activated on the DApp but not listed, please check back later for an updated list._
