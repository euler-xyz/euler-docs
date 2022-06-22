---
description: Learn more about the Euler Governance launch phases
---

# Euler DAO Launch Phases

EulerDAO will kick off in three phases for a guarded launch towards full decentralisation of the Euler protocol. Each phase is described below.

The EulerDAO uses the OpenZeppelin Governor smart contracts (version 4.6.0) for governance (as well as the EUL token contract). It is a governance protocol — similar to the one Compound uses — where delegates vote on active proposals to make changes to the EulerDAO and Euler protocol.

Euler uses the Tally governance dashboard application to manage the governance process. Through Tally, you can set up your wallet to become a delegate, create on-chain proposals, vote on active proposals, discover delegates in the community, and delegate your voting power to a community member.


## Phase 1 
The first phase of the launch will be such that actions to be performed directly on the Euler protocol smart contracts will be executed by the Euler team on behalf of the community. In this case, all on-chain governance proposals will point to or target a function in a stub smart contract (in place of the Euler protocol smart contracts).

Should the proposal become successful and executed, the target function will then be executed (via the TimelockController controller smart contract). It will emit the proposal description string and proposal transaction data, which will then be validated by the Euler team and executed against the Exec module via the Euler multisig.

Hence, the `governorOnly()` modifier in the Euler Governance module smart contract will be checking that the caller of its functions is the Euler mulisig and not the TimelockController smart contract.

To create the proposal transaction data, we have implemented a [tool](https://governance.euler.finance/) which will help the proposer to auto generate this depending on what actions should be executed. 

The proposer can select a token from the dropdown token list (this will auto populate the fields with the current configuration for the token/market on Euler), the proposer can then make modifications and generate the proposal transaction hex to be executed via the Euler Exec module (`batchDispatch()` function) and use this hex data as the input to the target function in the stub smart contract when creating a proposal on Tally.

Examples of the kinds of decisions token holders might vote on include proposals to modify:
* The tier of an asset
* Collateral and borrow factors
* Price oracle parameters
* Reactive interest rate model parameters
* Reserve factors


## Phase 2 
In the second phase, the governor admin for the Euler Governance module will switch from the Euler multisig to the TimelockController smart contract. Hence, the `governorOnly()` modifier in the Euler Governance module smart contract will be checking that the caller of its functions is the TimelockController smart contract.

In this case, proposals created via the Tally governance dashboard will need to target the Euler [Governance module](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Governance.sol) directly. Successful proposals which receive a higher number of votes in support will then be executed without the control of the Euler team. 

During execution, the TimelockController smart contract will call the target function in the Euler Governance module as specified within the on-chain proposal. Proposers will be able to add a batch of actions / functions to be executed within the Euler Governance module into a single on-chain proposal as well.

## Phase 3
In this phase, the Installer Admin will also be switched to the TimelockController smart contract.

Not only giving the community control over the Governance module for asset configuration modifications but also full control over the protocol including the installer module. This module is used to bootstrap install the rest of the modules, and can later on be used to upgrade modules to add new features and/or fix bugs.