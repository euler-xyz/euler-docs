---
description: Learn more about the Euler Governance smart contract parameters
---

# Governance Parameters

## Introduction

This page outlines the governance parameters for both on-chain and off-chain governance.

### On-Chain Governance Parameters

This section outlines the governance parameters for the Euler Governance smart contracts (managed via [Tally](https://www.tally.xyz/governance/eip155:1:0xd8E2114f6bCbaee83CDEB1bD6650a28BBcF144D5)). All parameters are displayed in Table 1 below.

Execution Delay, Voting Delay and Voting Period are based on the assumption of a 15 seconds block creation time on the Ethereum Mainnet.

The governance smart contract inherits functionality from the OpenZeppelin [GovernorSettings.sol module](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/governance/extensions/GovernorSettings.sol) allowing Voting Delay, Voting Period and Proposal Threshold to be updated through an on-chain governance proposal and voting process.

**Table 1** Euler On-Chain Governance Parameters

| Parameter | Value |
|-------|------|
| Voting Delay | 11520 blocks (2 days) |
| Voting Period | 17280 blocks (3 days) |
| Execution Delay | 172800 blocks (2 days) |
| Quorum Numerator | 3% of EUL Supply |
| Proposal Threshold | 75,000 EUL |

When a governance proposal is created, it enters a 2 day review period (i.e., Voting Delay), after which voting weights are recorded and voting begins.

Voting lasts for 3 days (i.e., Voting Period); once the voting period is over, if quorum was reached (enough voting power participated) and the majority voted in favour, the proposal is considered successful and can proceed to be executed 2 days (48 hours) later (i.e., Execution Delay).

Addresses delegated at least 75,000 EUL can create governance proposals having met the Proposal Threshold.

The image below depicts the on-chain governance phases and durations for each phase:

![](<../../.gitbook/governance/governance_process.png>)

### Off-Chain Governance Parameters

This section outlines the governance parameters for off-chain governance (managed via [Snapshot](https://snapshot.org/#/eulerdao.eth/proposal/0x3b4b7e79c40df6860e7d612bdccc4969753e283dfd84673dc5fc4d201abcb317)). All parameters are displayed in Table 2 below.

**Table 2** Euler Off-Chain Governance Parameters

| Parameter | Value |
|-------|------|
| Voting Period | 6 days |
| Quorum | 1,000 EUL |
| Proposal Threshold | 50 EUL |

There is no voting delay or execution delay for the off-chain governance process given there is no direct effect on the protocol's smart contracts.

Addresses holding or delegated at least 50 EUL can create governance proposals having met the Proposal Threshold. With regards to voting power, the delegated voting power or EUL balance at the proposal creation block number is counted towards voting power. The [Snapshot voting strategies](https://docs.snapshot.org/strategies/what-is-a-strategy) enabled are `erc20-balance-of` and `erc20-votes`.
