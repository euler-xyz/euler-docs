# Risk Factors List

| Token | collateralFactor | borrowFactor | reserveFactor | borrowIsolated | crossBorrow | InterestRateModel | Uniswap V3 fee tier (%) |
|-------|------|-------|-------|------|-------|-------|------|
| USDT | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| ENS | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| 1INCH | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| ILV | 0| 0.28 | 0.23 | true | false | Default | 1 |
| CVX | 0| 0.28 | 0.23 | true | false | Default | 1 |
| RENDOGE | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| FLX | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| RAI | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BRIGHT | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| AGEUR | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| ANT | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| BANK | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| WBTC | 0| 0.28 | 0.23 | true | false | Default | 0.3 |
| DAI | 0.85| 0.88 | 0.23 | false | true | Default | 0.3 |
| WETH | 0.88| 0.91 | 0.23 | false | true | Default | Pegged |
| USDC | 0.9| 0.94 | 0.23 | false | true | Default | 0.3 |



_Note: the Collateral Factor of the lent asset(s) is multiplied by the Borrow Factor of the borrowed asset(s) to arrive at the final factor._

_For eg if you lend 1000 USD worth of USDC, you can borrow UNI in line with a final factor of 0.648 (0.90 x 0.72). Hence, 648 USD worth of UNI._

_Alternatively, if you lend 500 USD worth of USDC and 500 USD worth of WETH, your risk-adjusted collateral value is (500 x 0.90) + (500 x 0.88) = 890 USD. If you were to borrow UNI, you could borrow 890 x 0.72 = 640.8 USD worth of UNI._&#x20;

_Note that if you borrowed less UNI, for eg 500 USD worth, you could still borrow additional UNI or a cross tier asset like LINK against your risk adjusted collateral before hitting the threshold._
