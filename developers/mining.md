# EUL Token Liquidity Mining

EUL tokens are issued to users of the protocol who borrow assets, according to a time-weighted record of how long they retain those debts. The goal of this is to increase borrowing utilisation of the pools, including for longer-tail assets. This should have the effect of increasing interest rates for depositors in the pool which allow passive investors such as yield aggregators to indirectly benefit from liquidity mining without having to participate themselves.

Not all assets are eligible for mining rewards, however. A user could activate a custom market of which they control the entire underlying supply, and easily capture all the rewards for that market. Instead, only a subset of markets will receive rewards. This subset is determined by a staking system where participants allocate EUL tokens to the markets they would like to earn rewards on. Each epoch (approximately 2 weeks), the top `N` markets will be selected to earn rewards during the following epoch. The proportion of the total rewards issued for each markets is based on the square root of the number of tokens staked on that market. Both the total EUL distributed and the `N` parameter that controls the number of tokens are controlled by Euler governance.

## EulDistributor

This contract implements a merkle drop. Governance will seed it with an amount of EUL tokens at least necessary to cover the current cumulative distribution, although extra can be pre-committed if desired. It also supports distributing tokens other than EUL, so that token partners can leverage the distribution infrastructure if governance approves.

The current merkle root as well as the previous merkle root is kept in storage. They are typically (but not necessarily) updated once per epoch. Either root is eligible to claim rewards so as to prevent pending transactions from failing when the root is updated.

The leaves of the merkle tree are 72 bytes long, preventing interior nodes from being reinterpreted as leaves.

In its constructor, this contract approves its sister contract `EulStakes` access to its EUL tokens. This is necessary to implement "auto-staking", a feature which allows a user to claim EUL tokens and directly stake them on a market for voting purposes. This allows EOA wallets to do this operation in one transaction and save gas since it doesn't need to transit the user's wallet.

## EulStakes

This contract maintains the record of how much each user has staked on each market, for the purposes of voting. To save gas, the aggregate amount voted on each market is not available on-chain and must be reconstructed from the contract's logs.

Rather than implementing disjoint staking/unstaking functions, the interface is unified into a compound operation that accepts an array of `StakeOp` commands. Each command can either increase or decrease a user's stake on a market. After applying all the operations, the sum of all modifications is checked. If this amount is positive, that amount of EUL tokens must be transferred *in* to the contract. If negative, that amount is transferred *out* to the user's wallet. If zero, then no tokens are transferred. This allows EOAs to easily deposit/withdraw and rebalance stakes in a single operation.

In order to implement "auto-staking" described in previous section, `stakeGift` allows somebody to apply a single *deposit* operation on behalf of another "beneficiary" account.

There is also a `stakePermit` function that applies an EIP-2612 permit message to the EUL contract prior to applying the `StakeOp`s. This allows an EOA to approve the EulStakes contract and perform staking within a single transaction.
