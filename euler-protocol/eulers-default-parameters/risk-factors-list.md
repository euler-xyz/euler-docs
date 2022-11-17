---
description: Find information about the risk factors for each asset on Euler
---

# Risk Factors

## Introduction

This page outlines the main risk parameters on Euler, as determined by [governance](broken-reference). All parameters are displayed in Table 1 below.

**Table 1** | Collateral, borrow, and reserve factor parameter settings on Euler\_.\_

| Token | collateralFactor | borrowFactor | reserveFactor | borrowIsolated | crossBorrow | InterestRateModel | Uniswap V3 fee tier (%) |
|-------|------|-------|-------|------|-------|-------|------|
| USDT | 0.9| 0.94 | 0.05 | false | true | Major | Chainlink |
| WSTETH | 0.85| 0.89 | 0.1 | false | true | Mega | Chainlink |
| STETH | 0.87| 0.91 | 0.1 | false | true | Lido | Chainlink |
| FLX | 0| 2.5e-10 | 0.23 | true | false | Default | 0.3 |
| AAVE | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| ALCX | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| ANT | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| APE | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| BABL | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BADGER | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| BAL | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BANK | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BED | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BRIGHT | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BUSD | 0| 0.28 | 0.23 | true | false | Default | 1 |
| CARD | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| CNV | 0| 0.28 | 0.23 | true | false | Default | 1 |
| COMP | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| CRV | 0| 0.28 | 0.23 | true | false | Default | 1 |
| CTX | 0| 0.28 | 0.23 | true | false | Default | 1 |
| CVXCRV | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| DPI | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| DPX | 0| 0.28 | 0.23 | true | false | Default | 1 |
| DYDX | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| ETH2X-FLI | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| EXRD | 0| 0.28 | 0.23 | true | false | Default | 1 |
| FLOAT | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| FNT | 0| 0.28 | 0.23 | true | false | Default | 1 |
| FPIS | 0| 0.28 | 0.23 | true | false | Default | 1 |
| FRAX | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| FTT | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| FXS | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| GAMMA | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| GFI | 0| 0.28 | 0.23 | true | false | Default | 1 |
| GRT | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| GTC | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| GUSD | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| IDLE | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| ILV | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| IMX | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| INDEX | 0| 0.28 | 0.23 | true | false | Default | 1 |
| LDO | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| LOOKS | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| LQTY | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| LRC | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| LUSD | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| LYXE | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| MIM | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| MPL | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| MTA | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| MVI | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| NMR | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| OGN | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| QNT | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| QSP | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| RAD | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| RAI | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| RENDOGE | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| REQ | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| RETH | 0| 0.28 | 0.23 | true | false | Default | 0.05 |
| RLC | 0| 0.28 | 0.23 | true | false | Default | 1 |
| RPL | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| SETH2 | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| SLP | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| SNX | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| SOCKS | 0| 0.28 | 0.23 | true | false | Default | 1 |
| SOS | 0| 0.28 | 0.23 | true | false | Default | 1 |
| SSV | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| STG | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| SUSD | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| TCR | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| TON | 0| 0.28 | 0.23 | true | false | Default | 1 |
| TORN | 0| 0.28 | 0.23 | true | false | Default | 1 |
| TRDL | 0| 0.28 | 0.23 | true | false | Default | 1 |
| UBI | 0| 0.28 | 0.23 | true | false | Default | 1 |
| VEGA | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| WAMPL | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| WILD | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| WNXM | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| WOO | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| XCN | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| XMON | 0| 0.28 | 0.23 | true | false | Default | 1 |
| YFI | 0| 0.28 | 0.23 | true | false | Default | Chainlink |
| YVBOOST | 0| 0.28 | 0.23 | true | false | Default | 1 |
| 1INCH | 0| 0.5 | 0.23 | true | false | Major | Chainlink |
| AGEUR | 0| 0.5 | 0.23 | false | true | Stable | 0.05 |
| CVX | 0| 0.5 | 0.23 | false | true | Major | Chainlink |
| PERP | 0| 0.5 | 0.23 | false | true | Major | Chainlink |
| RBN | 0| 0.5 | 0.23 | false | true | Major | 1 |
| SHIB | 0| 0.5 | 0.23 | false | true | Major | Chainlink |
| OSQTH | 0| 0.56 | 0.23 | false | true | Major | 0.3 |
| AXS | 0| 0.66 | 0.23 | false | true | Major | Chainlink |
| ENS | 0| 0.66 | 0.23 | false | true | Major | Chainlink |
| MATIC | 0| 0.66 | 0.23 | false | true | Major | Chainlink |
| MKR | 0| 0.66 | 0.23 | false | true | Major | Chainlink |
| LINK | 0.3| 0.76 | 0.23 | false | true | Major | Chainlink |
| UNI | 0.3| 0.76 | 0.23 | false | true | Major | Chainlink |
| DAI | 0.85| 0.88 | 0.23 | false | true | Stable | Chainlink |
| WBTC | 0.88| 0.91 | 0.23 | false | true | Mega | Chainlink |
| WETH | 0.88| 0.91 | 0.23 | false | true | Default | Pegged |
| USDC | 0.9| 0.94 | 0.23 | false | true | Stable | Chainlink |


_Note: the Collateral Factor of the lent asset(s) is multiplied by the Borrow Factor of the borrowed asset(s) to arrive at the final factor._

_For example, if you lend 1,000 USD worth of USDC, you can borrow UNI in line with a final factor of 0.648 (0.90 x 0.72). Hence, 648 USD worth of UNI._

_Alternatively, if you lend 500 USD worth of USDC and 500 USD worth of WETH, your risk-adjusted collateral value is (500 x 0.90) + (500 x 0.88) = 890 USD. If you were to borrow UNI, you could borrow 890 x 0.72 = 640.8 USD worth of UNI._

_Note that if you borrowed less UNI, for example 500 USD worth, you could still borrow additional UNI or a cross tier asset like LINK against your risk-adjusted collateral before hitting the threshold._

_Lastly, please note that the risk factors list will be periodically updated. If a token/market is activated on the DApp but not listed, please check back later for an updated list._
