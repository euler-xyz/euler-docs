---
description: Learn more about how to participate in Euler Governance
---

# Voting & Governance

On-chain governance, allows unique features such as delegated voting and proposition powers, rapid protocol (and governance configuration) upgrades via a time lock executor. 
This ensures the protocol can quickly adapt to evolving market conditions, as well as upgrade core parts of the protocol over time.


## General Governance Process

The [General Governance Process](https://forum.euler.finance/t/welcome-to-the-euler-governance-forum/7) is documented on the Governance Forum.

Governance Forum → eIP (Euler Improvement Proposal) → Create Proposal on Snapshot → Create Proposal on Tally → Voting and Execution


## Overview

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

For example, the image below shows active, passed and failed proposals for the Compound protocol:

![](<../.gitbook/assets/proposals.png>)

The image below shows the top voters on proposals created for the Compound protocol:

![](<../.gitbook/assets/top_voters.png>)

Users can also view the total percentage of votes in support or against a specific proposal as shown in the image below:

![](<../.gitbook/assets/votes_in_support_against.png>)

And when voting, users have the option to vote for or against a proposal or an abstain vote as shown in the image below:

![](<../.gitbook/assets/tally-vote.png>)

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


[Delegation process using Tally governance dashboard](https://medium.com/silo-protocol/introducing-silos-on-chain-governance-1de76452072b)



### Delegate

Delegate votes from the sender to a delegatee. Users can delegate to 1 address at a time, and the number of votes added to the delegatee’s vote count is equivalent to the balance of EUL in the user’s account. Votes are delegated from the current block and onward, until the sender delegates again, or transfers their EUL. Delegation can be done via the smart contract function described below or via the Tally user interface.


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


### Timelock (Governance)
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

The canceller can cancel proposals which have not been executed or do not have a ```state == Executed```. The canceller will only cancel proposals in the event of an unforeseen vulnerability. The canceller cannot execute proposals or alter any voting on proposals nor can it prevent users from voting on proposals.


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

## Timelock
Certain smart contracts within the Euler protocol allow the Timelock address to modify them. The Timelock contract can modify system parameters, logic, and contracts in a 'time-delayed, opt-out' upgrade pattern.

The Timelock has a hard-coded minimum delay of 2 days (48 hours), which is the least amount of notice possible for a governance action. Each proposed action will be published at a minimum of 2 days in the future from the time of announcement. Major upgrades, such as changing the risk system, may have a 14 day delay.

The Timelock is controlled by the governance module; pending and completed governance actions can be monitored via the Timelock.
