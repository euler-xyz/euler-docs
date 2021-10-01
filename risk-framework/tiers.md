# Tiers

Euler assets fall into three different tiers: isolated, cross and collateral tiers. 

**Isolated-tier** assets are available for ordinary lending and borrowing, but they cannot be used as collateral to borrow other assets, and they can only be borrowed in isolation. What this means is that they cannot be borrowed alongside other assets using the same pool of collateral. For example, if a user has USDC and DAI as collateral, and they want to borrow isolation-tier asset ABC, then they can only borrow ABC. If they later want to borrow another token, XYZ, then they can only do so using a separate account on Euler.

Governance allows to promote assets to cross and collateral tiers, but also to alter borrow factors. However, there will be a default borrow factor for all assets listed in the isolated tier.

**Cross-tier** assets are available for ordinary lending and borrowing, and cannot be used as collateral to borrow other assets, but they can be borrowed alongside other assets. For example, if a user has USDC and DAI as collateral, and they want to borrow cross-tier assets ABC and XYZ, then they can do so from a single account on Euler.

**Collateral-tier** assets are available for ordinary lending and borrowing, cross-borrowing, and they can be used as collateral. For example, a user can deposit collateral assets DAI and USDC, and use them to borrow collateral assets UNI and LINK, all from a single account.   


