# Chainlink support on Euler

Euler, to fulfill its role of being a permissionless protocol, lets users activate a lending market for any asset that has a WETH pair on Uniswap v3. To achieve that, Euler uses Uniswap v3 time-weighted average price \(TWAP\) as its main pricing oracle. However, this core dependency on Uniswap comes with its limitations. Currently on Euler, it is not possible to list an asset that does not have a WETH pair on Uniswap v3. The tiers of the assets in the protocol (collateral, cross, isolated) rely on the Uniswap oracle strength and the risks associated. Moreover, bringing the TWAP to Euler is a relatively expensive operation in terms of gas usage. Hence, it has been decided to extend the pricing types supported on Euler and include Chainlink oracles as the pricing source.

Chainlink is the most used data provider in the industry. It has a very good reputation and provides secure pricing feeds that are used by lending protocols industry leaders like Aave, Compound and others. Integration with Chainlink on Euler will bring a reduction of the protocol's dependency on Uniswap. It will lower the oracle manipulation risks for those assets that have very little liquidity in WETH pair on Uniswap v3. Also, for all the assets that will have the Chainlink oracle set as a price source, it will reduce the gas usage for all the operations that require price fetching. 


## Contracts changes

In order to integrate with Chainlink, several contract modules on Euler require to be upgraded. The integration is a non-breaking change, meaning that all the pricing types that existed on Euler until now, should still be supported.

### `Constants.sol`

A new pricing type of `PRICINGTYPE__CHAINLINK` is introduced.

### `Events.sol`

A new `GovSetChainlinkPriceFeed()` event is introduced. It will be emitted when the governance decides to configure a Chainlink oracle address for a given underlying asset.

### `Storage.sol`

`chainlinkPriceFeedLookup` is added to store the Chainlink oracle addresses for given underlying assets.

### `Governance.sol`

`setChainlinkPriceFeed()` is added to configure a Chainlink oracle address for a given underlying asset. It has to be called first before the pricing type for the asset is changed to Chainlink. As WETH is a reference asset on Euler, only ETH quote types will be supported. Hence, it is sufficient to store only the address of the oracle and there is no need to store the decimals (they will always be 18 for all asset/ETH price feeds).

`setPricingConfig()` is modified to support setting the pricing type of a given underlying asset to `PRICINGTYPE__CHAINLINK`. As already mentioned, `setChainlinkPriceFeed()` must be called first. Worth noting is the fact that even though `PRICINGTYPE__CHAINLINK` is configured, pricing parameters will still be pointing to the Uniswap pool fee which TWAP will be used as a fallback oracle in case Chainlink oracle becomes stale. However, if 0 passed as a `newPricingParameter`, there will be no Uniswap fallback pool configured.

### `Markets.sol`

`getChainlinkPriceFeedConfig()` view method is added to easily read the Chainlink oracle configured for a given asset.

Moreover, natspec documentation was modified to reflect the addition of a new pricing type and the way pricing parameters are interpreted within the system.

### `RiskManager.sol`

`RiskManager.sol` contains the most significant changes to the system. The `getPriceInternal()` function was updated to support `PRICINGTYPE__CHAINLINK`. It calls a new function `callChainlinkLatestAnswer()` that calls the Chainlink oracle's `latestAnswer()` function to get the current price. `callChainlinkLatestAnswer()` fetches the price and implements the verification of staleness in the same way Aave does. Although it calls the `latestAnswer()`, which is marked as deprecated, the answer is validated and if less than or equal to 0 the transaction will either be reverted with `e/unable-to-get-the-price` error or Uniswap price will be fetched if pool fee previously configured. The highest supported price in the system is `1e36` hence the returned price is limited if greater. 

Important to note is the fact that up to now the system has been relying on TWAP hence `twap` and `twapPeriod` were returned by `getPriceInternal()`. Now, because the price reported by Chainlink is the current price, the returned `twap` represents the current price and `twapPeriod` period returned is always 0. Also for `PRICINGTYPE__CHAINLINK`, `getPriceFull()` returns current Chainlink price both for `twap` and `currPrice`.
