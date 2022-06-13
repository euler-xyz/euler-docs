---
description: Learn more about how to participate in Euler Governance
---

# Voting & Governance

On-chain governance, allows unique features such as delegated voting and proposition powers, rapid protocol (and governance configuration) upgrades via a time lock executor. 
This ensures the protocol can quickly adapt to evolving market conditions, as well as upgrade core parts of the protocol over time.

## Euler DAO Launch Phases

The Euler DAO will be launched in three phases for a guarded launch towards full decentralisation of the Euler protocol. Each phase is described below.
The Euler DAO uses the OpenZeppelin Governor smart contracts (version 4.6.0) for governance (as well as the EUL token contract). It is a governance protocol — similar to the one Compound uses — where delegates vote on active proposals to make changes to the Euler DAO and Euler protocol.

Euler uses the Tally governance dashboard application to manage the governance process. Through Tally, you can set up your wallet to become a delegate, create on-chain proposals, vote on active proposals, discover delegates in the community, and delegate your voting power to a community member.


### Phase 1 
The first phase of the launch will be semi-decentralised wherein actions to be performed directly on the Euler protocol smart contracts will be performed or executed by the Euler team on behalf of the community. In this case, all on-chain governance proposals will point to or target a function in a stub smart contract (in place of the Euler protocol smart contracts). Should the proposal become successful and executed, the target function will then be executed (via the TimelockController controller smart contract) and it will emit the proposal description string and proposal transaction data which will then be validated by the Euler team and executed against the Exec module via the Euler multisig.

Hence, the `governorOnly()` modifier in the Euler Governance module smart contract will be checking that the caller of its functions is the Euler mulisig and not the TimelockController smart contract.

