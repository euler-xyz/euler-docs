# Collateral and Borrow Factor Methodology

On Euler, we use a two-sided approach to estimate risks of borrowing any tokens versus any given collateral. These risks are encapsulated in asset-specific collateral factors (as on Compound) and borrow factors (an Euler innovation).

Consequently, collateral factor reflects the risk of the asset that’s being used as collateral, whilst borrow factors reflect risks of the asset that’s being borrowed.

### **Collateral Assets**

When it comes to quality of collateral, it is of paramount importance that it ranks very high in our index list.

An illiquid collateral asset can be exploited by causing a price surge to allow a malicious user to borrow an inflated amount of tokens without an incentive to return them.

Alternatively, a collateral asset that’s collapsing in price and is experiencing high slippage makes it uneconomical for liquidators to close positions, leading to bad debts. This scenario is more systemic, which is why only the highest quality assets can become eligible collaterals.

### **Borrowed Assets**

While borrowed assets are less systemic than collateral assets, they also have specific risks.

For example, a borrowed token price that triples in a matter of seconds versus its collateral means there’s no incentive for the borrower to return the token, which results in bad debt. This is why the borrow factor should reflect the volatility and liquidity of the asset.

Alternatively, crashing a borrowed asset's price allows a malicious actor to borrow more tokens than normally possible. This attack can happen if there's not enough liquidity overall, especially if liquidity is too concentrated around a tiny range.

### **Asset Config Overrides**

While Collateral and Borrow factors allow controlling risks of borrowing any asset with any given collateral, it is also possible for governance to set granular factor overrides on selected liability - collateral asset pairs. It is useful especially for assets that are expected to be correlated in price, e.g. USD stablecoins or ETH LSDs. Governance may decide to set an override, designating both the liability asset, the collateral asset and a special collateral factor to be used. The borrow factor for the pair is always one. Users who deposit and borrow assets with an override can usually expect better capital efficiency. The override mechanism can effectively be applied to behave similarily to AAVE's V3 efficiency mode (emode).
