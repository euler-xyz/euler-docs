---
description: >-
  Find out how Euler works and how it differs from other popular lending
  protocols
---

# White Paper (ENG-CHN)

## White Paper

## Euler 白皮书-了解 Euler 的特别之处，与其他借贷协议又有何不同（ENG-CHN）

### 作者 - Authors

Michael Bentley & Doug Hoyte\
[https://www.euler.finance](https://www.euler.finance)

本文翻译自@Euler 团队的关于 Euler 项目的白皮书。已得到作者的授权。译者为@chainguys。转载请注明作者和译者。 （Coptyright©2021 by @Euler, translated by @chainguys）

### 概览 - Abstract

Here, we present Euler: a permissionless lending protocol custom-built to help users lend and borrow more Ethereum-based tokens than ever before. The purpose of this white paper is to describe how Euler works at a high level and highlight new features and innovations that help to set it apart from other popular lending protocols, like Compound and Aave.

我们在此向您介绍 Euler:为帮助用户借贷更多基于以太坊的代币而生，去（无）审批化的借贷协议。我们在此向您介绍 Euler:一个为了帮助更多用户更方便地借贷各类以太坊代币而出生，去（无）审批化的借贷协议。本白皮书的目的是描述 Eule 如何在高层次上（宏观上）工作，并强调（那些）有助于将 Euler 与其他流行的借贷协议（如 Compound 和 Aave）区分开来的新功能和创新。

### 导览 - Introduction

The ability to lend and borrow assets efficiently is a crucial feature of any financial system. In the world of traditional finance, this process is typically facilitated by trusted and permissioned third-parties such as banks, who connect people with a surplus of money to those who need access to it in the short-term. In the world of decentralised finance (DeFi), trusted and permissioned third-parties are no longer needed; banks have been replaced by trustless and permissionless lending protocols running on the blockchain [(1)](white-paper.md#references).

对任何金融系统来说，高效借贷能力都是至关重要的特征。在传统金融中，这个过程通常由可信和经审批（监管）的第三方来完成，比如银行，由它们来连接那些资本充裕和短时间需要资金的人。在 DeFi 的世界中，可信和经受审批（监管）的第三方将不再需要：银行已经被链上运行的去信任化和去审批化借贷协议所取代(1)。

Among the first-generation of DeFi lending protocols are Compound [(2)](white-paper.md#references) and Aave [(3)](white-paper.md#references). These protocols provide users with access to lending and borrowing capabilities for a handful of the most liquid ERC20 tokens. However, these protocols were not designed to handle the risks associated with lending and borrowing illiquid or volatile assets and have therefore relied on a permissioned listing system to protect their users from the risks associated with such assets.

第一代 DeFi 借贷协议主要有 Compound (2) and Aave (3)。这些协议为用户提供了借贷某些流动性最好的 ERC20 代币的入口。然而，这些协议在设计中却并未考虑处理由（借贷）流动性不佳，价格有较大波动的资产所带来的风险，所以这些协议要依赖一个需要审批的上币系统来帮用户规避这些风险。

Consequently, there remains significant unmet demand for lending and borrowing the long tail of crypto assets. On the lending side, users want to deposit tokens to earn yield and take leveraged long positions. On the borrowing side, users want to reduce their exposure to volatility and take leveraged short positions. Here, we present Euler: a permissionless lending protocol custom-built with an array of new features to help users lend and borrow more types of tokens than ever before.

从结果上来说，市场上存在着借贷长尾资产的巨大需求。在出借方的角度看，用户希望存入代币来获得收益并且建立带杠杆的多仓。在借款方来看的角度看，用户需要减少波动性（风险）并且建立带杠杆的空仓。在此，我们向各位介绍 Euler:一个去审批化的借贷协议——它拥有多项量身定做的新特性，可以帮助用户借贷更多种类的代币。

### 准备开始 - Getting Started

Euler comprises a set of smart contracts deployed on the Ethereum blockchain that can be openly accessed by anyone with an internet connection. Euler is managed by holders of a protocol native governance token called Euler Governance Token (EUL). Euler is entirely non-custodial; users are responsible for managing their own funds.

As creators of the protocol, the Euler development team have produced a convenient and user-friendly front-end to the Euler smart contracts which is hosted at [https://app.euler.finance](https://app.euler.finance). However, users are free to access the protocol in whatever format they wish, and we encourage developers to create their own front-end access points to the protocol to help decentralise access and increase censorship resistance.

Euler 包含了一些列部署在以太坊上，任何人都可以上网公开进入的智能合约。Euler 由治理代币 Euler Governance Token (EUL)的持有人管理。Euler 没有托管方，用户需要自己管理自己的资产。 作为该协议的创造者，Euler 研发团队已经研发出了一个对用户友好的智能合约管理界面（https://app.euler.finance）。当然，用户也可以用自己喜欢的方式进入协议，而且我们鼓励开发者创造他们自己的前端界面来促进去中心化和增加抗审查性。

### 去审批化上币 - Permissionless Listing

Euler lets its users determine which assets are listed. To enable this functionality, Euler uses Uniswap v3 as a core dependency [(4)](white-paper.md#references). Any asset that has a WETH pair on Uniswap v3 can be added as a lending market on Euler by anyone straight away [(5)](white-paper.md#references).

Euler 让用户自行决定哪些资产可以上市。Euler 主要使用了 Uniswap V3 来实现这个功能(4)。任何在 Uniswap V3 有 WETH 交易对的资产都可以被 Euler 直接添加(5)。

#### 资产梯队/分层 - Asset Tiers

Permissionless listing is much riskier on decentralised lending protocols than on other DeFi protocols, like decentralised exchanges, because of the potential for risk to spill over from one pool to another in quick succession. For example, if a collateral asset suddenly decreases in price, and subsequent liquidations fail to repay borrowers' debts sufficiently, then the pools of multiple different types of assets can be left with bad debts.

To counter these challenges, Euler uses risk-based asset tiers to protect the protocol and its users:

在去中心化借贷协议上进行去审批化上币，要比在其他 Defi 项目（如去中心化交易所）更具风险，因为风险可能会迅速从一个流动性池传导到其他流动性池。举例来说，如果一个抵押资产的价格突然快速下降，并且在清算中无法充分偿还借款人的债务，那么多个流动性池子都会陷入债务危机。

**Isolation-tier** assets are available for ordinary lending and borrowing, but they cannot be used as collateral to borrow other assets, and they can only be borrowed in isolation. What this means is that they they cannot be borrowed alongisde other assets using the same pool of collateral. For example, if a user has USDC and DAI as collateral, and they want to borrow isolation-tier asset ABC, then they can _only_ borrow ABC. If they later want to borrow another token, XYZ, then they can only do so using a separate account on Euler.

隔离层资产可以用来常规的借贷，但是它们不能作为抵押物使用来借出别的资产，它们也只能隔离使用。这意味着它们不能在相同抵押物的流动性池中使用。举例来说，如果一个用户用 USDC 和 DAI 来做抵押物(这两者都不是隔离层资产)，当用户想借一种隔离资产 ABC 时，他就只能借到 ABC。如果这时要借出另一种代币 XYZ，那么就需要在 Euler 上创建另外单独的账户（才能借到 XYZ）。

**Cross-tier** assets are available for ordinary lending and borrowing, and cannot be used as collateral to borrow other assets, but they can be borrowed alongside other assets. For example, if a user has USDC and DAI as collateral, and they want to borrow cross-tier assets ABC and XYZ, then they can do so from a single account on Euler.

跨层资产可以用于普通借贷，可以与其他资产一起使用，但不能作为抵押物使用。举例来说，如果一个用户用 USDC 和 DAI 做抵押物，那他可以在同一个账户内借到跨层资产 ABC 和 XYZ。

**Collateral-tier** assets are available for ordinary lending and borrowing, cross-borrowing, and they can be used as collateral. For example, a user can deposit collateral assets DAI and USDC, and use them to borrow collateral assets UNI and LINK, all from a single account.

EUL holders can vote to liberate assets from the isolation-tier and promote them to the cross-tier or collateral-tier through governance mechanisms. Promoting assets up the tiers increases capital efficiency on Euler, because it allows lenders and borrowers to use capital more freely, but it may also expose protocol users to increased risk. It is therefore in EUL holders' interests to balance these concerns.

抵押层资产可以用来进行普通借贷，交叉借款，也可以作为抵押物。举例来说，一个用户可以存入 DAI 和 USDC 作为抵押物在一个账号中借到抵押层资产 UNI 和 LINK。EUL 持有者可以通过治理机制，投票决定这三类资产如何互相转化。 将资产“上升”梯度会增加资产在 Euler 上的资金效率，因为借贷双方交易更加自由了，但是也可能会增加协议用户暴露在风险中的几率。综合来看，EUL 持有者对这些担忧进行平衡是符合自身利益的。

PS:关于这三种资产，虽然白皮书原文描述比较晦涩，但是核心就可以用一句话阐述：能不能用作抵押物且被借后是否需要隔离管理。抵押层资产最方便，既可以做抵押物，但被借到之后也不需要隔离管理。跨层资产不能作为抵押物，但是被借到之后不需要隔离管理。隔离层资产不能作为抵押物使用，被借到之后必须隔离管理（一个子账号只能有一种隔离资产）。

### 借贷 - Lending and Borrowing

When lenders deposit into a liquidity to a pool on Euler, they receive interest-bearing ERC20 eTokens in return, which can be redeemed for their share of the underlying assets in the pool at any time, as long as there are unborrowed tokens in the pool (similar to Compound's [cTokens](https://compound.finance/docs/ctokens)). Borrowers take liquidity out of a pool and return it with interest. Thus, the total assets in the pool grows through time. In this way, lenders earn interest on the assets they supply, because their eTokens can be redeemed for an increasing amount of the underlying asset over time.

当出借人向流动性池中添加流动性时，他们会收到会产生利息的 ERC20 代币（eTokens），这些代币可以随时按比例赎回他们在流动性池中的资产，只要池中还有未借出的代币（与 Compound 的 cToken 类似）。借款方从池中借出流动性，返还时支付利息。于是，池中的资产就会随着时间而成长。如此，出借人就可以获得利息，因为它们的 eTokens 可以溢价退出。

#### 代币化债务 - Tokenised Debts

Similarly to Aave's [debt tokens](https://docs.aave.com/developers/tokens/debttoken), Euler also tokenises debts on the protocol with ERC20-compliant interfaces known as dTokens. The dToken interface allows the construction of positions without needing to interact with underlying assets and can be used to create derivative products that include debt obligations.

与 AAVE 的债务代币类似，Euler 也通过名为 dTokens 的，兼容 ERC20 代币的界面/接口，将债务代币化。dToken 接口/界面使得无需和标的资产交互就可以构筑仓位，也可以用来制作包含债务凭证的衍生品。

Rather than providing non-standard methods to transfer debts, Euler uses the regular transfer/approve ERC20 methods. However, the permissioning logic is reversed: rather than being able to send tokens to anyone, but requiring approval to take them, dTokens can be taken by anyone, but require approval to accept them. This also prevents users from "burning" their dTokens. For example, the zero address has no way of approving an in-bound transfer of dTokens.

Borrowers pay interest on their loans in terms of the underlying asset. The interest accrued depends on an algorithmically determined interest rate for each asset. A portion of the interest accrued is held in reserves to cover the accumulation of bad debts on the protocol.

没有选择提供非标准化措施来转移债务，Euler 使用常规的 ERC20 方法。但是，这个去审批化的逻辑就反过来了：不是等（当前）持有方同意后再发送给任何人，而是必须接收方同意后，dTokens 才可以被拿走。这也可以防止用户燃烧 dTokens。举例来说，零余额的地址就无法允许 dTokens 转入。 借款方付出利息。而利息的归集则取决于一个决定每类资产利息水平的算法。一部分利息会作为“风险金/储备金”而被归集到一起用来对冲坏账。

#### 受保护的抵押物 - Protected Collateral

On Compound and Aave, collateral deposited to the protocol is always made available for lending. Optionally, Euler allows collateral to be deposited, but not made available for lending. Such collateral is 'protected'. It earns a user no interest, but is free from the risks of borrowers defaulting, can always be withdrawn instantly, and helps protect against borrowers using tokens to influence governance decisions (see Maker governance issue [(6)](white-paper.md#references)) or take short positions.

在 Compound 和 Aave 上，存在协议上的抵押物是随时可以出借的。但 Euler 提供了另一个选项：抵押物可以先存入，但并不（马上）对外出借。这样的抵押物就是“受保护”的。虽然这样用户无法收取利息，但是也免除了默认出借所带来的风险。受保护的抵押物可以随时提现，也帮助避免有人利用代币恶意影响治理决策（参见 Maker governance issue (6)）

#### 展期/延期流动性 - Defer Liquidity

Normally, an account's liquidity is checked immediately after performing an operation that could fail due to insufficient collateral. For example, taking out a borrow, withdrawing collateral, or exiting a market could cause a transaction be reverted due to to a collateral violation.

However, Euler has a feature that allows users to defer their liquidity checks. Many operations can be performed and the liquidity is checked only once at the very end. For example, without deferring liquidity checks, a user must first deposit collateral before issuing a borrow. However, if done in the same transaction, deferring the liquidity check will allow the user to do this in any order.

正常情况下，一个账户在每完成一次可能因抵押物不足而失败的操作后，都会立刻被检测流动性。举例来说，借一笔钱，提出抵押物，或者是退出市场都可能因为抵押物（价值）波动而导致交易失败。 但是，Euler 有一个特性使得用户可以让流动性检验延期。许多操作可以被执行，流动性检测也只会在最后进行。举例来说，如果流动性检测不延期，一个用户在发起借款之前必须先存入抵押物。但是，展期流动性检测，用户就可以任意顺序完成上述交易。

#### 无费用闪贷 - Feeless Flash Loans

Unlike Aave, Euler doesn't have a native concept of flash loans. Instead, users can defer their liquidity check, make an uncollateralised borrow, perform whatever operation they like, and then repay the borrow. This can be used to rebalance positions, build-up leveraged positions, take advantage of external arbitrage opportunities, and more.

Because Euler only charges fees according to the time value of money, and from the blockchain's perspective flash loans are held for a duration of 0 seconds, they are entirely free on Euler (ignoring gas costs). We believe that flash loan fees are ultimately in a race to the bottom that will be accelerated by advances like flash minting. The ecosystem benefits gained from simple and free flash loans outweigh the relatively modest benefit from flash loan fees.

与 Aave 不同，Euler 并没有原生概念的闪贷。不过，用户可以延期流动性检查，使用无抵押借款，进行他们喜欢的任何操作，最后偿还或借款。这可以被用来做仓位的再平衡，建立杠杆仓位，进行外部套利等。 因为 Euler 只根据资金的时间价值来收费，且从区块链的角度来看闪贷的持续时间为 0，所以它是没有费用的（忽略 gas 费用）。

我们相信闪贷费用最终会在诸如闪铸（flash minting）等高级功能的加持下，最终走向底部。整个生态从简单和免费的闪电贷中获得的系统性收益超过闪电贷费用带来的相对温和的收益。

#### 风险调整借款能力 - Risk-adjusted Borrowing Capacity

Like other lending protocols, Euler requires users to ensure that the value of their collateral remains higher than the value of their liabilities (except during the intermediate period when liquidity checks have been deferred). Over-collateralisation is encouraged by limiting how much borrowers can take out as a loan in the first place.

Compound achieves this in a one-sided way by using collateral factors to adjust down the value of a borrower's collateral assets when deciding how much they can borrow. This gives rise to a 'risk-adjusted collateral value' that helps to create a buffer that can be drawn upon by liquidators in the event that the value of a borrower's assets and liabilities changes over time. One of the problems with this approach is that it only adjusts for the risks associated with a borrower's collateral assets decreasing in value. There may be an asymmetric risk, however, of the borrower's liabilities increasing in value. This risk is not factored into the collateral factors.

跟其他借贷协议一样，Euler 需要用户确保他们的抵押物的价值比他们的债务更高（除非在流动性检查延期的时候）。Euler 一开始就通过限制借款人的借款额来鼓励超量抵押。 Compound 使用一种单向的方法：当决定一个用户能借多少钱的时候，平台会根据抵押参数(因子)来做低抵押物的价值。这样会使得“风险调整后抵押物价值”上升，从而形成一个缓冲带——清算人可以据此在借款人的资产或者负债变化的时候（主动管理）。但一个问题是这样总会向借款人抵押物资产贬值的方向调整。于是就可能存在一个非对称风险，借款人的负债在增加，但这没有作为抵押参数进行考虑。

On Euler, we therefore use a two-sided approach where we also adjust up the market value of a borrower's liabilities to arrive at a 'risk-adjusted liability value'. This approach improves capital efficiency on the protocol because it allows Euler to factor in the asset-specific risks of both downside and upside price movements. These risks are encapsulated in asset-specific collateral factors (as on Compound) and borrow factors (new to Euler). Ultimately, this approach means that the liquidation threshold of every borrower is tailored to the specific risk profiles associated with the assets they are borrowing and using as collateral.

To give an example, suppose a user has $1000 worth of USDC, and wants to borrow UNI. How much can they borrow? If USDC has a collateral factor of 0.9, and UNI has a borrow factor of 0.7, then a user can borrow upto $1000 _0.9_ 0.7 = $630 worth of UNI. At this level of borrowing, the risk-adjusted value of their collateral is $1000 \* 0.9 = $900, and the risk-adjusted value of their liabilities is $630 / 0.7 = $900. If UNI increases in price, then the risk-adjusted value of their liabilities will also increase to >$900, and the they will be eligible for liquidation. The buffer allowing for liquidation is $1000 - $630 = $370.

在 Euler,我们使用一种双向的方法：我们也将借款人债务的市场价值上调，来产生“风险调整后抵押物价值”。这使得资本使用效率大大提升——因为它使得 Euler 将资产价值涨跌这两种情况带来的风险都考虑进来。这些风险有的被概括为特定的抵押物因子（类似 Compound），有的则作为借贷因子（Euler 的创新）。最终，这一套方法意味着每个借款人的清算条件都是根据他们自身借入和抵押品资产情况量身定做。 举例来说，假设一个用户有价值 1000USDC 的抵押物，然后他想借入 UNI。那他可以借出多少钱？如果 USDC 有一个抵押参数 0.9，而 UNI 则有一个 0.7 的抵押参数，那么用户就可以借价值$1000_0.9_0.7=$630 的 UNI。在这个情况下，风险调整后价值就是$1000\*0.9=900 美金，而风险调整负债就是$630/0.7=$900。如果 UNI 价格上涨，那么风险调整负债也会增加，大于$900，并且会作为清算资产。这时清算的缓冲是$1000-$630 = $370。

### 去中心化价格预言机 - Decentralised Price Oracles

To be able to calculate whether a loan is over-collateralised or not, Euler needs to monitor the value of users' assets. On Compound, Maker, and Aave, various systems are used to get prices from off-chain sources and put them on-chain so that they can be accessed by the relevant smart contracts.

This approach is unsuitable for Euler's purposes because it requires centralised intervention whenever a new lending market needs to be created. Euler therefore relies on Uniswap v3's decentralised time-weighted average price (TWAP) oracles to assess the solvency of users [(4)](white-paper.md#references). The reference asset used to normalise prices on Euler is Wrapped Ether (WETH), which is the most common base pair on Uniswap [(5)](white-paper.md#references).

要能够计算一笔贷款是否超额抵押，Euler 需要监控用户资产价值。在 Compound,Maker 和 Aave 上，各类系统被应用，来从链下获得价格信息并且将其上传到链上，从而使得相关智能合约能够访问。 这个方法对实现 Eculer 的目的来说就不适合了，因为每当要创造一个新的借贷市场时，就会需要一个中心化的干预（审批）。Euler 因此使用 Uniswap v3 的去中心化时间加权平均价格（TWAP）预言机来评估用户的偿付能力(4)。Euler 作为标准化定价单位的是 Wrapped Ether (WETH),这是 Uniswap 最常见的基础交易对(5)。

#### TWAP

Uniswap TWAP is calculated using the geometric mean price of an asset over some interval of time. TWAP in general is both a smoothed and lagging indicator of the trade price: a TWAP over a short interval is a less smooth function, but more up-to-date, whilst a TWAP over a long interval is a smoother function, but less up-to-date. TWAP is ideal for Euler's purposes for several reasons.

Uniswap 的时间加权平均价格（TWAP）是由某项资产在某几个时间段的几何平均数计算出来的。一般来说，TWAP 是一个对交易价格既平滑也相对滞后的指标：一个短期的 TWAP 是一个不那么平滑的函数，但是却更具时效性；但长期的 TWAP 看起来更加平滑，时效性却相对差一些。TWAP 对 Euler 来说是非常理想的，原因如下：

First, TWAP is resistant to price manipulation attacks. It cannot be manipulated within a transaction or block (for example with flash loans or flash bots), because it is calculated using historic data. It is also expensive to manipulate using large market orders, because the manipulated price must be maintained for some period of time relative to the TWAP time interval. During this time, other users can take advantage of the manipulated price with arbitrage which will cause it to revert back to the broader market price. Arbitrage is especially practical on the blockchain because arbitrageurs have access to large amounts of capital (including from flash loans) and the atomic nature of transactions means that arbitrage transactions have a low execution risk. For these reasons, manipulating the price on a single decentralised exchange usually requires more widespread manipulation of all on-chain exchanges simultaneously, although even this can't prevent the (less practical but still possible) arbitrage between on and off-chain exchanges.

首先，TWAP 可以对抗价格操纵攻击。用（一笔）链上交易和区块是不能操纵市场的的（比如用闪贷等手段），因为使用的是历史数据。如果要通过市场大单来操纵，那会非常昂贵，因为这需要内操纵的价格在 TWAP 的时间段内维持一定时间的稳定。在这段时间内，其他用户就可以利用这个情况来套利，接着价格就会回归。套利在区块链中是非常具有可操作性的，因为套利者一般资金充沛，而（区块链）的原子化交易又意味着套利交易在执行上的风险很低。因为上述原因，在一个去中心化交易所里操纵价格经常意味着要在更大的规模上同时操控所有的链上交易所（实际上更不可能但是理论上成立），但即使是这样还是无法阻止链上链下的套利行为。

Second, the smooth nature of TWAP helps to remove the impact of price shocks on borrowers. In the event of a large trade, the current price on Uniswap can be moved significantly. Usually arbitrage bots will quickly converge this to the broader market value, so the maximum deviation of the TWAP will only be a fraction of the temporary price movement. This prevents some unnecessary liquidations and loans that may quickly become undercollateralised.

Third, instead of instantly jumping between two price levels, TWAPs change continuously, second-by-second. This property is used by Euler's liquidation process to implement Dutch auctions that reduce the value captured by miners and front-running bots.

其次，TWAP 平滑的天性可以帮助移除价格冲击对借款人的影响。假如有大单，Uniswap 的当前价格就会迅速变化。通常情况下套利机器会迅速使得（Uniswap）的价格和其他市场（更广泛市场）的价值趋同，所以这个最大的波动（偏离）在 TWAP 上就仅仅只是一个暂时价格变动的一部分。这样的机制就可以防止一些不必要的，会迅速变得抵押不足的清算或贷款。

#### 时间间隔 - Time Interval

One of the challenges in using TWAP is determining the right interval over which it should be calculated for a given asset. The trade-offs involved with shorter (longer) intervals may sometimes need to be taken into consideration and altered for specific assets. Euler therefore allows the default time interval to be updated by governance if EUL holders deem it necessary.

### 清算 - Liquidations

A borrower is considered to be in violation on Euler when the value of their risk-adjusted liabilities exceeds the value of their risk-adjusted collateral. A borrower that has just become in violation still has enough collateral to repay their loan, but is adjudged to be at risk of defaulting on their loan. Consequently, they may be liquidated in order to limit the potential for them to default.

当 Euler 用户的风险调整后负债值超过了风险调整后抵押物的价值时，就会被认为“违约”了。一个借款人刚刚进入“违约”状态时依然有足额的抵押来偿付它的贷款，但是会有被调整到可能无法偿付贷款的风险。结果来说，为了防止他们违约，就可能会对他们进行清算。

#### MEV 抵抗 - MEV-resistance

On Compound and Aave, liquidations are incentivised by offering up a borrower's collateral to liquidators at a fixed percentage discount, which typically ranges between 5-10%. One of the issues with this strategy is that would-be liquidators often have no choice but to engage in priority gas auctions (PGA) for profitable liquidations, which exposes the liquidation bonus as so-called miner extractable value (MEV) [(7)](white-paper.md#references). Another issue with this approach is that a fixed discount can be punitive for large liquidations, and therefore discourage large borrowers, whilst being insufficient to cover costs and incentivise smaller liquidations.

在 Compound 和 Aave 上，系统给出 5%-10%抵押物的折扣来奖励清算人。这个策略的问题之一就是清算人常常别无选择,只能为了进行有利润的清算而参与 Gas 优先拍卖（priority gas auctions,PGA），这样就引发了“矿工可提取价值”（ miner extractable value, MEV）的问题(7).。另一个问题是这样提供一个固定折扣的方法对大型清算成本过高，也（变相）阻碍了借款人（继续借款），同时小型清算又变得费用不足，激励不够。

To remedy these issues, Euler uses a different approach. Rather than a fixed discount percentage, we allow the discount to rise as a function of how under-water a position is. This turns a one-shot opportunity, where liquidators have no option but to engage in a PGA, into a type of Dutch auction. As the discount slowly increases, each would-be liquidator must decide whether or not to bid for a liquidation at the current discount on offer. Liquidator A might be profitable at 4%, but liquidator B might run a more efficient operation and be able to jump in sooner at 3.5%. The Dutch auction is aided by the TWAP oracles used on Euler, because a shock to the price does not bring with it a singular point at which every liquidator becomes profitable all at once. Instead the price moves more smoothly over time leading to a continuum of opportunities to liquidate, which further helps to limit PGAs. Overall, this process should help to drive the discount price towards the marginal operating cost of liquidating a borrower.

为了解决这些问题，Eluer 采用了不同的方式。我们不采用固定折扣，而是采用一个公式来确定某个仓位到底“缩水”多少。这是“一锤子买卖”，清算人从别无选择参与 PGA 变成参与一种荷兰式拍卖。随着折扣慢慢增加，每个有意参与的清算者必须在当前的折扣水平下做出是否参与的决断。清算人 A 也许在 4%折扣时就可以盈利，但是清算人 B 的行动效率可能更高，在 3.5%折扣的时候就会果断出手。荷兰式拍卖会受到 Euler 上 TWAP 预言机的协助，因为一个价格冲击并不会使得价格立刻到达一个每个清算人都会盈利的奇点。随着时间变长，价格只会变得更加平滑，从而产生一系列可以清算的机会，而这还会限制 PGA。总的来说，这个过程会使得折扣价格和清算借款人的边际成本趋同。

However, by itself, this process does not prevent MEV, because miners and front-runners can still steal a liquidator's transaction. To limit this form of MEV, we allow liquidity providers on Euler to make themselves eligible for a "discount booster", which allows them to become profitable in the Dutch auction before miners and front-runners (who do not have the booster).

然而，这个过程自身并不能防止 MEV，因为矿工和抢跑者可能会偷掉一笔清算人的交易。要限制这种 MEV，Euler 会给流动性提供者一个“折扣推进器”，让他们在荷兰拍卖期间就可以盈利（矿工和抢跑者则不行，因为没有这个“推进器”）。

#### 稳定池 - Stability Pools

On other lending protocols liquidations are usually processed using an external source of liquidity. That is, a liquidator will generally source the repayment amount of the borrowed assets from a third-party exchange, repay the loan, and receive the collateral and any bonus for themselves. One of the downsides of this approach is that the price feed used to determine the liquidation price of a borrower will not always accurately reflect the exchange rate on external markets, meaning that liquidators will not always be able to liquidate at that price. Reasons for this include slippage, swap fees, extreme volatility, the use of price-smoothing algorithms such as TWAP (as on Euler), and delays posting new prices.

在其他借贷协议中，清算中经常使用外部的流动性。也就是说，一个清算人一般会从第三方交易所借入资金，来偿付（被清算人的）债务，然后接管抵押物和奖励。这其中不好的一点，就是借款人的清算执行价格并不总是能准确反应外部市场的汇率，这意味着清算人并不能总是以这个价格执行清算。这种现象的原因有很多，比如滑点，交易费用，极端波动，TWAP 等算法的应用（Euler 也使用 TWAP），报价延迟等。

To alleviate this issue, Euler enables lenders to support liquidations by providing liquidity to a stability pool associated with each lending market. Liquidity providers in the stability pool deposit eTokens and earn interest whilst they wait for liquidations to be processed. An unstaking period prevents them from moving assets in and out of the pool to try to game the system. When a liquidation is processed the liquidator uses liquidity from the stability pool to cancel a borrower's debts and they return discounted collateral to the stability pool in return (minus a fee, which they keep for themselves). Stability pool liquidity providers essentially end up swapping their eTokens for a discounted index of collateral assets.

要解决这些问题，Euler 允许出借人对清算人提供支持，方式就是出借人向每个借贷市场的稳定池注入流动性。稳定池的流动性提供者存入 eTokens 然后获得利息，同时等待清算发生。为了保持系统稳定，不被恶意操纵，存入 eTokens 后需要一定时间之后才能提出。当一笔清算发生时，清算人将使用稳定池的资金来偿还借款人的债务，然后抵押物也会（按比例）存入稳定池（扣除归属清算人其他费用后）。稳定池的流动性提供者最终可以用 eTokens 交换（池中）相应的抵押物资产。

This approach can be thought of as an extended multi-collateral form of the stability pool idea pioneered by Liquity protocol [(8)](white-paper.md#references). The main advantage of using a stability pool is that liquidations can be processed immediately using an internal source of liquidity at the point at which a borrower is deemed by the protocol to be in violation, without a liquidator needing to source the assets themselves from a third-party exchange. See Table 1 for some of the benefits of performing liquidations using internal versus external liquidity.

这被认为是多渠道抵押稳定池形式的一种扩展， Liquity protocol (8) 是这方面的先驱。使用稳定池主要的好处是，在借款人因被认为“违约”而面临清算时，可以使用内部流动性来进行清算，清算人则不必向外部/第三方交易所寻求资源。具体的好处请查看表 1：

**Table 1.** Comparison of using an internal stability pool for liquidations rather than using an external source of liquidity.

|                      | External                                                                                                   | Internal                                                                                                     |
| -------------------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Liquidity source     | Liquidator typically purchases from a DEX or has existing source of funds themselves                       | Liquidator uses internal liquidity in the stability pool                                                     |
| Transaction costs    | Gas costs may be high for DEX trades and cross-contract calls                                              | Gas costs often relatively cheap for internal token transfers                                                |
| Explicit trade costs | Swap fees                                                                                                  | No swap fees                                                                                                 |
| Implicit trade costs | Slippage on illiquid markets                                                                               | No slippage                                                                                                  |
| Liquidation price    | Liquidation expected to take place at price determined by the wider market                                 | Liquidation expected to take place at price determined by the internal price feed                            |
| Liquidation timing   | Liquidation expected to take place only after the dynamic discount exceeds operating costs and trade costs | Liquidation expected to take place soon after the dynamic discount exceeds the operating cost of liquidation |

**Table 表 1.** 使用内部/外部资源进行清算的比较:

| 文字     | 外部                          | 内部                     |
| ------ | --------------------------- | ---------------------- |
| 清算资源   | 清算人大部分从其他 DEX 购入或者有外部资金支持   | 清算人使用稳定池的内部流动性         |
| 转账费用   | Gas 费用在不同的 DEX 或者智能合约间可能会很贵 | 内部转账的 gas 一般更加便宜       |
| 显性交易成本 | 闪兑（swap）费用                  | 没有闪兑（swap）费用           |
| 隐形交易成本 | 流动性不佳产生的滑点                  | 没有滑点                   |
| 清算价格   | 清算预计以外部价格（更广泛市场的价格）展开       | 清算预计以内部价格展开            |
| 清算时机   | 只能在动态折扣超过执行成本和交易成本后执行       | 动态折扣超过执行成本和交易成本后就能迅速执行 |

#### 软性清算 - Soft Liquidations

The fraction of a borrower's debt that can be paid off by liquidators in one go is referred to by Compound as the \`close factor.' On both Compound and Aave, the close factor is currently fixed at 0.5, meaning liquidators can pay off upto half a borrower's loan in one go regardless of how underwater their position is. This approach has a couple of potential drawbacks.

一个清算人能够一次性偿还借款人债务的比例在 Compound 上叫做“偿还因子”。在 Compound 和 Aave 上，偿还因子目前是固定的 0.5，这意味着清算人可以最多一次性偿还借款人 50%的贷款，不管借款人的抵押物如何“缩水”。这种方式有一些潜在的不宜之处。

First, allowing liquidators to liquidate half a loan could be considered excessive if a smaller liquidation would have been sufficient to bring the borrower back to health. Larger borrowers are likely to be put off by such a process. Second, a large fixed discount can sometimes drive a borrower closer to insolvency and disincentivise them from repaying their loans (see [(8)](white-paper.md#references)).

首先，如果一个小型清算就足以使得借款人的（仓位）回到健康状态，那让清算人清算一半的贷款就显得比较“过”了。规模大一些的借款人对样的清算方式可能不感兴趣。其次，一个大额固定折扣会让借款人更接近资不抵债的状况，从而打消他们偿还贷款的积极性。

On Euler, we therefore use a dynamic close factor to try to \`soft liquidate' borrowers. Specifically, we allow liquidators to repay up to the amount needed to bring a violator back out of violation (plus an additional safety factor). This means that borrowers who are only slightly in violation will often have much less than half their debts repaid during a liquidation, whilst borrowers who are heavily in violation will often have much more than half their debts repaid during a liquidation (their whole position might be closed in some circumstances).

在 Euler，我们选择采用动态偿还因子来对借款人进行软性清算。具体来说，我们允许清算人偿还债务到违约的临界点（再附加一些其他的安全因子修正）。这就意味着那些只是轻微违约的人在清算时往往偿还的比例要显著小于 50%，当然同时严重违约的借款人就要在清算时偿还显著高于 50%的比例（某些情况下仓位可能被关闭）

### 储备 - Reserves

In rare circumstances the value of a borrower's collateral might become less than the value of their liabilities. In this situation the borrower is said to be 'insolvent.' Insolvent borrowers will typically be liquidated repeatedly until they have little to no collateral left. Any leftover liabilities after liquidations have stopped can be considered 'bad debt' that we can assume will never be repaid. If bad debt accumulates on the protocol, it increases the chance that lenders might all rush at once to withdraw their funds (to avoid becoming the bearer of the bad debt). This phenomenon is known as \`run on the bank.'

在一些极少的情况下，借款人的抵押物（价值）会低于他们的债务。在这种情形下，借款人就“资不抵债”。资不抵债的借款人一般会被反复清算直到他们只有极少的抵押物留存。任何清算停止后还存留的债务就成为“坏账”，我们基本可以认为“坏账”无法清偿。如果池中的坏账持续累积，就会增加出借人挤兑的风险（为了避免成为坏账的最终承担者而在同一时间大量提出资产）。

To reduce this risk, Euler follows Compound by allowing a portion of the interest paid by borrowers in each market to accumulate into a reserve. The idea behind this is to allow the reserves to act as a lender of last resort in the event of a run on the bank. Providing that reserves accumulate at a faster pace than bad debt, lenders do not need to worry about being able to withdraw their funds. Euler reserves operate similar to those on Compound, except that Euler reserves are tracked in eToken units, rather than underlying units, which means that Euler reserves earn interest automatically whereas Compound reserves do not.

为了减少这个风险，Euler 向 Compound 取经，将借款人在市场中支付利息的一部分积累起来，成为了储备金。这么做背后的想法是当挤兑发生时让储备金成为最后的出借人。只要储备金的增速高于坏账的增速，那么出借人就没有必要担心是否能取出自己的资产。Euler 的储备金与 Compound 的类似，但 Euler 储备金以 eTokens 为单位来追踪（价格），而不是标的资产，这意味着 Euler 的储备金会自动获取利息，而 Compound 储备金则不会。

The proportion of interest paid into the reserves is called the \`reserve factor' and it is a parameter specific to each lending market. There are trade-offs to consider when setting the reserve factor. A reserve factor of zero would mean no reserves accrue, which could stifle lending because of the bad debt issue. Nevertheless, a high reserve factor would mean a large portion of interest is diverted away from lenders, which could also stifle lending as lenders seek a better rate elsewhere. Thus EUL holders may wish to use governance to select a reserve factor that balances these trade-offs for each type of asset.

利息存入储备金的比例就叫做“储备因子”，而且每个特定的借贷市场都不相同。设置储备因子有一些问题需要取舍。如果储备因子为 0，则意味着不归集储备金，这可能会因为坏账和伤害出借方（积极性）。然而，储备因子如果太高，那就意味着大部分的利息从出借方流失了，从而也会损伤出借方（积极性）——他们可能就去别的地方寻求更好的回报率了。所以，EUL（Euler 治理代币）的持币人可能就需要在治理时选择能够平衡上述情况的储备因子。

#### 清算的额外费用 - Liquidation Surcharge

During a liquidation, the liquidator is required to provide a slightly larger amount of the borrowed asset than is being repayed on behalf of the violator. This extra amount is contributed to the reserves for the borrowed asset as a fee. The base liquidation discount starts at the level of this fee, so it is ultimately paid by the violator.

As a result, more volatile assets, which generally trigger more liquidations, will tend to accrue reserves at a faster pace than less volatile assets helping to protect lenders of those assets. Additionally, this fee ensures that 'self-liquidating' is always net-negative, which adds a profitability threshold that some undesirable manipulation strategies are unlikely to meet.

在清算的时候，清算者需要代表违约者来证明已经借出的资产比要偿还的要稍微多一些。这些多余的就会当做已借资产的保证金费用。基础清算折扣就从这个费用的水平开始（计算），最后由违约者偿付。 最终，越来越多的违约资产会引发更多的清算，（也会）导致归集保证金的速度比更少违约资产保护出借人的速度快。此外，这个费用还保证了“自清算”永远为净负值，从而为我们不愿见到的某些市场操纵行为添加了利润上的门槛。

### 利率 - Interest Rates

Both Compound and Aave use static linear (or piecewise linear) interest rate models to guide the cost of borrowing on their protocols. Broadly speaking, as demand for borrowing from the pool increases or supply decreases, interest rates go up, and when supply increases or the demand for borrowing decreases, interest rates go down.

Static models work well if they are appropriately parameterised ahead of time, but can be problematic when parametrised incorrectly. For example, if the slope of the static linear function is too shallow, it can lead to the cost of borrowing being underpriced, with lenders unable to withdraw their assets because a pool has become over-utilised. On the other hand, if the slope of the static linear function is too steep, it can lead to the cost of borrowing being too expensive, which can stifle borrowing and lead to low capital efficiency.

Compound 和 Aave 都使用静态线性（或分段线性）利率模型来指导协议中的借款成本。宽泛地来说，随着池中借款需求的升高或者供给的降低，利率就会下降。 如果提前设置好了恰当的参数，静态模型就会较为有效，但如果参数设置不好，就会有问题。举例来说，如果静态线性函数的斜率太平缓，就会导致借款成本被低估，出借人就会因池中（资产）被超额使用而无法提现自己的资产。相反，如果斜率太陡，就会导致借款成本过高，妨害借款人借款，也影响出借人资金利用效率。

#### 回应式汇率 - Reactive Interest Rates

To avoid the problem of having to choose the right parameters for every lending market, Euler uses control theory to help autonomously guide the cost of borrowing towards a level that maximises capital efficiency on the protocol. Specifically, we use a PID controller to amplify (dampen) the rate of change in interest rates when utilisation is above (below) a target level of utilisation. This gives rise to reactive interest rates that adapt to market conditions for the underlying asset in real-time without the need for ongoing governance intervention. A similar approach has also recently been described by the Delphi Labs team [(9)](white-paper.md#references).

为了避免强行为每个借贷市场都单独设定“正确”的参数（因为这样做耗费精力和各项成本都很巨大），Euler 采用了控制论来帮助指导借款成本达到一个最大化资本利用率的水平。具体来说，当利用率高于某个目标水平时，我们使用一个 PID 控制器来调整利率变化的幅度。无需持续干涉，就提升了回应式利率实时响应标的资产市场情况的能力(9)。

#### 复利 - Compound Interest

Compound interest is accrued on Euler on a per-second basis. This differs from other lending protocols, where interest is typically accrued on a per-block basis. A per-second basis is generally expected to perform more predictably in the long-run even if upgrades to Ethereum lead to changes in the average time between blocks.

Euler 上的复利是按秒归集的。这就和其他以区块归集复利的借贷协议不一样。以秒计算从长期来看更加有可预测性，即使因以太坊更新导致按区块间平均（出块）时间来计算。

#### 最优化 - Gas Optimisations

Euler’s smart contracts minimise the amount of storage used, implement a module system to reduce the amount of cross-contract calls, and have had a number of other gas usage optimisations applied. This makes the protocol cheaper on most operations than other lending protocols.

Euler 的智能合约将存储用量最小化，并且实施了一个模块系统来减少智能合约间的（无效）交互，（除了这些）还应用了一系列其他优化 gas 的措施。这使得整个协议在大部分运营成本上都比其他协议更廉价。

#### 交易建设者 - Transaction Builder

The user interface includes a convenient tool to help users batch up multiple transactions and reduce their gas costs, which we call a transaction builder. Advanced users can use this feature in conjunction with a defer liquidity option provided on the protocol to rebalance loans or perform flash loans.

用户界面包含了一套方便的，被称作交易建设者的工具来帮助用户管理多笔交易和减少 gas 费用。高级用户可以利用这个特性，来连接协议提供的延期清算选项，从而实现贷款的再平衡或实行闪贷。

#### 子账号 - Sub-accounts

Asset tiers help to isolate risks on Euler, but they open up a new user-experience problem. Specifically, it would quickly become cumbersome for borrowers to use Euler if they had to send collateral to a new Ethereum account for each new isolation-tier loan they wanted to take out.

Euler therefore enables every Ethereum account using the protocol to access up to 256 sub-accounts (including the primary account), which can be used to cost-effectively manage multiple positions at the same time. A user only needs to approve Euler's access to a token once and can then deposit into any sub-account. Additionally, no approvals are required to transfer assets and liabilities between sub-accounts, which allows users to isolate and segregate their collateral and debts as desired.

资产分层帮助隔离 Euler 上的风险，但是产生了一个用户体验的新问题。具体来说，如果用户每次都要把抵押物转账到新的以太账号上，那确实太繁琐了。Euler 于是采用了一个可以同时有效管理多账号的新办法：允许每个使用（Euler）协议的以太账号使用最多 256 个账号（含主账号）。除此之外，子账号之间转移资产和债务是不需要批准的，这也使得用户能按照自己的意愿隔离和配置他们的资产和债务。

### 治理 - Governance

Euler will broadly follow the governance model pioneered by Compound [(10)](white-paper.md#ref10). The protocol will be managed by holders of a protocol native governance token called Euler Governance Token (EUL). EUL tokens will represent voting shares. Holders with enough EUL tokens will be able to make a formal proposal for change on the protocol. Token holders will then be able to vote on the proposal themselves or delegate their vote shares to a third party. Examples of the kinds of decisions token holders might vote on include proposals to alter include:

* The tier of an asset
* Collateral and borrow factors
* Price oracle parameters
* Reactive interest rate model parameters
* Reserve factors
* Governance mechanisms themselves

Euler 在治理方面会较多采用 Compound (10) 提出和发展的一些方式。Euler 会被持有原生治理代币 Euler Governance Token (EUL)的人管理。EUL 代币将代表投票的比例。有足够数量 EUL 代币的人能够提出改变协议（治理）的正式提案。代币持有人也能够将投票权让渡给第三方。以下是持币人可能投票的内容：

* 资产分层
* 抵押物和借款因子
* 价格预言机参数
* 回应式利率模型的参数
* 储备因子
* 治理机制本身

### 鸣谢 - Acknowledgements

With special thanks to [Shaishav Todi](https://twitter.com/shaishav0x), [Luke Youngblood](https://twitter.com/LukeYoungblood), [Charlie Noyes](https://twitter.com/\_charlienoyes), [samczsun](https://twitter.com/samczsun), [Hasu](https://twitter.com/hasufl), [Dave White](https://twitter.com/\_Dave\_\_White\_), [Rick Pardoe](https://twitter.com/rick\_liquity), Ayana Aspembitova and the [Delphi Labs](https://twitter.com/Delphi\_Digital) team, [Mariano Conti](https://twitter.com/nanexcool), Lev Livnev, and [Chainguys](https://twitter.com/Chainguys).

特别感谢以下诸位 [Shaishav Todi](https://twitter.com/shaishav0x), [Luke Youngblood](https://twitter.com/LukeYoungblood), [Charlie Noyes](https://twitter.com/\_charlienoyes), [samczsun](https://twitter.com/samczsun), [Hasu](https://twitter.com/hasufl), [Dave White](https://twitter.com/\_Dave\_\_White\_), [Rick Pardoe](https://twitter.com/rick\_liquity), Ayana Aspembitova and the [Delphi Labs](https://twitter.com/Delphi\_Digital) team, [Mariano Conti](https://twitter.com/nanexcool), Lev Livnev, and [Chainguys](https://twitter.com/Chainguys).

### 引用文献 - References

1. [https://docs.ethhub.io/built-on-ethereum/open-finance/what-is-open-finance/](https://docs.ethhub.io/built-on-ethereum/open-finance/what-is-open-finance/)
2. [https://compound.finance/documents/Compound.Whitepaper.pdf](https://compound.finance/documents/Compound.Whitepaper.pdf)
3. [https://github.com/aave/aave-protocol/blob/master/docs/Aave\_Protocol\_Whitepaper\_v1\_0.pdf](https://github.com/aave/aave-protocol/blob/master/docs/Aave\_Protocol\_Whitepaper\_v1\_0.pdf)
4. [https://uniswap.org/whitepaper-v3.pdf](https://uniswap.org/whitepaper-v3.pdf)
5. [https://weth.io/](https://weth.io)
6. [https://www.theblockcrypto.com/post/82721/makerdao-issues-warning-after-a-flash-loan-is-used-to-pass-a-governance-vote](https://www.theblockcrypto.com/post/82721/makerdao-issues-warning-after-a-flash-loan-is-used-to-pass-a-governance-vote)
7. [https://research.paradigm.xyz/MEV](https://research.paradigm.xyz/MEV)
8. [https://docsend.com/view/bwiczmy](https://docsend.com/view/bwiczmy)
9. [https://members.delphidigital.io/reports/dynamic-interest-rate-model-based-on-control-theory](https://members.delphidigital.io/reports/dynamic-interest-rate-model-based-on-control-theory)
10. [https://medium.com/compound-finance/compound-governance-5531f524cf68](https://medium.com/compound-finance/compound-governance-5531f524cf68)
