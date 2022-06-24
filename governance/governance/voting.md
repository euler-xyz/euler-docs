---
description: Learn more about how to participate in Euler Governance
---

# On-Chain Governance & Voting

## Introduction

The [Euler protocol](https://www.euler.finance/) is governed and upgraded by EUL token-holders, using three distinct components; the EUL token, governance module, and timelock module. Together, these contracts allow the community to propose, vote, and implement changes. Proposals can modify system parameters, support new markets, or add entirely new functionality to the protocol. 

EUL is an ERC-20 token that allows token holders to delegate voting rights to any address, including their own address. Changes to the owner’s token balance automatically adjust the voting rights of the delegate. In order to enable these features, the Euler Token smart contract inherits the features from the openzeppelin [ERC20Votes](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/ERC20Votes.sol) abstract contract. 

On the other hand, Euler uses [OpenZeppelin Governance smart contracts](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/governance) for governance. It is a governance protocol allowing voters/delegates vote on active proposals to make changes to the Euler governance configurations (i.e., voting delay, voting duration and proposal threshold) and Euler protocol.

Euler will be managed by holders of a protocol native governance token called Euler Token (EUL). EUL tokens represent voting shares. A holder can vote on a governance proposal themselves or delegate their votes to a third party. Addresses that own or have been delegated at least 0.5% of the total EUL supply can create governance proposals.

Specifically, the smart contract functions capable of modifying the protocol and controlled via governance have been implemented in the Euler [Governance module](https://github.com/euler-xyz/euler-contracts/blob/457e5302fd506d5b578776e57188661e047fda81/contracts/modules/Governance.sol) of the protocol.

Examples of the kinds of decisions token holders might vote on include proposals to modify:
* The tier of an asset
* Collateral and borrow factors
* Price oracle parameters
* Reactive interest rate model parameters
* Reserve factors
* Governance configurations themselves, i.e., voting period, voting delay and proposal threshold via a newly released [GovernorSettings.sol base contract](https://github.com/OpenZeppelin/openzeppelin-contracts/pull/2904) in v4.6.0 of the OpenZeppelin Smart Contracts.

When a governance proposal is created, it enters a 2 day review period, after which voting weights are recorded and voting begins. Voting lasts for 3 days; once the voting period is over, if quorum was reached (enough voting power participated) and the majority voted in favour, the proposal is considered successful and can proceed to be executed 2 days (48 hours) later.

On-chain governance actions (proposal, voting, etc.) for the Euler protocol can be done via the [Tally](#tally) governance dashboard (described below). 

## Tally

Tally is a governance app in the form of a web-based platform focused on enabling on-chain governance for DeFi projects. The Tally governance web application [provides transparency around the governance of various DeFi protocols, e.g., Compound, Uniswap, etc.](https://docs.tally.xyz/) bringing all of the proposals and voting for these protocols under a shared user interface.

Tally empowers user owned governance through a voting dashboard, governance tooling, and real time research and analysis. Users can use the app to review data on governance systems, active and prior proposals, and individual delegates or token holders. The platform also enabled direct on-chain voting and vote delegation, helping users put their governance insights into action. Through integration with the Euler governance smart contract, Euler token holders can connect their wallets and create proposals, vote, delegate voting power to a community member, discover other delegates in the community, and more.

### Delegate

If you wish to have a say in governance, you need to delegate your vote to self or someone in the community. 

In summary, delegates are token holders that have completed a one-time setup process (executing the delegate function of the token to delegate another user or the token holder themselves to enable the governor contract to determine their voting power). Once you become a delegate, you can vote on active proposals, and create proposals if you have enough voting power. If you choose not to directly vote on proposals, you can pass your voting power on to a delegate as well.

The delegate sections below describe the delegation using the EUL token smart contract and via the Tally Governance Dashboard.

Delegate votes from the sender to a delegatee. Users can delegate to 1 address at a time, and the number of votes added to the delegatee’s vote count is equivalent to the balance of EUL in the user’s account. Votes are delegated from the current block and onward, until the sender delegates again, or transfers their EUL. Delegation can be carried out via the smart contract function described below or via the Tally user interface.

#### Tally Governance Dashboard

The first step in the delegation process via the Tally governance application is to visit the EulerDAO page on the Tally governance application and connect your wallet. 

![](<../../.gitbook/governance/connect_wallet.png>)

The second step is to click on "Delegate vote" at the top right corner of the screen. 

Users can then choose to either delegate to themselves or to another wallet, delegate or community member. By delegating to self, you retain your voting power. Next time there is an active proposal, you can choose to vote in any way you choose.

![](<../../.gitbook/governance/delegate_to_self.png>)

If you choose to delegate to an address or delegate, the following screen will be shown instead where you can enter the address you wish to delegate your voting power to. 

![](<../../.gitbook/governance/delegate_to_other_address.png>)

This will not transfer any of your tokens to the delegate, you will only be delegating your voting power, i.e., voting via proxy who will be voting on your behalf or representing you at the polls! You can always change the delegate later on or delegate to yourself again. This helps to ensure that there is a good degree of participation from the community on on-chain governance proposals voting.

Finally, regardless of whether you are delegating to yourself or delegating to a delegate, you will be required to confirm the transaction in your wallet and this transaction will cost gas.


![](<../../.gitbook/governance/delegate_to_self_metamask.png>)

To recap, delegates are token holders that have completed a one-time setup process. Once you become a delegate, you can then vote on active proposals, and create proposals if you have enough voting power. If you choose not to directly vote on proposals, you can pass your voting power on to a delegate as we have seen.


#### EUL

For developers who wish to interact with the EUL token contract directly, the EUL contract has a delegate function defined below with examples on how to interact with it.

    function delegate(address delegatee)
* ```delegatee```: The address the sender wishes to delegate their votes to.
* ```msg.sender```: The address of the EUL token holder that is attempting to delegate their votes.
* ```RETURN```: No return.

#### Solidity
    EUL eul = EUL(0x123...); // contract address
    eul.delegate(delegateeAddress);

#### Web3
    const tx = await eul.methods.delegate(delegateeAddress).send({ from: sender });




### Proposal Creation and Voting

The images below depict the use of the Tally governance dashboard for governance proposal creation and voting.

The governance home page on Tally shows a list of active and succeeded proposals:

![](<../../.gitbook/governance/recent_proposals.png>)

On Tally, users can also see the top voters on proposals created for the Euler test DAO as shown below:

![](<../../.gitbook/governance/top_voters.png>)

Users can also view the total percentage of votes in support or against a specific proposal. In the image below, the test proposal succeeded with all votes in support:

![](<../../.gitbook/governance/succeeded_proposal.png>)


#### Proposal Creation

To create a new proposal, users will need to click on `Create New Proposal` from the DAO home page on Tally as shown in the top right corner in the image below:

![](<../../.gitbook/governance/dao_1_tally_2.png>)

This will then open up the proposal creation dialog taking users through the required steps to create an on-chain proposal. In the initial step / screen, it will check that the user has enough voting power to meet the proposal threshold specified within the governance smart: 

![](<../../.gitbook/governance/new_proposal_1.png>)

The next step will require users to name the proposal and add a short description as shown below:

![](<../../.gitbook/governance/new_proposal_2.png>)

In the next step, users will need to add the actions to be executed should the proposal become successful or receive majority of vote in support. In this step, users can specify the target smart contract and required function parameters:

![](<../../.gitbook/governance/new_proposal_3.png>)

The following page will then be the review page allowing the user to review and confirm that the specified actions are correct: 

![](<../../.gitbook/governance/new_proposal_review.png>)


Once confirmed, the proposal will then be created on-chain and if successful, Tally will display the proposal page with the description and status (e.g., pending, active, succeeded, queued, executed). 
![](<../../.gitbook/governance/new_proposal_submitted.png>)


#### Voting

When voting, users have the option to vote for or against a proposal or an abstain vote as shown in the images below:

Firstly users will need to connect their wallet to cast a vote
![](<../../.gitbook/governance/connect_to_vote.png>)

Followed by casting a vote with or without a comment for the community
![](<../../.gitbook/governance/vote_for.png>)

Full Tally documentation can be accessed online at: [Tally](https://docs.withtally.com). The documentation describes how to navigate the web app, voting and delegation and creating a Tally account.