To create the proposal transaction data, we have implemented a [tool](https://governance.euler.finance/) which will help the proposer to auto generate this depending on what actions should be executed. The proposer can select a token from the dropdown token list (this will auto populate the fields with the current configuration for the token/market on Euler), the proposer can then make modifications and generate the proposal transaction hex to be executed via the Euler Exec module (`batchDispatch()` function) and use this hex data as the input to the target function in the stub smart contract when creating a propsal on Tally.

Examples of the kinds of decisions token holders might vote on include proposals to modify:
* The tier of an asset
* Collateral and borrow factors
* Price oracle parameters
* Reactive interest rate model parameters
* Reserve factors


### Phase 2 
In the second phase, we will switch the governor admin for the Euler Governance module from the Euler multisig to the TimelockController smart contract. Hence, the `governorOnly()` modifier in the Euler Governance module smart contract will be checking that the caller of its functions is the TimelockController smart contract. In this case, proposals created via the Tally governance dashboard will need to target the Euler [Governance module](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Governance.sol) directly. Successful proposals which receive a higher number of votes in support will then be executed without the control of the Euler team. 

During execution, the TimelockController smart contract will call the target function in the Euler Governance module as specified within the on-chain proposal. Proposers will be able to add a batch of actions / functions to be executed within the Euler Governance module into a single on-chain proposal as well. 

### Phase 3
In the final phase of the DAO launch, we will be moving towards full decentralisation. In this phase, the Installer Admin will also be switched to the TimelockController smart contract. Not only giving the community control over the Governance module for asset configuration modifications but also full control over the protocol including the installer module. This module is used to bootstrap install the rest of the modules, and can later on be used to upgrade modules to add new features and/or fix bugs.


## Introducing Euler's Governance Proposal Creation Tool (for Euler DAO Phase 1)

### Introduction

The first phase of Euler’s DAO / Governance launch will be semi-decentralised wherein actions to be performed directly on the Euler protocol smart contracts will be performed or executed by the Euler team on behalf of the community. In this case, all on-chain governance proposals will point to or target a function in a stub smart contract (in place of the Euler protocol smart contracts). 

Should the proposal become successful and executed, the target function will then be executed (via the TimelockController controller smart contract. It will emit the proposal description string and proposal transaction hex data, which will then be validated by the Euler team and executed against the `Exec` module via the Euler multisig (on OpenZeppelin Defender).

Hence, the `governorOnly()` modifier in the [Euler Governance module](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Governance.sol) will be checking that the caller of its functions is the Euler mulisig and not the TimelockController smart contract of the DAO.

To create the proposal transaction data, we have implemented a [tool](https://governance.euler.finance/) which will help the proposal creator to auto-generate it depending on what actions should be executed. The proposal transaction data is simply an encoded version of the on-chain transaction to the Exec module’s batchDispatch function.

The rest of the article will describe the process of creating the proposal transaction data on Euler’s governance proposal creation tool and using the generated proposal transaction data to create an on-chain proposal on the [Tally](https://www.tally.xyz/) governance dashboard.

### Section 1. Creating the proposal transaction data for Euler’s Exec Module

#### Step 1

Navigate to the [proposal transaction data creation tool](https://governance.euler.finance/).

The web application should look like the following image:

![](<../.gitbook/governance/gov_tool_1.png>)


#### Step 2 


The tool requires MetaMask to be installed in your browser. 
Switch your MetaMask wallet to mainnet. 

The tool currently supports the Ethereum Mainnet and our Ropsten testnet Exec modules. It will create the appropriate transaction data to be executed depending on the selected network.


#### Step 3

At the top left of the window, we have a text field for proposal description and below that we have a dropdown menu representing a list of tokens, e.g., USDC, DAI, etc.

At the left of the window, under the token list, we have a set of dropdown menus and text fields which will be autopopulated with the current token configurations (if the token has an activated market on Euler).

To create the proposal transaction data, the proposer needs to enter a proposal description and then select a token from the token list. Once selected, the rest of the fields will be automatically populated with the current configuration of the token or market on Euler if it has an activated market.

The image below shows the proposal description and the fields on the left populated with the current market configuration for USDC on Euler:

![](<../.gitbook/governance/gov_tool_3.png>)


#### Step 4

The proposer can then make modifications and generate the proposal transaction hex data to be executed via the Euler Exec module (`batchDispatch()` function) and use this hex data as the input to the target function in the stub smart contract when creating a proposal on Tally (this is described in Section 2 below).

For example purposes, let’s change the borrow factor of USDC to 0.6. To do this, we simply change the collateral factor from 0.9 to 0.6 in the text field for collateral factor and click on `CREATE PROPOSAL DATA`. Once we do this, we should see the markdown table showing the changes we want to make to the asset. We will also see the batch items Hex transaction data which we need for our on-chain governance proposal stub smart contract on Tally. 

![](<../.gitbook/governance/gov_tool_4_i.png>)

Note: This process can be repeated for multiple tokens and configurations (or multiple configurations of the same token). They will be added in a batch and encoded to form the transaction data for the batchDispatch functionality in the Euler Exec module.

For example, let us select DAI from the token list and change the borrow factor of DAI to 0.3. Again, the fields are automatically populated when we select DAI and when we change the borrow factor to 0.3 and click on `CREATE PROPOSAL DATA`. The list of configuration updates is updated to reflect the change we are making to DAI, while the USDC update information still remains. The transaction hex is also updated.

![](<../.gitbook/governance/gov_tool_4_ii.png>)


#### Step 5

To validate the updates we have selected, we can copy the auto-generated hex under batch items hex TX data (under batch items, which is under proposal description) and click on `DEBUG TX HEX DATA` and paste the copied hex into the text field. 

The tool should also decode the hex and show us a markdown with the updates the Euler team will be applying to the selected tokens once the proposal gets executed. The Euler team will also follow this process to make sure that the proposal description reflects the updates to be made before executing the transaction in the Exec module on behalf of the community. 

![](<../.gitbook/governance/gov_tool_5.png>)

As shown in the image above, the hex data is decoded to show the updates we selected to be applied to DAI and USDC. There is a close button at the bottom right of the window to close the debug modal and return to the main page. 

Once you get to this point, you now have your proposal transaction data which you can use to create your on-chain proposal on Tally. After the voting period, if successfully executed, the decoded hex data will be submitted to OpenZeppelin Defender for the Euler team to execute on behalf of the community.

Please let us know if you have any questions or feedback while using the tool in our Discord Governance channel.



### Section 2.Using the Auto-Generated transaction data for Euler’s Exec Module to Create an on-chain proposal for the DAO on Tally

At this point, we assume you now have the proposal transaction hex data needed for the Euler Exec module’s batchDispatch function. And you want to create the on-chain proposal for members of the community (and delegates) to vote on. If so, please read on! 

Below, we will describe the steps required to accomplish this goal.


#### Step 1

Head over to the EulerDAO dashboard on Tally and connect your MetaMask wallet.



#### Step 2

Click on `Create new proposal` at the right corner of the window. 

![](<../.gitbook/governance/dao_1_tally_2.png>)

It should then take you to the proposal creation window below.

![](<../.gitbook/governance/dao_1_tally_2i.png>)

Click on `Continue` to move onto the next step (`Name your proposal`). 


#### Step 3

Enter a proposal title and description and click `Continue`.

![](<../.gitbook/governance/dao_1_tally_3.png>)


#### Step 4

In the next section, you will be required to specify the governance proposal actions, i.e., target smart contract, target function and parameters. The Tally dashboard allows you to specify multiple actions in a single proposal which will be called/executed if the proposal is successful and executed.

![](<../.gitbook/governance/dao_1_tally_4_i.png>)

To add the proposal transaction hex from Section 1 and set the governance stub contract as the target smart contract, we will click on `Add custom action` => enter the stub smart contract address as the target smart contract. Then select the `executeProposal` function from the dropdown menu under `contract method` as the target function in the target smart contract. Here is the interesting part: enter the required parameters, i.e., proposal description string and the proposalData which is your proposal transaction hex data from Section 1.

![](<../.gitbook/governance/dao_1_tally_4_ii.png>)



#### Step 5

Once done, click continue and review the proposal. Once you are happy, you can click `Submit on-chain` which will open a MetaMask pop-up window for you to sign the transaction to create the proposal on-chain, via the Governance smart contract.

![](<../.gitbook/governance/dao_1_tally_5.png>)


## General Governance Process

The [General Governance Process](https://forum.euler.finance/t/welcome-to-the-euler-governance-forum/7) is documented on the Governance Forum.

The general flow for the governance process is proposed as follows:
Governance forum Idea/Proposal Discussion → eIP (Euler Improvement Proposal) creation on Governance forum by forum moderator → eIP created on Tally → On-chain Voting (and Execution if successful)

The image below depicts the on-chain governance phases and durations for each phase:

![](<../.gitbook/governance/governance_process.png>)



### Idea
A great place to start a discussion on a potential governance proposal is the idea section. If you feel confident that your idea is relevant to the community and is well-formulated, head over the to Governance Forum to begin a discussion with the community around your idea (following the process described on the forum). 

Once a discussion / commenting begins around your idea, be proactive with the community and be open to suggestions. It typically takes a week for the request for comments to mature before it becomes an eIP.

### Governance Proposal
If the discussion is well-formulated and the community has a clear understanding of the proposal and supports your idea, it will be moved by a moderator to the governance category as an eIP: Euler Improvement Proposal. Once the proposal has an eIP, an on-chain proposal can be created on the Tally governance dashboard under the Euler DAO.

A Tally proposal vote does not always need to be posted by the original eIP author, it can be posted by someone else or by the core team in case the minimum threshold of EUL is not being met.

A good governance proposal example can be found here: [eIP: Promote WBTC to collateral tier 3](https://forum.euler.finance/t/eip-1-promote-wbtc-to-collateral-tier/27).

Stay updated by subscribing to the [community newsletter](https://newsletter.euler.finance/) and follow the [Twitter Page](https://twitter.com/eulerfinance)!


## Governance Overview and Smart Contracts

The [Euler protocol](https://www.euler.finance/) is governed and upgraded by EUL token-holders, using three distinct components; the EUL token, governance module, and Timelock. Together, these contracts allow the community to propose, vote, and implement changes. Proposals can modify system parameters, support new markets, or add entirely new functionality to the protocol. Euler uses OpenZeppelin Governor for governance. It is a governance protocol — similar to the one Compound uses — where voters/delegates vote on active proposals to make changes to the Euler governance configurations and Euler protocol.

Euler will be managed by holders of a protocol native governance token called Euler Token (EUL). EUL tokens represent voting shares. A holder can vote on a governance proposal themselves or delegate their votes to a third party. Addresses that own or have been delegated at least 0.5% of the total EUL supply can create governance proposals.

Specifically, the smart contract functions capable of modifying the protocol and controlled via governance have been implemented in the [governance module](https://github.com/euler-xyz/euler-contracts/blob/457e5302fd506d5b578776e57188661e047fda81/contracts/modules/Governance.sol) of the protocol.

Examples of the kinds of decisions token holders might vote on include proposals to modify:
* The tier of an asset
* Collateral and borrow factors
* Price oracle parameters
* Reactive interest rate model parameters
* Reserve factors
* Governance configurations themselves, i.e., voting period, voting delay and proposal threshold via a newly released [GovernorSettings.sol base contract](https://github.com/OpenZeppelin/openzeppelin-contracts/pull/2904) in v4.6.0 of the OpenZeppelin Smart Contracts.

When a governance proposal is created, it enters a 2 day review period, after which voting weights are recorded and voting begins. Voting lasts for 7 days; once the voting period is over, if quorum was reached (enough voting power participated) and the majority voted in favour, the proposal is considered successful and can proceed to be executed 2 days (48 hours) later.

On-chain governance actions (proposal, voting, etc.) for the Euler protocol can be done via the [Tally](#tally) governance dashboard (described below) while off-chain governance actions can be carried out via [Snapshot](#snapshot). More information on on-chain and off-chain governance (i.e., proposals and voting) is described under the [Propose](#propose) section while both platforms are described as follows:

### Tally

Tally is a governance app in the form of a web-based platform focused on enabling on-chain governance for DeFi projects. The Tally governance web application [provides transparency around the governance of various DeFi protocols, e.g., Compound, Uniswap, etc.](https://www.coindesk.com/tally-defi-governance-funding-round) bringing all of the proposals and voting for these protocols under a shared user interface.

Tally empowers user owned governance through a voting dashboard, governance tooling, and real time research and analysis. Users can use the app to review data on governance systems, active and prior proposals, and individual delegates or token holders. The platform also enabled direct on-chain voting and vote delegation, helping users put their governance insights into action. Through integration with the Euler governance smart contract, Euler token holders can connect their wallets and create proposals, vote, delegate voting power to a community member, discover other delegates in the community, and more.

For example, the image below shows a list of active and succeeded proposals:

![](<../.gitbook/governance/recent_proposals.png>)

The image below shows the top voters on proposals created for the Euler test DAO:

![](<../.gitbook/governance/top_voters.png>)

Users can also view the total percentage of votes in support or against a specific proposal. In the image below, the test proposal succeeded with all votes in support:

![](<../.gitbook/governance/succeeded_proposal.png>)

And when voting, users have the option to vote for or against a proposal or an abstain vote as shown in the images below:

Firstly users will need to connect their wallet to cast a vote
![](<../.gitbook/governance/connect_to_vote.png>)

Followed by casting a vote with or without a comment for the community
![](<../.gitbook/governance/vote_for.png>)

Full Tally documentation can be accessed online at: [Tally](https://docs.withtally.com). The documentation describes how to navigate the web app, voting and delegation and creating a Tally account.


### Snapshot
Snapshot is an off-chain, gasless, multi-governance community polling dashboard. It allows soft voting (e.g. gauging how the community feels about a certain topic) and does not implement changes to the DAO or the protocol.

It is described by Cointelegraph as a [“governance-as-a-service” provider for a number of decentralized finance projects, including Yearn.finance, SushiSwap, Balancer, Aave, Cream and others](https://cointelegraph.com/news/gnosis-and-snapshot-create-tool-to-bind-defi-governance-votes-on-chain). It provides a simple interface to create governance proposals and lets users vote on them by connecting their wallets and the governance tokens contained within. However, the actual voting process is conducted off-chain to save on gas costs and complexity.

The image below shows the Snapshot user interface:

![](<../.gitbook/assets/snapshot_ui.png>)

Snapshot proposals are not binding. Team members and multisignature key holders for the projects are expected to execute the proposals, but the process relies entirely on their goodwill. Full Snapshot documentation can be accessed online at: [Snapshot](https://docs.snapshot.org).



## EUL

EUL is an ERC-20 token that allows token holders to delegate voting rights to any address, including their own address. Changes to the owner’s token balance automatically adjust the voting rights of the delegate. In order to enable these features, the Euler Token smart contract inherits the features from the openzeppelin [ERC20Votes](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/ERC20Votes.sol) abstract contract. 

If you wish to have a say in governance, you need to delegate your vote to self or someone in the community. 

In summary, delegates are token holders that have completed a one-time setup process (executing the delegate function of the token to delegate another user or the token holder themselves to enable the governor contract determine their voting power). Once you become a delegate, you can vote on active proposals, and create proposals if you have enough voting power. If you choose not to directly vote on proposals, you can pass your voting power on to a delegate as well.


The delegate sections below describe the delegation using the ERC20Votes (EUL token) smart contract and via the Tally Governance Dashboard.

### Delegate

Delegate votes from the sender to a delegatee. Users can delegate to 1 address at a time, and the number of votes added to the delegatee’s vote count is equivalent to the balance of EUL in the user’s account. Votes are delegated from the current block and onward, until the sender delegates again, or transfers their EUL. Delegation can be done via the smart contract function described below or via the Tally user interface.

#### Tally Governance Dashboard

The first step in the delegation process via the Tally governance application is to visit the Euler DAO page on the Tally governance application and connect your wallet. 

![](<../.gitbook/governance/connect_wallet.png>)

The second step is to click on "Delegate vote" at the top right corner of the screen. 

Users can then choose to either delegate to themselves or to another wallet, delegate or community member. By delegating to self, you retain your voting power. Next time there is an active proposal, you can choose to vote in any way you choose.

![](<../.gitbook/governance/delegate_to_self.png>)

If you choose to delegate to an address or delegate, the following screen will be shown instead where you can enter the address you wish to delegate your voting power to. 

![](<../.gitbook/governance/delegate_to_other_address.png>)

This will not transfer any of your tokens to the delegate, you will only be delegating your voting power, i.e., voting via proxy who will be voting on your behalf or repsenting you at the polls! You can always change the delegate later on or delegate to yourself again. This helps to ensure that there is a good degree of participation from the community on on-chain governance proposals voting.

Finally, regardless of whether you are delegating to yourself or delegating to a delegate, you will be required to confirm the transaction in your wallet and this transaction will cost gas.
![](<../.gitbook/governance/delegate_to_self_metamask.png>)


To recap, delegates are token holders that have completed a one-time setup process. Once you become a delegate, you can then vote on active proposals, and create proposals if you have enough voting power. If you choose not to directly vote on proposals, you can pass your voting power on to a delegate as we have seen.


#### EUL
    function delegate(address delegatee)
* ```delegatee```: The address in which the sender wishes to delegate their votes to.
* ```msg.sender```: The address of the COMP token holder that is attempting to delegate their votes.
* ```RETURN```: No return, reverts on error.

#### Solidity
    EUL eul = EUL(0x123...); // contract address
    eul.delegate(delegateeAddress);

#### Web3 1.2.6
    const tx = await eul.methods.delegate(delegateeAddress).send({ from: sender });


### Delegate By Signature

Delegate votes from the signatory to the delegatee. This method has the same purpose as Delegate but it instead enables offline signatures to participate in Euler governance vote delegation. For more details on how to create an offline signature, review [EIP-712](https://eips.ethereum.org/EIPS/eip-712).

#### EUL
    function delegateBySig(address delegatee, uint nonce, uint expiry, uint8 v, bytes32 r, bytes32 s)
* ```delegatee```: The address in which the sender wishes to delegate their votes to.
* ```nonce```: The contract state required to match the signature. This can be retrieved from the contract’s public nonces mapping.
* ```expiry```: The time at which to expire the signature. A block timestamp as seconds since the unix epoch (uint).
* ```v```: The recovery byte of the signature.
* ```r```: Half of the ECDSA signature pair.
* ```s```: Half of the ECDSA signature pair.
* ```RETURN```: No return, reverts on error.

#### Solidity
    EUL eul = EUL(0x123...); // contract address
    eul.delegateBySig(delegateeAddress, nonce, expiry, v, r, s);

#### Web3 1.2.6
    const tx = await eul.methods.delegateBySig(delegateeAddress, nonce, expiry, v, r, s).send({});


### Get Current Votes 
Gets the balance of votes for an account as of the current block.

#### EUL
    function getVotes(address account) returns (uint96)
* ```account```: Address of the account in which to retrieve the number of votes.
* ```RETURN```: The number of votes (integer).

#### Solidity
    EUL eul = EUL(0x123...); // contract address
    uint votes = eul.getVotes(0xabc...);

#### Web3 1.2.6
    const account = '0x123...'; // contract address
    const votes = await eul.methods.getVotes(account).call();


### Get Past Votes
Gets the prior number of votes for an account at a specific block number. The block number passed must be a finalized block or the function will revert.

#### EUL
    function getPastVotes(address account, uint blockNumber) returns (uint96)
* ```account```: Address of the account in which to retrieve the prior number of votes.
* ```blockNumber```: The block number at which to retrieve the prior number of votes.
* ```RETURN```: The number of prior votes.

#### Solidity
    EUL eul = EUL(0x123...); // contract address
    uint pastVotes = eul.getPastVotes(account, blockNumber);

#### Web3 1.2.6
const pastVotes = await eul.methods.getPastVotes(account, blockNumber).call();


### Key Events

| Event                                                                                                                                                                    | Description                                                            |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| DelegateChanged(address indexed delegator, address indexed fromDelegate, address indexed toDelegate)                                                                     | An event thats emitted when an account changes its delegate            |  
| DelegateVotesChanged(address indexed delegate, uint previousBalance, uint newBalance)                                                                                    | An event thats emitted when a delegate account's vote balance changes.  |
| ProposalCreated(uint id, address proposer, address[] targets, uint[] values, string[] signatures, bytes[] calldatas, uint startBlock, uint endBlock, string description) | An event emitted when a new proposal is created.                       |  
| VoteCast(address voter, uint proposalId, bool support, uint votes)                                                                                                       | An event emitted when a vote has been cast on a proposal.              |   
| ProposalCanceled(uint id)                                                                                                                                                | An event emitted when a proposal has been canceled.                    | 
| ProposalQueued(uint id, uint eta)                                                                                                                                        | An event emitted when a proposal has been queued in the Timelock.      |  
| ProposalExecuted(uint id)                                                                                                                                                | An event emitted when a proposal has been executed in the Timelock.    |   |



## Governor

Governor is the governance module of the protocol; it allows addresses with more than 0.5% of the EUL (Euler token) total supply to propose changes to the protocol. Addresses that held voting weight, at the start of the proposal, invoked through the ```getPastVotes``` function, can submit their votes during a 7 day voting period. If a majority, and at least 3% votes are cast for the proposal, it is queued in the Timelock, and can be implemented after 2 days.

### Name

Name of the governor instance (used in building the ERC712 domain separator).

#### Governance
    function name() returns (string)
* ```RETURN```: Name of the governor instance (used in building the ERC712 domain separator).

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint name = gov.name();

#### Web3 1.2.6
    const name = await gov.methods.name().call();


### Version
Version of the governor instance (used in building the ERC712 domain separator). Default: "1".

#### Governance
    function version() returns (string)
* ```RETURN```:  Version of the governor instance (used in building the ERC712 domain separator). Default: "1".

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint version = gov.version();

#### Web3 1.2.6
    const version = await gov.methods.version().call();


### Counting Mode 

A description of the possible `support` values for {castVote} and the way these votes are counted, meant to be consumed by UIs to show correct vote options and interpret the results. The string is a URL-encoded sequence of key-value pairs that each describe one aspect, for example `support=bravo&quorum=for,abstain`.

There are 2 standard keys: `support` and `quorum`.
* - `support=bravo` refers to the vote options 0 = For, 1 = Against, 2 = Abstain, as in `GovernorBravo`.
* - `quorum=bravo` means that only For votes are counted towards quorum.
* - `quorum=for,abstain` means that both For and Abstain votes are counted towards quorum.

NOTE: The string can be decoded by the standard [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) JavaScript class.

#### Governance
    function COUNTING_MODE() returns (string)
* ```RETURN```:  

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint counting_mode = gov.COUNTING_MODE();

#### Web3 1.2.6
    const counting_mode = await gov.methods.COUNTING_MODE().call();


### Quorum Votes

The required minimum number of votes required for a proposal to succeed.
Note: The `blockNumber` parameter corresponds to the snaphot used for counting vote. This allows to scale the quroum depending on values such as the totalSupply of a token at this block (see the openzeppelin [ERC20Votes](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/ERC20Votes.sol) abstract contract).

#### Governance
    function quorum(uint blockNumber) public pure returns (uint)
* ```blockNumber```: The block number at which to retrieve the quorum.
* ```RETURN```: The minimum number of votes required for a proposal to succeed.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint quorum = gov.quorumVotes(blockNumber);

#### Web3 1.2.6
    const quorum = await gov.methods.quorumVotes(blockNumber).call();


### Timelock
Public accessor to check the address of the timelock.

#### Governance
    function timelock() returns (address)
* ```RETURN```: The address of the timelock contract used by the Governance contract for proposal queueing and execution.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint timelock = gov.timelock();

#### Web3 1.2.6
    const timelock = await gov.methods.timelock().call();


### Proposal ETA
Public accessor to check the eta of a queued proposal.

#### Governance
    function proposalEta(uint proposalId) returns (address)
* ```RETURN```: The eta of a queued proposal.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint proposalEta = gov.proposalEta();

#### Web3 1.2.6
    const proposalEta = await gov.methods.proposalEta(proposalIds).call();


### Proposal Threshold

The minimum number of votes required for an account to create a proposal. This can be changed through governance.

#### Governance
    function proposalThreshold() returns (uint)
* ```RETURN```: The minimum number of votes required for an account to create a proposal.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint threshold = gov.proposalThreshold();

#### Web3 1.2.6
    const threshold = await gov.methods.proposalThreshold().call();


### Proposal Snapshot 

The block number used to retrieve user's votes and quorum.

#### Governance
    function proposalSnapshot(uint proposalId) returns (uint)
* ```proposalId```: The proposal ID
* ```RETURN```: Block number.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint snapshot = gov.proposalSnapshot(proposalId);

#### Web3 1.2.6
    const snapshot = await gov.methods.proposalSnapshot(proposalId).call();


### Proposal Deadline 

The timestamp at which votes close.

#### Governance
    function proposalDeadline(uint proposalId) returns (uint)
* ```proposalId```: The proposal ID
* ```RETURN```: Timestamp at which votes close.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint deadline = gov.proposalDeadline(proposalId);

#### Web3 1.2.6
    const deadline = await gov.methods.proposalDeadline(proposalId).call();


### Voting Delay

The number of Ethereum blocks to wait before voting on a proposal may begin. This value is added to the current block number when a proposal is created. This can be changed through governance.

#### Governance
    function votingDelay() returns (uint)
* ```RETURN```: Number of blocks to wait before voting on a proposal may begin.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint votingDelay = gov.votingDelay();

#### Web3 1.2.6
    const votingDelay = await gov.methods.votingDelay().call();


### Voting Period

The duration of voting on a proposal, in Ethereum blocks. This can be changed through governance.

#### Governance
    function votingPeriod() returns (uint)
* ```RETURN```: The duration of voting on a proposal, in Ethereum blocks.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint votingPeriod = gov.votingPeriod();

#### Web3 1.2.6
    const votingPeriod = await gov.methods.votingPeriod().call();




### Propose

The first step is to canvas support from the wider community for making an upgrade. This will usually involve submission of a description of the general idea to the Euler Forum, here. 

Once the idea has been debated and refined with input from others, it can be put forward for an off-chain vote via Snapshot, here. Off-chain voting is non-binding, but helps the community verify that there is real support for a proposal before it goes to the final stage.

The final stage of a proposal requires a governance action to be created and submitted as a formal on-chain proposal. An on-chain proposal requires a user to have 0.5% of the total EUL supply owned or delegated to them.
A governance action is a package of executable code that can be used to alter the state of the protocol in some way or transfer funds from the Euler Treasury. For example, it could be code that alters an interest rate parameter (see Euler Parameters), or promotes an asset from Isolation Tier to Collateral Tier (see Asset Tiers), or a much more involved proposal that adds an entirely new module to the Euler smart contracts (see Euler Smart Contracts).

Proposals will be voted on by delegated voters. If there is sufficient support before the voting period ends, the proposal shall be automatically enacted. Enacted proposals are queued and executed in the Timelock contract.

The sender must hold more EUL than the current proposal threshold (```proposalThreshold()```) as of the immediately previous block.

The proposer cannot create another proposal if they currently have a pending or active proposal. It is not possible to queue two identical actions in the same block (due to a restriction in the Timelock), therefore actions in a single proposal must be unique, and unique proposals that share an identical action must be queued in different blocks.

#### Governance

    function propose(address[] memory targets, uint[] memory values, bytes[] memory calldatas, string memory description) returns (uint)
* ```targets```: The ordered list of target addresses for calls to be made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```values```: The ordered list of values (i.e. msg.value) to be passed to the calls made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```calldatas```: The ordered list of data to be passed to each individual function call during proposal execution. This array must be the same length as all other array parameters in this function.
* ```description```: A human readable description of the proposal and the changes it will enact.
* ```RETURN```: The ID of the newly created proposal.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint proposalId = gov.propose(targets, values, calldatas, description);

#### Web3 1.2.6
    const tx = gov.methods.propose(targets, values, calldatas, description).send({ from: sender });


### Hash Proposal

Hashing function used to (re)build the proposal id from the proposal details.

    function hashProposal(
        address[] calldata targets,
        uint256[] calldata values,
        bytes[] calldata calldatas,
        bytes32 descriptionHash
    ) public pure virtual returns (uint)
* ```targets```: The ordered list of target addresses for calls to be made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```values```: The ordered list of values (i.e. msg.value) to be passed to the calls made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```calldatas```: The ordered list of data to be passed to each individual function call during proposal execution. This array must be the same length as all other array parameters in this function.
* ```descriptionHash```: A hash of the human readable description of the proposal and the changes it will enact.
* ```RETURN```: The ID of the proposal.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint proposalId = gov.hashProposal(targets, values, calldatas, description);

#### Web3 1.2.6
    const proposalId = gov.methods.hashProposal(targets, values, calldatas, descriptionHash).call();


### Queue

After a proposal has succeeded, it is moved into the Timelock waiting period using this function. The waiting period (e.g. 2 days) begins when this function is called.

The queue function can be called by any Ethereum address.

#### Governance
    function queue(address[] memory targets, uint[] memory values, bytes[] memory calldatas, string memory description) returns (uint)
* ```targets```: The ordered list of target addresses for calls to be made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```values```: The ordered list of values (i.e. msg.value) to be passed to the calls made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```calldatas```: The ordered list of data to be passed to each individual function call during proposal execution. This array must be the same length as all other array parameters in this function.
* ```descriptionHash```: A hash of the human readable description of the proposal and the changes it will enact.
* ```RETURN```: The ID of the newly created proposal.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    gov.queue(targets, values, calldatas, descriptionHash);

#### Web3 1.2.6
    const tx = await gov.methods.queue(targets, values, calldatas, descriptionHash).send({ from: sender });


### Execute

After the Timelock waiting period has elapsed, a proposal can be executed using this function, which applies the proposal changes to the target contracts. This will invoke each of the actions described in the proposal.

The execute function can be called by any Ethereum address.

Note: this function is payable, so the Timelock contract can invoke payable functions that were selected in the proposal.

#### Governance
    function execute(address[] memory targets, uint[] memory values, bytes[] memory calldatas, string memory description) returns (uint)
* ```targets```: The ordered list of target addresses for calls to be made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```values```: The ordered list of values (i.e. msg.value) to be passed to the calls made during proposal execution. This array must be the same length as all other array parameters in this function.
* ```calldatas```: The ordered list of data to be passed to each individual function call during proposal execution. This array must be the same length as all other array parameters in this function.
* ```descriptionHash```: A human readable description of the proposal and the changes it will enact.
* ```RETURN```: The ID of the newly created proposal.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    gov.execute(targets, values, calldatas, descriptionHash).value(999).gas(999)();
    
#### Web3 1.2.6
    const tx = gov.methods.execute(targets, values, calldatas, descriptionHash).send({ from: sender, value: 1 });


### Cancel

A proposal is eligible to be cancelled at any time prior to its execution, including while queued in the Timelock, using this function.

Previously, the cancel function was callable by the proposal creator, or any Ethereum address, if the proposal creator fails to maintain more delegated votes than the proposal threshold.

In the latest version (4.6.0) of the TimelockController smart contract, there is now a separate [canceller role for the ability to cancel](https://github.com/OpenZeppelin/openzeppelin-contracts/pull/3165). The contract introduces a new `CANCELLER_ROLE` that requires set up to be assignable. As such, only addresses with this role will have the ability to cancel. Proposers will no longer be able to cancel. Assigning cancellers can be done by an admin (including the timelock itself) once the role admin is set up.

The canceller can cancel proposals which have been queued but not executed or do not have a ```state == Executed```. The canceller will only cancel proposals in the event of an unforeseen vulnerability. The canceller cannot execute proposals or alter any voting on proposals nor can it prevent users from voting on proposals. The canceller role is assigned to the Euler multisig. On the other hand, the governance smart contract can only be used to cancel proposals that have not been queued for execution within the TimeLockController smart contract.


#### Governance
    function cancel(bytes32 id) public virtual onlyRole(CANCELLER_ROLE)
* ```id```: The governance operation id.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    gov.cancel(id);

#### Web3 1.2.6
    const tx = gov.methods.cancel(id).send({ from: sender });

### Has Voted
Returns weither an address has casted a vote on a proposal ID.

#### Governance
    function hasVoted(uint proposalId, address voterAddress) returns (bool)
* ```proposalId```: ID of the proposal in which to get a voter’s ballot receipt.
* ```voterAddress```: Address of the account of a proposal voter.
* ```RETURN```: true or false.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    boolean hasVoted = gov.hasVoted(proposalId, account);

#### Web3 1.2.6
    const proposalId = 11;
    const voterAddress = '0x123...';
    const result = await gov.methods.hasVoted(proposalId, voterAddress).call();
    const { hasVoted } = result;


### Get Votes (Governance)
Gets the prior number of votes for an account at a specific block number. The block number passed must be a finalized block or the function will revert.

#### Governance
    function getVotes(address account, uint blockNumber) returns (uint96)
* ```account```: Address of the account in which to retrieve the prior number of votes.
* ```blockNumber```: The block number at which to retrieve the prior number of votes.
* ```RETURN```: The number of prior votes.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    uint votes = gov.getVotes(account, blockNumber);

#### Web3 1.2.6
const votes = await gov.methods.getVotes(account, blockNumber).call();


### State
Gets the proposal state for the specified proposal. The return value, ProposalState is an enumerated type defined in the Governance contract.

#### Governance
    function state(uint proposalId) returns (ProposalState)
* ```proposalId```: ID of a proposal in which to get its state.
* ```RETURN```: Enumerated type ProposalState. The types are Pending, Active, Canceled, Defeated, Succeeded, Queued, Expired, and Executed.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    Governance.ProposalState state = gov.state(123);

#### Web3 1.2.6
    const proposalStates = ['Pending', 'Active', 'Canceled', 'Defeated', 'Succeeded', 'Queued', 'Expired', 'Executed'];
    const proposalId = 123;
    result = await gov.methods.state(proposalId).call();
    const proposalState = proposalStates[result];


### Cast Vote

Cast a vote on a proposal. The account's voting weight is determined by the number of votes the account had delegated to it at the time the proposal state became active.

Once an on-chain proposal has been successfully made, 3% of the EUL supply is required to vote ‘yes’ on the proposal in order for it to reach quorum. There is a 7 day period in which people can vote. If a vote passes, there is a 2 day time lock delay on execution during which Euler users can prepare for the change. 

#### Governance
    function castVote(uint proposalId, uint8 support)
* ```proposalId```: ID of a proposal in which to cast a vote.
* ```support```: An integer of 0 for against, 1 for in-favor, and 2 for abstain.
* ```RETURN```: No return, reverts on error.


#### Solidity
    Governor gov = Governor(0x123...); // contract address
    gov.castVote(proposalId, 1);
    
#### Web3 1.2.6
    const tx = gov.methods.castVote(proposalId, 0).send({ from: sender });


### Cast Vote With Reason
Cast a vote on a proposal with a reason attached to the vote.

#### Governance
    function castVoteWithReason(uint proposalId, uint8 support, string calldata reason)
* ```proposalId```: ID of a proposal in which to cast a vote.
* ```support```: An integer of 0 for against, 1 for in-favor, and 2 for abstain.
* ```reason```: A string containing the voter's reason for their vote selection.
* ```RETURN```: No return, reverts on error.

#### Solidity
    Governor gov = Governor(0x123...); // contract address
    gov.castVoteWithReason(proposalId, 2, "I think...");

#### Web3 1.2.6
    const tx = gov.methods.castVoteWithReason(proposalId, 0, "I think...").send({ from: sender });
    
### Cast Vote By Signature
Cast a vote on a proposal. The account's voting weight is determined by the number of votes the account had delegated at the time that proposal state became active. This method has the same purpose as Cast Vote but it instead enables offline signatures to participate in Euler governance voting. For more details on how to create an offline signature, review EIP-712.


#### Governance
    function castVoteBySig(uint proposalId, uint8 support, uint8 v, bytes32 r, bytes32 s)
* ```proposalId```: ID of a proposal in which to cast a vote.
* ```support```: An integer of 0 for against, 1 for in-favor, and 2 for abstain.
* ```v```: The recovery byte of the signature.
* ```r```: Half of the ECDSA signature pair.
* ```s```: Half of the ECDSA signature pair.
* ```RETURN```: No return, reverts on error.

#### Solidity
     Governor gov =  Governor(0x123...); // contract address
    gov.castVoteBySig(proposalId, 0, v, r, s);
#### Web3 1.2.6
    const tx = await gov.methods.castVoteBySig(proposalId, 1, v, r, s).send({});

## TimelockController
Certain smart contracts within the Euler protocol allow the TimelockController smart contract address to modify them. The TimelockController contract can modify system parameters, logic, and contracts in a 'time-delayed, opt-out' upgrade pattern.

The TimelockController has a hard-coded minimum delay of 2 days (48 hours), which is the least amount of notice possible for a governance action. Each proposed action will be published at a minimum of 2 days in the future from the time of announcement.

The TimelockController is controlled by the governance module; pending and completed governance actions can be monitored via the TimelockController.
