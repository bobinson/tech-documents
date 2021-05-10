# Speak network Storage Mining



[TOC]



## 1. Introduction

This document outlines the process of verifying storage on the SPK Network and how it is rewarded.  For avoidance of doubt, this document only describes storage mining and not the other types of mining in the SPK Network, such as running other Network Mill's Nodes including CDN Nodes, Encoding / Transcoding Nodes and Service Nodes  


### 1.1 Definitions

- In order to make sure there is sufficient decentralisation, the SPK Storage network will have a minimum number of validator nodes before rewards can be distributed.  It will also have a and maximum number of validators in order to prevent sibl attacks.
- **Storage Node:** Servers hosting the files uploaded into the speak network are designated as storage nodes. Each node will have a unique NAI aka adress on the Peerplays blockchain. These nodes can choose to mine BROCA and SPEAK by staking LARNYX. The storage nodes must use IPFS protocol and publicly share the DLT for anyone to access. Each node in the network is incetivised to maintain new files, rare files and as large a percentage of the entire Network as possible. 
- **Validator nodes:** These are high performance servers mapped with validator blockchain accounts. Each of the validator nodes must have LARNYX tokens staked to become eligible for rewards for the services provided to the network. Each validator node receives SPEAK and BROCA tokens on the completion of verification or validation work.  The dispersal of tokens happens immediately after the verification-validation round is completed. 
- **Verification:** Validators verify storage node proofs by downloading and verifying the files hosted by the storage node undergoing verification.
- **Confirmation**: The process by which a threashold number of validator nodes confirm a verification.  Once a threashold of confirmations is reached, payouts are executed.  Each validator that performs a confirmation, stores the data to the DPoS blockchain which can then be picked up by other validators who can also assist in carrying out a confirmation of the claim. 

- **Payouts**:
  - A storage node receives exponentially more rewards in BROCA and SPEAK based on the amount of LARNYX staked.  This disincentivises miners pretending to be two or more separate nodes on the Network so that they can mine more rewards for themselves whilst increasing competition for LARYNX Miner Tokens.   
  - A validator node receives exponentially more rewards in SPEAK and BROCA proportionally to the amount of LARNYX staked.  They are rewarded upon executing verifications or carrying out a confirmation.
  - Since the recall block is selected at random selection of file claim is random, it may also happen that a storage node will never get paid or won't get paid for a long period of time. This situation can be changed by ensuring hosting rare files, new files and hosting larger percentage or even the entire storage network.

**Proof of Storage** : claim and proof need do define (TODO)

**Timeout**:  Each validator node must complete the verification or validation process in pre-defined, configurable time window defined as *validator timeout*. This timeout is essential to ensure that storage nodes are able to provide fast uplink and the validator nodes has enough CPU and network capacity to perform validation within finite time periods.

### 2. Storage Nodes



register > active > maintenance > unregister



## 3.1 Validator nodes

Any SPEAK network user can register themselves as a validator & run a validator node. 



A validator node can have the following 4 states. 

- *register*
- *active*
- *maintenance* 
- *un-register*

### 3.1.1 registration

A Speak network user can stake SPEAK tokens of certain pre-defined miner-denominations and become a validation node. Until the user announces his readiness to take part in the network by broadcasting a heart, the node will remain in registered mode. The only earning might be the earning that will be possible from the SIP which will be introduced later. Once registered a validator node may choose to copy a part of the IPFS network to assist with verification and validation of storage claims.

### 3.1.2 *active* validator node

A validator node can start sending heart beats to the blockchain by raising  proposals or sending heart beats signature to the the *custom_json* filed for more than 3  times for a period of 60  block times will be considered as active nodes. The nodes whose state are active & with enough votes will be eligible to take part in the validation process. Any node failing to maintain the heart beats for continuous periods of time without manually announcing to be in maintenance mode will loose reputation.

An active validator node will be elected in a round robin fashion to verify and validate the storage claims by the storage nodes.

At any point in time the minimum cardinality of the active validator node set should be eleven for the mining and validation to work.

