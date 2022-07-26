---
description: Learn more about the Euler On-Chain Governance launch phases
---

# On-Chain Governance Launch Phases

## Introduction

EulerDAO will kick off in three phases for a guarded launch towards full decentralisation of the Euler protocol. Each phase is described below.

The EulerDAO uses the [OpenZeppelin Governance smart contracts](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/governance) (version 4.6.0) for governance (as well as the EUL token contract). It is a governance protocol — similar to the one Compound uses — where delegates vote on active proposals to make changes to the EulerDAO and Euler protocol.

Euler uses the Tally governance dashboard application to manage the governance process. Through Tally, you can set up your wallet to become a delegate, create on-chain proposals, vote on active proposals, discover delegates in the community, and delegate your voting power to a community member.

## Phase 1

The first phase of the launch will be such that actions to be performed directly on the Euler protocol smart contracts will be executed by the Euler team on behalf of the community. In this case, all on-chain governance proposals will point to or target a function in a stub smart contract (in place of the Euler protocol smart contracts).

Should the proposal become successful and executed, the target function will then be executed (via the TimelockController controller smart contract). It will emit the proposal description string and proposal transaction data, which will then be validated by the Euler team and executed against the Exec module via the Euler multisig.

Hence, the `governorOnly()` modifier in the Euler Governance module smart contract will be checking that the caller of its functions is the Euler mulisig and not the TimelockController smart contract.

