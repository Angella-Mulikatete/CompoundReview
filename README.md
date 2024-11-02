# GovernorBravo Smart Contract
| Title            | Smart Contract Review Report  |
|------------------|-------------------------------|
| **Target**       | GovernorBravoDelegateG2       |
| **Version**      | 1.0                           |
| **Author**       | Angella Mulikatete            |
| **Classification** | Public                      |
| **Status**       | Draft                         |
| **Date Created** | 2nd Nov, 2024                 |

---

### Table of Contents
1. [INTRODUCTION](#10-introduction)  
   1.1 [About Me](#11-about-me)  
   1.2 [Skills](#12-skills)      
   1.3 [Links](#13-links)  
   1.4 [Compound Protocol](#14-compound-protocol)  
   1.5 [Compound Governance](#15-compound-governance)  
   1.6 [GovernorBravoDelegate](#16-governorbravodelegate)  
   1.7 [Contracts Structure](#17-contracts-structure)  
2. [CONTRACT REVIEW](#20-contract-review)  
3. [FINDINGS](#30-findings)  
   3.1 [Qualitative Analysis](#31-qualitative-analysis)  
   3.2 [Summary](#32-summary)  
   3.3 [Recommendations](#33-recommendations)  
4. [CONCLUSION](#40-conclusion)  


---

### 1.0 INTRODUCTION

#### 1.1 About Me  
Hello, I'm Angella Mulikatete, a Software Engineer, Smart Contract Developer. My background is grounded in Web2,web3(blockchain development), with a focus on producing secure, efficient smart contracts that can reshape how we interact with digital assets.

#### 1.2 Skills  
- Solidity, Diamond Standard, Foundry, Hardhat, React, Nestjs, Laravel, NextJs
#### 1.3 Links  
- [LinkedIn](https://www.linkedin.com/in/angella-mulikatete-7b83371a2/)  
- [Twitter](https://x.com/AMulikatete)  

---
### 1.4 Compound Protocol
The Compound Protocol is a decentralized finance (DeFi) application that allows users to lend and borrow cryptocurrencies in a trustless manner. It operates on the Ethereum blockchain and is known for its algorithmic interest rate model that adjusts based on supply and demand

####  Components of the Compound Protocol

1. **Lending and Borrowing**: DUsers can supply assets to the Compound protocol to earn interest or borrow assets by providing collateral. The protocol calculates interest rates algorithmically based on the current utilization of the assets.
2. **cTokens**: When users supply assets to Compound, they receive cTokens in return. These tokens represent the user's share in the Compound pool and accrue interest over time. For example, if a user supplies DAI, they receive cDAI, which can be redeemed for the underlying DAI plus interest.
3. **Interest Rates**:  Interest rates in Compound are dynamic and vary based on the supply and demand of each asset. Users can see current interest rates for lending and borrowing on the platform.
4. **Collateralization**:To borrow assets, users must provide collateral. The collateral must exceed the value of the borrowed assets to ensure the protocol's solvency. If the value of the collateral falls below a certain threshold, it can be liquidated to cover the loan.
5. **Governance**: Compound is governed by its community of token holders who hold COMP tokens. These tokens grant governance rights, allowing holders to propose changes to the protocol, vote on proposals, and influence future developments.
   
### 1.5 Compound Governance
Compound Governance refers to the decentralized governance system employed by Compound Finance, a prominent decentralized finance (DeFi) protocol. Compound Finance is built on the Ethereum blockchain and provides lending and borrowing services for various cryptocurrencies.

The governance mechanism allows token holders to participate in the decision-making process regarding the protocol's development, changes, and upgrades. The native token of Compound, COMP, plays a central role in this governance system.

####  Components of the Compound Governance

1. **COMP Token**: The COMP token is the native governance token of the Compound Protocol. Users can earn COMP tokens by supplying or borrowing assets on the platform. COMP holders can participate in governance by voting on proposals or creating new proposals.
2. **Governance Proposals**: Any user with COMP tokens can submit governance proposals. These proposals can include changes to the protocol parameters, such as interest rates, collateral factors, or the addition of new assets.
3. **Voting Mechanism**:  Proposals are voted on by COMP holders. Each token represents one vote, and proposals require a majority of votes to pass. Voting takes place over a defined period, typically one week.
4. **Timelock**:Once a proposal is passed, it goes into a timelock period before implementation. This provides an opportunity for users to respond to the proposal before it is enacted.

### 1.6 GovernorBravoDelegate  
GovernorBravoDelegate contract is an implementation of the governance mechanism used in Compound. It is a contract that handles the logic for proposing and voting on changes to the protocol

####  Components of the Compound Governance

1. **Proposal Creation**: Users can create proposals that specify actions to be taken, including calling specific functions on other contracts with parameters defined in the proposal.
2. **Voting Process**: The contract manages the voting process, allowing users to cast their votes for or against proposals during a specified voting period.
3. **Proposal States**: Proposals can have various states, including Pending, Active, Canceled, Succeeded, Queued, Expired, and Executed. The state of a proposal dictates what actions can be taken at any given time.
4. **Vote Recording**:The contract records votes and maintains receipts that track which addresses voted and how they voted.
5. **Implementation Upgrades**: The `GovernorBravoDelegate` also allows for upgrades to the governance logic itself by enabling a new implementation address to be set, which is important for evolving the governance mechanisms.
6. **Whitelist Management**: The contract may incorporate features for managing a whitelist of accounts that can participate in certain governance activities.
7. **Vote Recording:**:The `GovernorBravoEvents` contract emits events during key actions, such as proposal creation, voting, and changes to governance parameters, which helps in tracking the protocol's governance activities on-chain.

### 1.7 Contracts Structure

1. **GovernorBravoEvents**: Defines all events emitted during governance activities.
2. **GovernorBravoDelegatorStorage**: Contains base storage variables and access control (`admin`, `pendingAdmin`).
3. **GovernorBravoDelegateStorageV1**: Stores parameters for proposal and voting configuration (`votingDelay`, `votingPeriod`, `proposalThreshold`).
4. **GovernorBravoDelegateStorageV2**: Adds whitelisting capabilities, allowing specified accounts to perform actions under the guardian’s management.
5. **Interfaces**:
   - **TimelockInterface**: This interface defines the functions that can be called on the Timelock contract. The delay function returns the delay period specified in the Timelock contract. The GRACE_PERIOD function returns the grace period specified in the Timelock contract. The acceptAdmin function is used to accept the admin role for the Timelock contract. The queuedTransactions function is used to check whether a transaction with the specified hash has been queued in the Timelock contract. The queueTransaction function is used to add a transaction to the queue in the Timelock contract. The cancelTransaction function is used to cancel a transaction that has been queued in the Timelock contract. The executeTransaction function is used to execute a transaction that has been queued in the Timelock contract.
   - **CompInterface**:This interface defines the functions that can be called on the COMP token contract. The getPriorVotes function is used to get the number of votes that an account had at a specific block number. This function is used in the governance system of the Compound protocol to determine the voting power of token holders.
   - **GovernorAlpha**:This interface defines the function that can be called on the GovernorAlpha contract. The proposalCount function returns the total number of proposals (state variable) that have been created in the governance system of the Compound protocol. This function is used to keep track of the number of proposals.

---

### 2.0 CONTRACT REVIEW
SPDX License and Solidity Version Declaration
```
// SPDX-License-Identifier: BSD-3-Clause
pragma solidity ^0.8.10;
```
The SPDX identifier indicates the license type (BSD-3-Clause), which is a permissive license.
The pragma statement sets the Solidity version to 0.

The contract contains the following state constant variables:
```
string public constant name = "Compound Governor Bravo";
```
This line sets the name of the contract to "Compound Governor Bravo." It’s a public, constant variable, meaning it cannot be changed after deployment and helps identify the contract’s purpose for users and interfaces interacting with it.
```
uint public constant MIN_PROPOSAL_THRESHOLD = 50000e18; // 50,000 Comp
uint public constant MAX_PROPOSAL_THRESHOLD = 100000e18; // 100,000 Comp
```
Proposal Threshold is the minimum amount of COMP tokens a user needs to propose changes to the Compound protocol.
These constants define the minimum (MIN_PROPOSAL_THRESHOLD) and maximum (MAX_PROPOSAL_THRESHOLD) values for this threshold. The values are set at 50,000 COMP and 100,000 COMP, respectively, allowing flexibility within these boundaries.
This range is crucial for balancing accessibility with security. Setting the threshold too low could allow low-value proposals that clutter governance, while setting it too high could restrict participation to only large holders.

```
uint public constant MIN_VOTING_PERIOD = 5760; // About 24 hours
uint public constant MAX_VOTING_PERIOD = 80640; // About 2 weeks
```
Voting Period refers to the duration over which a proposal is open for voting. Here, it ranges from a minimum of about 24 hours to a maximum of about 2 weeks (depending on block times).
These limits ensure that proposals have a reasonable time window for participation, which supports adequate debate and consensus while preventing extended periods that could delay protocol updates.

```
uint public constant MIN_VOTING_DELAY = 1;
uint public constant MAX_VOTING_DELAY = 40320; // About 1 week
```
Voting Delay is the time between the proposal’s submission and the start of the voting period. This delay allows token holders to prepare for voting on the proposal.
With a minimum delay of 1 and a maximum of about 1 week, this parameter ensures that there’s enough time to notify stakeholders, yet not too long to delay governance unnecessarily

```
uint public constant quorumVotes = 400000e18; // 400,000 = 4% of Comp
```
Quorum Votes is the number of votes required for a proposal to be considered valid. For this contract, it’s set at 400,000 multiplied by 10^18 COMP (4% of the total COMP supply).
This ensures that proposals can only pass if they achieve enough community support, preventing low-turnout decisions that may not reflect the will of the wider Compound community.

```
uint public constant proposalMaxOperations = 10; // 10 actions
```
This constant limits each proposal to a maximum of 10 actions (such as function calls or state changes).
```
bytes32 public constant DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,uint256 chainId,address verifyingContract)");
```
EIP-712 is a standard for typed, structured data hashing and signing. This `DOMAIN_TYPEHASH` value helps create the domain separator for EIP-712-compliant signatures.
The domain separator ensures that signatures are bound to this specific contract (and not reused in other contexts), providing security for off-chain voting through signed messages.

```
bytes32 public constant BALLOT_TYPEHASH = keccak256("Ballot(uint256 proposalId,uint8 support)");
```
This `BALLOT_TYPEHASH` is the EIP-712 typehash used for votes or “ballots” cast by users. It specifies the structure of the data to be signed, including the proposal ID and the support type (e.g., for, against).

The following functions are part of the compound governance contract

#### 2.1 initialize()
```
  function initialize(address timelock_, address comp_, uint votingPeriod_, uint votingDelay_, uint proposalThreshold_) public {
        require(address(timelock) == address(0), "GovernorBravo::initialize: can only initialize once");
        require(msg.sender == admin, "GovernorBravo::initialize: admin only");
        require(timelock_ != address(0), "GovernorBravo::initialize: invalid timelock address");
        require(comp_ != address(0), "GovernorBravo::initialize: invalid comp address");
        require(votingPeriod_ >= MIN_VOTING_PERIOD && votingPeriod_ <= MAX_VOTING_PERIOD, "GovernorBravo::initialize: invalid voting period");
        require(votingDelay_ >= MIN_VOTING_DELAY && votingDelay_ <= MAX_VOTING_DELAY, "GovernorBravo::initialize: invalid voting delay");
        require(proposalThreshold_ >= MIN_PROPOSAL_THRESHOLD && proposalThreshold_ <= MAX_PROPOSAL_THRESHOLD, "GovernorBravo::initialize: invalid proposal threshold");

        timelock = TimelockInterface(timelock_);
        comp = CompInterface(comp_);
        votingPeriod = votingPeriod_;
        votingDelay = votingDelay_;
        proposalThreshold = proposalThreshold_;
    }
```
This initialize function in the GovernorBravoDelegate contract is used in setting up the Compound governance contract's parameters and dependencies.  It sets core configuration parameters that define how governance proposals will be created, voted on, and executed. This function is only called once, as indicated by the require checks, and it can only be called by the contract’s admin.

#### Parameters:
1. **address timelock_**: Address of the Timelock contract, which enforces a delay for executing proposals. This delay ensures time for users to adjust positions before a passed proposal is executed.
2. **address comp_**: Address of the COMP token contract, which is the governance token of Compound. Only users holding COMP can vote and participate in governance.
3. **uint votingPeriod_**: Duration of the voting period (in blocks), determining how long a proposal is open for voting.
4. **uint votingDelay_**: Delay (in blocks) between the proposal creation and the start of voting, allowing users to prepare before voting begins.
5. **uint proposalThreshold_**: Minimum amount of COMP tokens required to create a proposal. This helps prevent spam by ensuring that only significant stakeholders can propose changes.

#### KeyChecks

1. `require(address(timelock) == address(0), "can only initialize once")`: Ensures that the contract is initialized only once by checking that the timelock address has not been set previously. This prevents reinitialization, which could disrupt governance settings.
2. `require(msg.sender == admin, "admin only")`: Ensures that only the admin (presumably the deployer or a trusted account) can initialize the contract, providing security against unauthorized changes.
3. `require(timelock_ != address(0), "invalid timelock address")` and `require(comp_ != address(0), "invalid comp address")`: Verifies that valid addresses are passed for the Timelock and COMP contracts. Null addresses would cause errors in governance functionality.
4. `require(votingPeriod_ >= MIN_VOTING_PERIOD && votingPeriod_ <= MAX_VOTING_PERIOD, "invalid voting period")`: Ensures the votingPeriod falls within allowed boundaries (e.g., between a minimum and maximum number of blocks). This prevents setting unreasonably short or long voting periods, which could disrupt governance.
5. `require(votingDelay_ >= MIN_VOTING_DELAY && votingDelay_ <= MAX_VOTING_DELAY, "invalid voting delay")`: Validates that the votingDelay is within a set range to ensure fair participation.
6. `require(proposalThreshold_ >= MIN_PROPOSAL_THRESHOLD && proposalThreshold_ <= MAX_PROPOSAL_THRESHOLD, "invalid proposal threshold")`: Validates the proposalThreshold, ensuring it is neither too low (which could lead to spam) nor too high (which could prevent genuine governance).

#### Setting statevariables

1. `timelock = TimelockInterface(timelock_)`:  Sets the timelock address, allowing proposals to be subject to a delay after they pass but before they are executed.
2. `comp = CompInterface(comp_)`: Sets the comp address, enabling the contract to interact with the COMP token for governance rights.
3. `votingPeriod = votingPeriod_, votingDelay = votingDelay_, proposalThreshold = proposalThreshold_`: Sets the votingPeriod, votingDelay, and proposalThreshold variables with the provided values, configuring the governance process parameters.

   







