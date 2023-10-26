---
description: Get answers to frequently asked questions about Euler.
---

# FAQ

### General

#### What is Euler?

Euler is a non-custodial protocol on Ethereum that allows users to lend and borrow almost any crypto asset. Learn more about how Euler works by reading the [white paper](../getting-started/white-paper.md) here.

#### Who developed Euler?

Euler was initially created by a team of developers at a company called Euler Labs (see website [here](http://euler.xyz)). Today it is progressively decentralising and receives contributions from the external developer community as well as ongoing contributions from Euler Labs.

#### What is EulerDAO?

EulerDAO is a decentralised autonomous organisation encapsulating all holders of a governance token called EUL. Holders of the token have voting powers to propose and make changes to the underlying code of the Euler Protocol.

#### What is the Euler Foundation?

Since DAOs not have a formal legal structure, the Euler Foundation was established as a non-profit Foundation Company designed to represent EulerDAO in the ‘real world’. The Euler Foundation has no shareholders and cannot pay out dividends to its members. Its purpose is to provide a vehicle by which EulerDAO can sign a contract or engage a company for a service that the DAO requires.

### Community Involvement

#### How can I get involved in EulerDAO?

Join the [Discord](https://discord.gg/CdG97VSYGk) and meet the community, make proposals and discussion on the [governance forum](https://forum.euler.finance/), or send a message if you have other ideas of contributing to the protocol.

#### Where is the developer documentation?

Please refer to the [Developers](../developers/getting-started/integration-guide.md) section and check out the [Euler SDK](https://blog.euler.finance/announcing-the-euler-sdk-976f6e34c73).

#### Where are your branding guidelines/materials?

The branding materials are located at the following link: [euler.finance/branding](https://www.euler.finance/branding/#branding). Copyright is owned by the Euler Foundation.

### Euler dApp

#### How do I deposit and borrow?

Check out the How To guides [here](ui/). Or just go to the [Euler app](https://app.euler.finance/), login via the Connect button on ETH mainnet. Click on the Quick Action button. You can deposit and borrow through the same named action buttons. Choose the asset and amounts, then approve of the transactions.

**How do I activate a market?**

Search for an asset in the search bar on the [Euler app](https://app.euler.finance/). Unlisted assets can be activated by the Activate button, which will ask you to initiate the transaction. Once complete, the asset will be listed and activated.

#### How do I get testnet tokens?

The Goerli testnet has a test ER20 token faucet smart contract deployed a [0x1215396CB53774dCE60978d7237F32042cF3a1db](https://goerli.etherscan.io/address/0x1215396CB53774dCE60978d7237F32042cF3a1db).

To get testnet tokens for Goerli, connect open the smart contract on Etherscan by clicking the link above. Click on the tab with the green tick, then click on `Write Contract` and connect your wallet. Once connected, expand the withdraw feature and paste the underlying ERC20 token smart contract address and click on the `Write` button. This will require you to confirm the transaction in your wallet which costs gas.

Once confirmed, the token faucet smart contract will an amount of the specified testnet ERC20 token (up to a pre-defined threshold) to your connected wallet address.

The Goerli testnet token faucet supports the following ERC20 tokens: [WETH](https://goerli.etherscan.io/address/0xa3401DFdBd584E918f59fD1C3a558467E373DacC), [UNI](https://goerli.etherscan.io/address/0x2980D241BEA2A49d3333AA931884d68C704E7Db7), [USDC](https://goerli.etherscan.io/address/0x693FaeC006aeBCAE7849141a2ea60c6dd8097E25), [USDT](https://goerli.etherscan.io/address/0x7594a0368F18e666480Ad897612f28ad17435B4C), [DOGE](https://goerli.etherscan.io/address/0x67cF0FF98bE17bF02F7c6346028C9e8BB3c203B2), [WBTC](https://goerli.etherscan.io/address/0xc49BB678a4d822f7F141D5bb4585d44cCe51e25E), [COMP](https://goerli.etherscan.io/address/0x6520f3394a2000eA76e7cA96449B78BB0eD07561), [CRV](https://goerli.etherscan.io/address/0x9eA3D1d18A0e7Ec379C577f615220e6D715F3b29).

#### Why can't I find a specific token to activate?

Some tokens might not be on the token list or might not have a pool on Uniswap v3. Please [send a message](https://discord.gg/CdG97VSYGk) if you have trouble finding an unlisted asset.

#### What are asset tiers?

Euler uses risk-based [asset tiers](../getting-started/white-paper.md#asset-tiers) to protect the protocol and its users. Isolated and Cross assets cannot be used as collateral, but Cross assets can be borrowed alongside other assets, while Isolated assets cannot.

#### What are sub-accounts?

[Sub-accounts](https://docs.euler.finance/developers/getting-started/architecture#sub-accounts) enable users to isolate positions into different accounts.

#### What oracle does Euler use?

By default Euler uses Uniswap V3 Time Weighted Average Price (TWAP) as the pricing oracle. However, the oracle used can be changed in the governance process on one-to-one basis. Currently, Euler also supports Chainlink price feeds as a price source.

#### What is the oracle rating?

The [Oracle Rating system](../euler-protocol/getting-started/methodology/oracle-rating.md) attempts to rank Uniswap v3 price oracles for different markets high, medium, or low based on the ease with which they can be manipulated.

#### What are the reserves?

[Reserves](https://docs.euler.finance/developers/architecture#reserves-1) are protocol-owned liquidity deposited on Euler to provide a backstop against a 'run on the bank' scenario. Reserves build up over time as borrowers pay interest on their loans. The reserves are ultimately controlled by EulerDAO Governance.

#### How can an asset become collateral?

An asset must have substantial liquidity with wide distribution in its Uniswap V3 WETH paired pool. If the asset has a low-risk oracle, it is in a better position to be regarded as a safer asset to become collateral through a [governance proposal](https://forum.euler.finance/t/welcome-to-the-euler-governance-forum/7).

#### Is Euler on any other chains/L2s?

Euler is currently only on Ethereum Mainnet. Euler is open to and exploring other chains and layers, but nothing is currently imminent.

#### What is the difference between Sign Permit and Enable?

Enable is the standard approval transaction that allows Euler smart contracts access to that asset. You can edit the amount from unlimited in Metamask. Sign Permit is a gasless way of approving a contract to use your tokens as a one-time allowance ([EIP-2612](https://eips.ethereum.org/EIPS/eip-2612)).

### Features

#### What are Mint and Burn?

[Mint](ui/#mint) enables users to more efficiently create leveraged positions of borrowers and deposits. For example, a user can deposit $1,000 USDC, and mint $2,000 USDC. Then you will have $3,000 USDC deposits, and $2,000 USDC liabilities. Burn closes Mint positions.

#### What does the Transfer action do?

Users can [transfer](ui/#transfer-etokens) deposits (eTokens) and debt (dTokens) to other accounts. Always check the accounts involved in your operation will have sufficient collateral to support it.

#### Can I swap tokens?

Yes, the swap feature enables users to exchange one deposited asset for another using Uniswap and 1inch DEXs.

#### How can I short a token?

The [Short](ui/#short) action allows users to build a leveraged short position by borrowing and then immediately selling an asset on an external exchange, including 1inch and Uniswap.

#### Should I mine at 19x?

Euler does not give financial advice, but users should note that mining at 19x is highly risky and can lead to liquidation if the user’s collateral cannot cover the interest fees. Mining at 19x most often liquidates positions within the same day it is created.

#### What is Time To Liquidation (TTL)?

[TTL](https://www.euler.finance/blog/announcing-new-features-of-euler-dapp) allows users to see the amount of time they have until their position is liquidated based on the current interest rates and prices of those positions.

#### What is a soft liquidation?

Euler allows [liquidators](../getting-started/white-paper.md#soft-liquidations) to repay up to the amount needed to bring a violator back out of violation (plus an additional safety factor). Other protocols are fixed so that liquidators can pay off up to half a borrower's loan in one go, regardless of how underwater their position is.

### Gauges & EUL Distribution

#### How can I claim EUL tokens?

Users can go to the [Euler app](https://app.euler.finance/), click on the Claim button in the navbar and claim any available tokens of previous epochs in the Distribution window once EUL tokens are available to claim.

#### What utility does EUL have?

EUL’s main utility is as a [governance token](broken-reference/) for the Euler protocol. Users with EUL can have a say in the future decisions and direction, as well as the EUL distribution in the Euler gauges.

#### What is the distribution of EUL tokens for borrowers?

The distribution is decided by the amount of EUL tokens staked in the [gauges](https://app.euler.finance/gauges).

#### How are markets decided for each epoch?

Users can add or remove EUL distribution eligible markets simply by staking EUL tokens in their preferred gauges. See the link in the above question for the results of these votes. Please see [eIP 51](https://snapshot.org/#/eulerdao.eth/proposal/0x551f9e6f3fba50a0fc2c69e361f7a81979189aa7f0ed923a1873bd578896942b) for the latest iteration of EUL distribution.

In order to receive EUL emmission, assets (as per [eIP 24](https://snapshot.org/#/eulerdao.eth/proposal/0x7e65ffa930507d9116ebc83663000ade6ff93fc452f437a3e95d755ccc324f93)) need to have a Chainlink pirce feed as well as receive EUL votes in the gauge system.&#x20;

### EUL Token

#### Is there a token? How can I earn it?

The Euler token (EUL) is distributed to borrowers on select markets on the platform. Please see the [Gauges](https://docs.euler.finance/eul/gauges) section for more details.

#### What are the tokenomics?

Allocation, vesting and other information about the EUL token can be found in the About section under [EUL](https://docs.euler.finance/eul/about).

#### Is there a TGE/ICO/IDO?

There is no public sale.

#### Where can I trade EUL?

While EUL token has been released, Euler Labs does not give financial advice on trading the token.

#### How do I get an airdrop?

There is no airdrop. 1% of the supply was allocated to users who interacted with the dApp during [Epoch 0](https://docs.euler.finance/governance/distribution#epoch-0) as a one-off retroactive distribution.

#### Do testnet users receive rewards?

No, [testnet](https://goerli.euler.finance/) is to preview upcoming features and for users to learn about the protocol without any mainnet gas fees.

#### Someone messaged me promising free tokens/ICO/NFTs/etc, is it real?

No, that is fake. No one related to Euler will ever message anyone directly, nor offer free tokens or investments of any kind.

### Partnerships

#### Who can I contact about partnerships/integrations?

Feel free to reach out through Discord or other platforms in the Quick Links section. Also read the [integration guide](../developers/getting-started/integration-guide.md) for more details.

#### Can we list EUL on our exchange?

Euler cannot advise on exchange listings, nor pay for any listings.

#### Can we offer our token in your liquidity mining programme?

Euler will be adding this feature in the near future. Please get in touch if you’d like to integrate with the distribution mechanisms.

#### Can you market our company/token if we pay you or activate our token?

Sorry, Euler does not accept payments or donations of any kind to promote activated markets.

### Miscellaneous

#### How does the Euler dApp detect wallets associated with illicit activities?

In alignment with industry best-practices, Euler utilizes Chainalysis to identify and block wallets that are associated with certain illicit activities.

Chainalysis is a market leader in protecting against interactions with bad actors linked to sanctions, financial crime, child sexual abuse material, terrorist financing, scams, hacked or stolen funds, ransomware, and human trafficking.

It is Euler’s aim to prevent those engaged or associated with illegal activity from using the protocol. Euler is committed to responsible development, innovation, and financial inclusion.