To create the proposal transaction data, we have implemented a [tool](https://proposal.euler.finance/) which will help the proposer to auto generate this depending on what actions should be executed.

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

# Euler's Governance Proposal Creation Tool for Phase 1

## Introduction

The first phase of Euler’s DAO / Governance launch will be semi-decentralised wherein actions to be performed directly on the Euler protocol smart contracts will be performed or executed by the Euler team on behalf of the community. In this case, all on-chain governance proposals will point to or target a function in a stub smart contract (in place of the Euler protocol smart contracts).

Should the proposal become successful and executed, the target function will then be executed (via the TimelockController controller smart contract. It will emit the proposal description string and proposal transaction hex data, which will then be validated by the Euler team and executed against the `Exec` module via the Euler multisig (on OpenZeppelin Defender).

Hence, the `governorOnly()` modifier in the [Euler Governance module](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Governance.sol) will be checking that the caller of its functions is the Euler mulisig and not the TimelockController smart contract of the DAO.

To create the proposal transaction data, we have implemented a [tool](https://proposal.euler.finance/) which will help the proposal creator to auto-generate it depending on what actions should be executed. The proposal transaction data is simply an encoded version of the on-chain transaction to the Exec module’s batchDispatch function.

The rest of the article will describe the process of creating the proposal transaction data on Euler’s governance proposal creation tool and using the generated proposal transaction data to create an on-chain proposal on the [Tally](https://www.tally.xyz/) governance dashboard.

## Section 1. Creating the proposal transaction data for Euler’s Exec Module

### Step 1

Navigate to the [proposal transaction data creation tool](https://proposal.euler.finance/).

The web application should look like the following image:

![](<../../.gitbook/governance/gov_tool_1.png>)

### Step 2

The tool requires MetaMask to be installed in your browser.
Switch your MetaMask wallet to mainnet.

The tool currently supports the Ethereum Mainnet and our Ropsten testnet Exec modules. It will create the appropriate transaction data to be executed depending on the selected network.

### Step 3

At the top left of the window, we have a text field for proposal description and below that we have a dropdown menu representing a list of tokens, e.g., USDC, DAI, etc.

At the left of the window, under the token list, we have a set of dropdown menus and text fields which will be autopopulated with the current token configurations (if the token has an activated market on Euler).

To create the proposal transaction data, the proposer needs to enter a proposal description and then select a token from the token list. Once selected, the rest of the fields will be automatically populated with the current configuration of the token or market on Euler if it has an activated market.

The image below shows the proposal description and the fields on the left populated with the current market configuration for USDC on Euler:

![](<../../.gitbook/governance/gov_tool_3.png>)

### Step 4

The proposer can then make modifications and generate the proposal transaction hex data to be executed via the Euler Exec module (`batchDispatch()` function) and use this hex data as the input to the target function in the stub smart contract when creating a proposal on Tally (this is described in Section 2 below).

For example purposes, let’s change the borrow factor of USDC to 0.6. To do this, we simply change the current collateral factor to 0.6 in the text field on the left side of the screen for collateral factor and click on `CREATE PROPOSAL DATA`. Once we do this, we should see the markdown table showing the changes we want to make to the asset. We will also see the batch items Hex transaction data which we need for our on-chain governance proposal stub smart contract on Tally.

![](<../../.gitbook/governance/gov_tool_4_i.png>)

Note: This process can be repeated for multiple tokens and configurations (or multiple configurations of the same token). They will be added in a batch and encoded to form the transaction data for the batchDispatch functionality in the Euler Exec module.

For example, let us select DAI from the token list and change the borrow factor of DAI to 0.3. Again, the fields are automatically populated when we select DAI and when we change the borrow factor to 0.3 and click on `CREATE PROPOSAL DATA`. The list of configuration updates is updated to reflect the change we are making to DAI, while the USDC update information still remains. The transaction hex is also updated.

![](<../../.gitbook/governance/gov_tool_4_ii.png>)

### Step 5

To validate the updates we have selected, we can copy the auto-generated hex under batch items hex TX data (under batch items, which is under proposal description) and click on `DEBUG TX HEX DATA` and paste the copied hex into the text field.

The tool should also decode the hex and show us a markdown with the updates the Euler team will be applying to the selected tokens once the proposal gets executed. The Euler team will also follow this process to make sure that the proposal description reflects the updates to be made before executing the transaction in the Exec module on behalf of the community.

![](<../../.gitbook/governance/gov_tool_5.png>)

As shown in the image above, the hex data is decoded to show the updates we selected to be applied to DAI and USDC. There is a close button at the bottom right of the window to close the debug modal and return to the main page.

Once you get to this point, you now have your proposal transaction data which you can use to create your on-chain proposal on Tally. After the voting period, if successfully executed, the decoded hex data will be submitted to OpenZeppelin Defender for the Euler team to execute on behalf of the community.

Please let us know if you have any questions or feedback while using the tool in our Discord Governance channel.

## Section 2.Using the Auto-Generated transaction data for Euler’s Exec Module to Create an on-chain proposal for the DAO on Tally

At this point, we assume you now have the proposal transaction hex data needed for the Euler Exec module’s batchDispatch function. And you want to create the on-chain proposal for members of the community (and delegates) to vote on. If so, please read on!

Below, we will describe the steps required to accomplish this goal.

### Step 1

Head over to the EulerDAO dashboard on Tally and connect your MetaMask wallet.

### Step 2

Click on `Create new proposal` at the right corner of the window.

![](<../../.gitbook/governance/dao_1_tally_2.png>)

It should then take you to the proposal creation window below.

![](<../../.gitbook/governance/dao_1_tally_2i.png>)

Click on `Continue` to move onto the next step (`Name your proposal`).

### Step 3

Enter a proposal title and description and click `Continue`.

![](<../../.gitbook/governance/dao_1_tally_3.png>)

### Step 4

In the next section, you will be required to specify the governance proposal actions, i.e., target smart contract, target function and parameters. The Tally dashboard allows you to specify multiple actions in a single proposal which will be called/executed if the proposal is successful and executed.

![](<../../.gitbook/governance/dao_1_tally_4_i.png>)

To add the proposal transaction hex from Section 1 and set the governance stub contract as the target smart contract, we will click on `Add custom action` => enter the stub smart contract address as the target smart contract. Then select the `executeProposal` function from the dropdown menu under `contract method` as the target function in the target smart contract. Here is the interesting part: enter the required parameters, i.e., proposal description string and the proposalData which is your proposal transaction hex data from Section 1.

![](<../../.gitbook/governance/dao_1_tally_4_ii.png>)

### Step 5

Once done, click continue and review the proposal. Once you are happy, you can click `Submit on-chain` which will open a MetaMask pop-up window for you to sign the transaction to create the proposal on-chain, via the Governance smart contract.

![](<../../.gitbook/governance/dao_1_tally_5.png>)
