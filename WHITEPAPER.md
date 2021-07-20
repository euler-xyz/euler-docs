# Euler Docs

## Table of contents
1. [Introduction](#introduction)
2. [Accessing Euler](#accessing-euler)
      1. [Transaction Builder](#transaction-builder)
3. [Permissionless Listing](#permissionless-listing)
      1. [Asset Tiers](#asset-tiers)
      2. [Sub-accounts](#sub-accounts)
4. [Lending and Borrowing](#lending-and-borrowing)
      1. [Tokenised Debts](#tokenised-debts)
      2. [eToken/dToken Symmetry](#etoken-dtoken-symmetry)
      3. [Optional Collateral Lending](#optional-collateral-lending)
      4. [Defer Liquidity](#defer-liquidity)
      5. [Feeless Flash Loans](#feeless-flash-loans)
      6. [Risk-adjusted Borrowing Capacity](#risk-adjusted-borrowing-capacity)
5. [Decentralised Price Oracles](#decentralised-price-oracles)
      1. [TWAP](#twap)
      2. [Time Interval](#time-interval)
6. [Liquidations](#liquidations)
      1. [MEV-resistance](#mev-resistance)
      2. [Stability Pools](#stability-pools)
      3. [Soft Liquidations](#soft-liquidations)
7. [Reserves](#reserves)
      1. [Liquidation Surcharge](#liquidation-surcharge)
8. [Interest Rates](#interest-rates)
      1. [Reactive Interest Rates](#reactive-interest-rates)
      2. [Compound Interest](#compound-interest)
9. [Smart Contracts](#smart-contracts)
      1. [Gas Optimisations](#gas-optimisations)
10. [Governance](#governance)
11. [Summary](#summary)
12. [Acknowledgements](#acknowledgements)
13. [Definitions](#definitions)

## Introduction

The ability to lend and borrow assets efficiently is a crucial feature of any financial system. In the world of traditional finance, this process is typically facilitated by trusted and permissioned third-parties such as banks, who connect people with a surplus of money to those who need access to it in the short-term. In the world of decentralised finance (DeFi), trusted and permissioned third-parties are no longer needed; banks have been replaced by trustless and permissionless lending protocols running on the blockchain. 

Among the first-generation of DeFi lending protocols are \textbf{\hrefc{https://whitepaper.io/document/586/compound-whitepaper{Compound and \textbf{\hrefc{https://whitepaper.io/document/533/aave-whitepaper{Aave. These protocols provide users with access to lending and borrowing capabilities for a handful of the most liquid ERC-20 tokens. However, these protocols were not designed to handle the risks associated with lending and borrowing illiquid or volatile assets and have therefore relied on a permissioned listing system to protect their users from the risks associated with such assets. 

Consequently, there remains significant unmet demand for lending and borrowing a much wider range of crypto assets. On the lending side, users want to deposit tokens to earn yield and take leveraged long positions. On the borrowing side, users want to reduce their exposure from holding locked tokens and take leveraged short positions. 

Here, we present Euler: a permissionless lending protocol custom-built with an array of new features to help users lend and borrow more tokens than ever before. Euler is managed by holders of a protocol native governance token called Euler Governance Token (EUL). The purpose of this white paper is to describe how Euler works at a high level and highlight new features and innovations that help to set it apart from other popular lending protocols, like Compound and Aave. 

<a name="accessing-euler"></a>
## Accessing Euler

Euler comprises a set of smart contracts deployed on the Ethereum blockchain that can be openly accessed by anyone with an internet connection. Euler is entirely non-custodial; users are responsible for managing their own funds. 

As creators of the protocol, the development team at Euler XYZ have provided a convenient and user-friendly front-end to the Euler smart contracts at \textbf{\url{https://www.euler.xyz. However, users are free to access the protocol in whatever format they wish. 

<a name="transaction-builder"></a>
### Transaction Builder

The user interface includes a convenient tool to help users batch up multiple transactions and reduce their gas costs, which we call a \textbf{transaction builder. Advanced users can use this feature in conjunction with a \textbf{defer liquidity option provided on the protocol to rebalance loans or perform \textbf{flash loans.

<a name="permissionless-listing"></a>
## Permissionless Listing

Euler lets its users determine which assets are listed. Any asset that has a WETH pair on Uniswap v3 can be added as a lending market on Euler by anyone straight away. 

<a name="asset-tiers"></a>
### Asset Tiers

Permissionless listing is much riskier on decentralised lending protocols than on other DeFi protocols, like decentralised exchanges, because of the potential for risk to spill over from one pool to another in quick succession. The biggest risk of contagion is posed by collateral assets suddenly dropping in price, because these will often leave borrowers from multiple pools under-collateralised. However, a sudden increase in the value of a borrowed asset also has the potential to leave borrowers unable to repay debts from multiple pools if they have borrowed multiple assets at once using the same pool of collateral. To counter these challenges, Euler uses risk-based \textbf{asset tiers to protect protocol users. 

\textbf{Isolation-tier assets are generally newly listed assets on Euler and are assumed to pose the biggest threat because they are an unknown quantity. As such, these assets are available for ordinary lending and borrowing, but they cannot be used as collateral to borrow other assets and they can only be borrowed in isolation. 

\textbf{Cross-tier assets are generally better-known assets that are assumed to be non-malicious and have been deemed to be safe enough to be borrowed alongside other assets.

\textbf{Collateral-tier assets are generally highly liquid assets with low volatility. They include stablecoins and `blue chip' DeFi tokens. Collateral assets pose the biggest threat to the protocol. Promotion to the top-tier therefore requires careful consideration. 

EUL holders can vote to liberate assets from the isolation-tier and promote them to the cross-tier or collateral-tier through governance mechanisms. Promoting assets up the tiers increases capital efficiency on Euler, because it allows lenders and borrowers to use capital more freely, but it may also expose protocol users to increased risk. It is therefore in EUL holders interests to balance these concerns. 

<a name="sub-accounts"></a>
### Sub-accounts

Asset tiers help to isolate risks on Euler, but they open up a new user-experience problem. Specifically, it would quickly become cumbersome for borrowers to use Euler if they had to send collateral to a new Ethereum account for each new isolation-tier loan they wanted to take out. 

Euler therefore enables every Ethereum account using the protocol to access up to 256 sub-accounts (including the primary account), which can be used to cost-effectively manage multiple positions at the same time. A user only needs to approve Euler's access to a token once and can then deposit into any sub-account. Additionally, no approvals are required to transfer assets and liabilities between sub-accounts, which allows users to isolate and segregate their collateral and debts as desired.

<a name="lending-and-borrowing"></a>
## Lending and Borrowing

When lenders provide liquidity to a pool on Euler, they receive interest-bearing ERC-20 eTokens in return, which can be redeemed for the underlying asset at any time, as long as there are unborrowed tokens in the pool (similar to Compound's cTokens). Tokenising supply in this way provides a convenient accounting scheme for recording the fraction of the total assets in a pool that are owned by a particular lender. 

Borrowers take liquidity out of a pool and return it with interest. Thus, the total assets in the pool grows through time. This is monitored at the smart contract level by an interest rate accumulator. A census of the accumulator is recorded for each borrower whenever they borrow from the protocol, which allows Euler to calculate how much the owe. In this way, lenders earn interest on the assets they supply, because their eTokens can be redeemed for an increasing amount of the underlying asset over time. 

<a name="tokenised-debts"></a>
### Tokenised Debts

Similarly to Aave, Euler also tokenises debts on the protocol with ERC-20-compliant interfaces known as dTokens. The dToken interface allows the construction of positions without needing to interact with underlying assets and can be used to create derivative products that include debt obligations.

Rather than providing non-standard methods to transfer debts, Euler uses the regular transfer/approve ERC-20 methods. However, the permissioning logic is reversed: rather than being able to send tokens to anyone, but requiring approval to take them, dTokens can be taken by anyone, but require approval to accept them. This also prevents users from "burning" their dTokens. For example, the zero address has no way of approving an in-bound transfer of dTokens.

Borrowers pay interest on their loans in terms of the underlying asset. The interest accrued depends on an algorithmically determined interest rate for each asset. A portion of the interest accrued is held in reserves to cover the accumulation of bad debts on the protocol.

<a name="etoken-dtoken-symmetry"></a>
### eToken/dToken Symmetry

The primary operations on eTokens and dTokens are deposit/withdraw and borrow/repay, respectively. However, there is another interface that in some ways is more fundamental: mint/burn. These operations work on both eTokens and dTokens simultaneously. A mint operation creates both eTokens and dTokens in equivalent amounts, and assigns both to the user. A burn operation destroys eTokens and dTokens in equivalent amounts. These operations can be thought of as borrowing from yourself and repaying yourself. Alternatively, eTokens and dTokens can be thought of as a sort of matter and anti-matter, appearing from "nowhere" when minted (no underlying tokens required) and cancelling one another out of existence when burned.

All of the primary operations can be re-conceptualised as variants of mint and burn. For example, if there were no borrow function, it could be implemented in terms of a mint and a withdraw: the mint would create both eTokens and dTokens, and then the withdraw would destroy the eTokens leaving just dTokens.

* deposit: mint, repay
* withdraw: borrow, burn
* borrow: mint, withdraw
* repay: deposit, burn

There are some practical advantages with the mint and burn operations. One of which is that it becomes possible to repay a loan with eTokens instead of the underlying by burning a corresponding amount of eTokens together with the dTokens from the loan. This may be useful when the underlying token is illiquid -- perhaps because it has been paused -- but there is still a market for eTokens (incidentally, the stability pools described in the liquidation section are examples of eToken to eToken markets).

Eventually Euler will implement a module that allows users to swap one eToken for another, by performing an external swap on Uniswap. This will save users gas by avoiding deposit/withdraw overhead. When combined with mint, this will allow users to construct leveraged positions without any underlying token ever transiting their wallet.

Another area where the eToken/dToken symmetry is exposed is liquidations. Instead of the liquidator sending borrowed tokens and receiving collateral, Euler's liquidation flow simply transfers borrowed dTokens and collateral eTokens from the violator to the liquidator. The liquidator will typically withdraw the collateral, exchange it, and then repay to destroy the dTokens, but this is not strictly necessary. The liquidator could choose to retain the debt if, for example, there is insufficient available collateral tokens in the pool, or the swapping conditions are temporarily sub-optimal.

<a name="optional-collateral-lending"></a>
### Optional Collateral Lending

On Compound and Aave, collateral deposited to the protocol is always made available for lending. Optionally, Euler allows collateral to be deposited, but not made available for lending. Such collateral earns a user no interest, but is free from the risks of borrowers defaulting, can always be withdrawn instantly, and helps protect against borrowers using tokens to influence governance decisions or take short positions. 

<a name="defer-liquidity"></a>
### Defer Liquidity

Normally, an account's liquidity is checked immediately after performing an operation that could fail due to insufficient collateral. For example, taking out a borrow, withdrawing collateral, or exiting a market could cause a transaction be reverted due to to a collateral violation.

However, Euler has a feature that allows users to defer their liquidity checks. Many operations can be performed and the liquidity is checked only once at the very end. For example, without deferring liquidity checks, a user must first deposit collateral before issuing a borrow. However, if done in the same transaction, deferring the liquidity check will allow the user to do this in any order.

<a name="feeless-flash-loans"></a>
### Feeless Flash Loans

Unlike AAVE, Euler doesn't have a native concept of flash loans. Instead, users can defer their liquidity check, make an uncollateralised borrow, perform whatever operation they like, and then repay the borrow. This can be used to rebalance positions, build-up leveraged positions, take advantage of external arbitrage opportunities, and more.

Because Euler only charges fees according to the time value of money, and from the blockchain's perspective flash loans are held for a duration of 0 seconds, they are entirely free on Euler (ignoring gas costs). We believe that flash loan fees are ultimately in a race to the bottom that will be accelerated by advances like flash minting. The ecosystem benefits gained from simple and free flash loans outweigh the relatively modest benefit from flash loan fees.

<a name="risk-adjusted-borrowing-capacity"></a>
### Risk-adjusted Borrowing Capacity

Like other lending protocols, Euler requires users to ensure that the value of their collateral remains higher than the value of their liabilities (except during the intermediate period when liquidity checks have been deferred). Over-collateralisation is encouraged by limiting how much borrower's can take out as a loan in the first place. 

Compound achieves this in a one-sided way by using collateral factors to adjust down the value of a borrower's collateral assets when deciding how much they can borrow. This gives rise to a \textbf{risk-adjusted collateral value that helps to create a buffer that can be drawn upon by liquidators in the event that the value of a borrower's assets and liabilities changes over time. One of the problems with this approach is that it only adjusts for the risks associated with a borrower's collateral assets decreasing in value. There may be an asymmetric risk, however, of the borrower's liabilities increasing in value. This risk is not factored in to the collateral factors. 

On Euler, we therefore use a two-sided approach where we also adjust \textit{up the market value of a borrower's liabilities to arrive at a \textbf{risk-adjusted liability value. This approach improves capital efficiency on the protocol because it allows Euler to factor in the asset-specific risks of both downside and upside price movements. These risks are encapsulated in asset-specific \textbf{collateral factors (as on Compound) and \textbf{borrow factors (new to Euler). Ultimately, this approach means that the liquidation threshold of every borrower is tailored to the specific risk profiles associated with the assets they are borrowing and using as collateral.

<a name="decentralised-price-oracles"></a>
## Decentralised Price Oracles

To be able to calculate whether a loan is over-collateralised or not, Euler needs to monitor the value of users' assets. On Compound, Maker, and Aave, various systems are used to get prices from off-chain sources and put them on-chain so that they can be accessed by the relevant smart contracts. 

This approach is unsuitable for Euler's purposes because it requires centralised intervention whenever a new lending market needs to be created. Euler therefore relies on Uniswap v3's decentralised time-weighted average price (TWAP) oracles to assess the solvency of users. The reference asset used to normalise prices on Euler is Wrapped Ether (WETH), which is the most common base pair on Uniswap. 

<a name="twap"></a>
### TWAP

Uniswap TWAP is calculated using the geometric mean price of an asset over some interval of time. TWAP in general is both a smoothed and lagging indicator of the trade price: a TWAP over a short interval is a less smooth function, but more up-to-date, whilst a TWAP over a long interval is a smoother function, but less up-to-date. TWAP is ideal for Euler's purposes for several reasons. 

First, TWAP is resistant to price manipulation attacks. It cannot be manipulated within a transaction or block (for example with flash loans or flash bots), because it is calculated using historic data. It is also expensive to manipulate using large market orders, because the manipulated price must be maintained for some period of time relative to the TWAP time interval. During this time, other users can take advantage of the manipulated price with arbitrage which will cause it to revert back to the broader market price. Arbitrage is especially practical on the blockchain because arbitrageurs have access to large amounts of capital (including from flash loans) and the atomic nature of transactions means that arbitrage transactions have a low execution risk. For these reasons, manipulating the price on a single decentralised exchange usually requires more widespread manipulation of all on-chain exchanges simultaneously, although even this can't prevent the (less practical but still possible) arbitrage between on and off-chain exchanges.

Second, the smooth nature of TWAP helps to remove the impact of price shocks on borrowers. In the event of a large trade, the current price on Uniswap can be moved significantly. Usually arbitrage bots will quickly converge this to the broader market value, so the maximum deviation of the TWAP will only be a fraction of the temporary price movement. This prevents some unnecessary liquidations and loans that may quickly become undercollateralised.

Third, instead of instantly jumping between two price levels, TWAPs change continuously, second-by-second. This property is used by Euler's liquidation process to implement Dutch auctions that reduce the value captured by miners and front-running bots.

<a name="time-interval"></a>
### Time Interval

One of the challenges in using TWAP is determining the right interval over which it should be calculated for a given asset. The trade-offs involved with shorter (longer) intervals may sometimes need to be taken into consideration and altered for specific assets. Euler therefore allows the default time interval to be updated by governance if EUL holders deem it necessary. 

TODO: Doug to include feedback stuff.

<a name="liquidations"></a>
## Liquidations

A borrower is considered to be in violation on Euler when the value of their risk-adjusted liabilities exceeds the value of their risk-adjusted collateral. A borrower that has just become in violation still has enough collateral to repay their loan, but is adjudged to be at risk of defaulting on their loan. Consequently, they may be liquidated in order to limit the potential for them to default. 

<a name="mev-resistance"></a>
### MEV-resistance

On Compound and Aave, liquidations are incentivised by offering up a borrower's collateral to liquidators at a fixed percentage discount, which typically ranges between 5-10\%. One of the issues with this strategy is that would-be liquidators often have no choice but to engage in priority gas auctions (PGA) for profitable liquidations, which exposes the liquidation bonus as miner extractable value (MEV). Another issue with this approach is that a fixed discount can be punitive for large liquidations, and therefore discourage large borrowers, whilst being insufficient to cover costs and incentivise smaller liquidations. 

To remedy these issues, Euler uses a dynamic liquidation discount coupled with a discount booster for liquidity providers on the protocol. This turns a one-shot opportunity, where liquidators have no option but to engage in a PGA, into a type of Dutch auction. The idea is that the discount on offer to liquidators rises as a function of how under water a borrower has become. As the discount slowly increases, each would-be liquidator must decide whether or not to bid for a liquidation at the current discount on offer. Liquidator A might be profitable at 4\%, but liquidator B might run a more efficient operation and be able to jump in sooner at 3.5\%. 

The Dutch auction is aided by the TWAP oracles used on Euler, because a shock to the price does not bring with it a singular point at which every liquidator becomes profitable all at once. Instead the price moves more smoothly over time leading to a continuum of opportunities to liquidate. This further helps to limit PGAs. 

Assuming the liquidation market is reasonably efficient, the Dutch auction should also help to drive the discount price towards the marginal operating cost of liquidating a borrower. With this approach a \$1M position is likely to be liquidated at a lower percentage discount than a \$1K position. It should also mean that discounts rise and fall with the price of gas on Ethereum.

Liquidators can make themselves eligible for a discount booster by allowing Euler to track their moving average liquidity on the protocol. The maximum boost is achieved by users who have liquidity on the protocol that is greater than or equal to the value of the liquidation repayment amount. The discount booster increases the rate at which the dynamic liquidation discount increases over time. It should help to reduce MEV by providing liquidity providers on Euler with a period of time to liquidate in the Dutch auction in which they are profitable, but miners and other competitors using front-running bots are not.  

<a name="stability-pools"></a>
### Stability Pools

On other lending protocols liquidations are usually processed using an external source of liquidity. That is, a liquidator will generally source the repayment amount of the borrowed assets from a third-party exchange, repay the loan, and receive the collateral and any bonus for themselves. 

One of the downsides of this approach is that the price feed used to determine the liquidation price of a borrower will not always accurately reflect the exchange rate on external markets, meaning that liquidators will not always be able to liquidate at that price. Reasons for this include slippage, swap fees, extreme volatility, the use of price-smoothing algorithms such as TWAP (as on Euler), and delays posting new prices. 

To alleviate this issue, Euler enables lenders to support liquidations by providing liquidity to a stability pool associated with each lending market. Liquidations can then be processed using this internal source of liquidity at the point at which a borrower becomes underwater, without a liquidator needing to source the assets themselves from a third-party exchange. The liquidation can take place quickly and efficiently at the liquidation price determined by the price feed on Euler.

Liquidity providers in the stability pool deposit eTokens and earn interest whilst they wait for liquidations to be processed. An unstaking period prevents them from moving assets in and out of the pool to try to game the system. When a liquidation is processed the liquidator uses liquidity from the stability pool to cancel a borrower's debts and returns discounted collateral to the stability pool in return. The liquidator keeps the dynamic liquidation discount themselves as a service fee. 

Stability pool liquidity providers are rewarded with a fixed stability pool discount relative to the liquidation price of the borrower whenever a liquidation happens. Note that unlike the fixed liquidation discount used on other protocols, this discount is not vulnerable to front-running by another liquidator or a miner, since the bonus it provides is always returned to one place, the stability pool. 

Lenders depositing to the stability pool effectively operate as a kind of market maker. The idea is that they will profit on most liquidations from the artificial spread created by the liquidation discount, but occasionally sell their assets at a sub-optimal price relative to the external exchange rate when the Euler price feed is not in sync with wider market conditions. 

This liquidation path is the preferred method of liquidation on Euler, and liquidators are expected to preferentially use the stability pool rather than a third-party exchange for liquidations. The reason for this is that liquidators can access liquidity from the stability pool without fees or slippage costs, and are therefore likely to be able to profitably liquidate borrowers at a lower dynamic discount percentage than they otherwise would if they used an external source of liquidity. See Table 1 for some of the benefits of performing liquidations using internal versus external liquidity. 

\begin{table[!htbp]
\caption{\textbf{Comparison of using an internal stability pool for liquidations rather than using an external source of liquidity.
\begin{tabular{|l|p{6cm|p{6cm|
\hline
                              & \textbf{External            & \textbf{Internal\hline
\textbf{Liquidity source &
  Liquidator typically purchases from a DEX or has existing source of funds themselves &
  Liquidator uses internal liquidity in the stability pool\hline
\textbf{Transaction costs &
  Gas costs may be high for DEX trades and cross-contract calls &
  Gas costs often relatively cheap for internal token transfers\hline
\textbf{Explicit trade costs & Swap fees                    & No swap fees     \hline
\textbf{Implicit trade costs & Slippage on illiquid markets & No slippage      \hline
\textbf{Liquidation price &
  Liquidation expected to take place at price determined by the wider market &
  Liquidation expected to take place at price determined by the internal price feed\hline
\end{tabular
\end{table

<a name="soft-liquidations"></a>
### Soft Liquidations

The fraction of a borrower's debt that can be paid off by liquidators in one go is referred to by Compound as the `close factor.' On both Compound and Aave, the close factor is currently fixed at 0.5, meaning liquidators can pay off upto half a borrower's loan in one go regardless of how underwater their position is. This approach has a couple of potential drawbacks. 

First, allowing liquidators to liquidate half a loan could be considered excessive if a smaller liquidation would have been sufficient to bring the borrower back to health. Larger borrowers are likely to be put off by such a process. Second, a large fixed discount can sometimes drive a borrower closer to insolvency and disincentivise them from repaying their loans (see REF). 

On Euler, we therefore use a dynamic close factor to try to `soft liquidate' borrowers. Specifically, we allow liquidators to repay up to the amount needed to bring a violator back out of violation (plus an additional safety factor). This means that borrowers who are only slightly in violation will often have much less than half their debts repaid during a liquidation, whilst borrowers who are heavily in violation will often have much more than half their debts repaid during a liquidation (their whole position might be closed in some circumstances). 

<a name="reserves"></a>
## Reserves

In rare circumstances the value of a borrower's collateral might become less than the value of their liabilities. In this situation the borrower is said to be 'insolvent.' Isolvent borrowers will typically be liquidated repeatedly until they have little to no collateral left. Any leftover liabilities after liquidations have stopped can be considered `bad debt' that we can assume will never be repaid. If bad debt accumulates on the protocol, it increases the chance that lenders might all rush at once to withdraw their funds (to avoid becoming the bearer of the bad debt). This phenomenon is known as `run on the bank.'

To reduce this risk, Euler follows Compound by allowing a portion of the interest paid by borrowers in each market to accumulate into a reserve. The idea behind this is to allow the reserves to act as a lender of last resort in the event of a run on the bank. Providing that reserves accumulate at a faster pace than bad debt, lenders do not need to worry about being able to withdraw their funds. Euler reserves operate similar to those on Compound, except that Euler reserves are tracked in eToken units, rather than underlying units, which means that Euler reserves earn interest automatically whereas Compound reserves do not. 

The proportion of interest paid into the reserves is called the `reserve factor' and it is a parameter specific to each lending market. There are trade-offs to consider when setting the reserve factor. A reserve factor of zero would mean no reserves accrue, which could stifle lending because of the bad debt issue. Nevertheless, a high reserve factor would mean a large portion of interest is diverted away from lenders, which could also stifle lending as lenders seek a better rate elsewhere. Thus EUL holders may wish to use governance to select a reserve factor that balances these trade-offs for each type of asset. 

<a name="liquidation-surcharge"></a>
### Liquidation Surcharge

During a liquidation, the liquidator is required to provide a slightly larger amount of the borrowed asset than is being repayed on behalf of the violator. This extra amount is contributed to the reserves for the borrowed asset as a fee. The base liquidation discount starts at the level of this fee, so it is ultimately paid by the violator.

As a result, more volatile assets, which generally trigger more liquidations, will tend to accrue reserves at a faster pace than less volatile assets helping to protect lenders of those assets. 

Additionally, this fee ensures that liquidating your own positions from another account ("self-liquidating") is always net-negative, which adds a profitability threshold that some undesirable strategies are unlikely to meet.

<a name="interest-rates"></a>
## Interest Rates

Both Compound and Aave use static linear (or piecewise linear) interest rate models to guide the cost of borrowing on their protocols. Broadly speaking, as demand for borrowing from the pool increases or supply decreases, interest rates go up, and when supply increases or the demand for borrowing decreases, interest rates go down. 

Static models work well if they are appropriately parameterised ahead of time, but can be problematic when parametrised incorrectly. For example, if the slope of the static linear function is too shallow, it can lead to the cost of borrowing being underpriced, with lenders unable to withdraw their assets because a pool has become over-utilised. On the other hand, if the slope of the static linear function is too steep, it can lead to the cost of borrowing being too expensive, which can stifle borrowing and lead to low capital efficiency. 

<a name="reactive-interest-rates"></a>
### Reactive Interest Rates

To avoid the problem of having to choose the right parameters for every lending market, Euler uses control theory to help autonomously guide the cost of borrowing towards a level that maximises capital efficiency on the protocol. Specifically, we amplify or dampen the \textit{rate of change in interest rates when utilisation is excessively high or particularly low. This gives rise to \textbf{reactive interest rates that adapt to market conditions for the underlying asset in real-time without the need for ongoing governance intervention. 

<a name="compound-interest"></a>
### Compound Interest

Compound interest is accrued on Euler on a per-second basis. This differs from Compound, where interest is accrued on a per-block basis. A per-second basis is generally expected to perform more predictably in the long-run even if upgrades to Ethereum lead to changes in the average time between blocks. 

<a name="smart-contracts"></a>
## Smart Contracts

TODO: Doug maybe a brief word on any cool architecture stuff?

<a name="gas-optimisations"></a>
### Gas Optimisations

Euler’s smart contracts minimise the amount of storage used, implement a module system to reduce the amount of cross-contract calls, and have had a number of other gas usage optimisations applied. This makes the protocol cheaper on most operations than other lending protocols.

<a name="governance"></a>
## Governance

Euler follows Compound's governance model. The protocol is managed by holders of a protocol native governance token called Euler Governance Token (EUL). EUL tokens represent voting shares. Holders with enough EUL tokens can make a formal proposal for change on the protocol. Token holders can then vote on the proposal themselves or delegate their votes to a third party. Examples of the kinds of decisions token holders might vote on include proposals to alter include:

* The tier of an asset
* Collateral and borrow factors
* Price oracle parameters
* Reactive interest rate model parameters
* Reserve factors
* Governance mechanisms themselves

<a name="summary"></a>
## Summary

<a name="acknowledgements"></a>
## Acknowledgements

We would like to thank all those people who reviewed earlier drafts of this document or who took the time to answer our questions. Special thanks go to Shaishav Todi, Lev Livnev, Luke Youngblood, Rick Pardoe, Charlie Noyes, Dan Robinson

<a name="definitions"></a>
## Definitions

 * Liquidity pool:
 * Permissionless lending: 
 * Perpetual loan: loan take over a period of several blocks, but without a specified repayment date.
 * Flash loan: loan taken from a liquidity pool that is repayable within the same atomic transaction.
 * Time-weighted average price (TWAP): the average price of an asset calculated over some historical interval of time.  
 * Collateral factor: parameter that governs what percentage of the market value of an asset can be used as collateral for borrowing.
 * Borrow factor: parameter that governs by what percentage a user must over-collateralise in order to borrow an asset. 
 * Over-collateralised: state in which a user has provisioned more collateral value than their liability value.
 * Under-collateralised: state in which a user has not provisioned enough collateral value to cover their liabilities. 
 * Insolvency: a state in which the market value of a user's collateral is worth less than the market value of their liabilities, meaning they no longer have an incentive to repay their loan.
 * Health score: The ratio of a user's collateral value to the value of their liabilities. When above 1, it means they are over-collateralised. When below 1, it means they are under-collateralised.
 * Collateral value: The value of a user's collateral that can be used to borrow other assets. It is calculated as the market value of a user's collateral multiplied by the relevant collateral factors. 
 * Liability value: The value of a user's borrows after adjusting to make sure they are over-collateralised. It is calculated as the market value of a user's borrows divided by the relevant collateral factors. 
 * Liquidationn event in which a user's collateral assets are exchanged for the assets they borrowed in order to bring them back to an over-collateralised state.     
 * Static interest rate: a type of model used on Compound and Aave in which the interest rate is constrained to be a function of the utilisation rate of a liquidity pool.
 * Reactive interest rate: a new type of interest rate model backed by control theory that allows interest rates to react freely to market conditions.  
 * Compound interest: the result of perpetually earning interest on interest already accrued.  
 * Euler XYZ: the initial developers of Euler Protocol.
 * Euler DAO: the decentralised autonomous organisation that will manage Euler Protocol and the Euler Treasury.
 * Euler Protocol: the collection of smart contracts comprising the protocol.
 * Euler Governance Token (EUL)] EUL tokens represent voting shares in Euler governance. A holder can vote on each proposal themselves or delegate their votes to a third party.