### 3.1.3 maintenance mode

An active validator node announce its state to be changing to maintenance of technical reasons or any other reasons. This ensures that any node in the network can perform routine activity or upgrade.

Any node that is missing the heart beat for 60 blocks will be marked as in maintenance and will be penalised. 

Maintenance to active state transition must be done manually.

### 3.1.4  unregister 

Any node in the maintenance node can announce to resign from the network by invoking unregister routine.



## 3.2 Verification and Validation

The validator nodes can perform its duties namely verification and validation provided the network has a minimum of 11 validation nodes and 13 storage nodes.

Verification or validation process for each file must be completed with 300 seconds. If any node spends more than 300 seconds to complete the steps, that particular node must issue timeout so that next validator can take up the work.

Each storage node who wants to participate in the SPEAK mining be accessible to the validator nodes in the network. Registered and active storage nodes will be considered for SPEAK mining if they have LARNYX staked.  Every 300 seconds, the validator nodes will look up the NodeID, fetch the DLT id and the list of all files hosted by all the eligible storage nodes in the speak network.

A data structure with NodeID, DLT_id and unique_PeerIDs will be created. From this data structure, the following will be identified.

[CATEGORY 1] files which are stored by smaller number of nodes (find the rarest)
[CATEGORY 2 ] files which are pinned by all nodes or most nodes
(CATEGORY 3) A total random file

[CATEGORY 4] Newest files

one node hosting the files in CATEGORY 1, CATEGORY 2  , CATEGORY 3, CATEGORY 4  will  be selected for the reward for that period with extra weights for CATEGORY 2 and CATEGORY 4 (highest weigt).

*ie*

```pascal
Random_Select(CAT1, CAT2, CAT3) = potential_reward_winner


```

This will provide us with a list of potential reward winner storage node(s). Now we need a second iteration of checks to ensure the files sizes published by the member nodes in potential_reward_winner list is same as they are claiming. Randomly select a node from the potential_reward_winner and then download the previously announced file from the node. The file should meet all the data or other parameters published by the node. This can be done for one or more than one of the potential_reward_winners if the first step fails.

```pascal
Verify_file(potential_reward_winner) = final_winner_before_validation


```

winner can be then given certain number of SPEAK based on the LARNYX miner (stake) they have.

The random number generator itself will be a provable fair on chain random number generator.

To incentive newer files, we can find files which are added newly to the IPFS DLT and in the above reward process provide additional weight to them. 

## 3.3 Selecting Validator nodes

Validator nodes who wants to earn rewards must publish their intention to do so and must get elected by SPEAK network users to earn rewards. The rewards earned will proportional to the votes received and SPEAK staked in to the LARNYX miners. The validator nodes will be considered for mining rewards only if they receive minimum 2 votes & has SPEAK staked. This requirement combined with the need to complete the verification or validation process in a time window of 30 minutes will ensure that no single node can earn rewards without providing active contribution and acceptance from the network. Even a certain user amasses large amounts of LARNYX, unless she stakes and also participates in the network by contributing work, she can't earn the rewards. 

### 3.3.1 Storage requirements of validator node
Each validator node is expected to store a substantial percentage of the network. Since each of verfication and validation step has a timeout, to earn maximum rewards each validation node must keep maximum storage as possible.

TODO: how to ensure that multiple validator and storage nodes are not sharing the same physical infrastructure ?

### 3.3.2 Maximum number of validator nodes

TODO : max number of validator nodes, consensus nodes, how to ensure there are backup validator nodes

## 3.X Validator node Blockchain communication

The validator nodes also should operate 3PSEAK SONs to communicate with the Peerplays blockchain. The selection of validator nodes will also elect the SPEAK SONs on the Peerplays blockchain. 



The SPEAK SONs will act similar to the Peerplays - Bitcoin SONs and received well formatted, predefined data from the Validators nodes and raise proposals on the Peerplays blockchain which will result in crediting SPEAK tokens to the storage miners. 

