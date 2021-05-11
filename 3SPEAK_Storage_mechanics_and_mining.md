
# 3speak network Storage mechanics and mining



[TOC]



## 1. Introduction

This document outlines the process of verifying storage on the 3SPEAK network and the rewards. 



### 1.1 Definitions

- The 3SPEAK Storage network will have a minimum 13 validator nodes and 15 storage nodes
- **Storage Node:** Servers hosting the files uploaded into the speak network are designated as storage nodes. These nodes can choose to mine LARNYX by staking SPEAK. The storage nodes must use IPFS protocol and publicly share the DLT for anyone to access. The end users may choose to manually select and upload files to any storage node. Each node in the network is encouraged to maintain new files, rare files and in general a large percentage or the entire files if possible.
- **Validator nodes:** These are high performance servers mapped with validator blockchain accounts. Each of the validator nodes must have SPEAK tokens staked to become eligible for rewards for the services provided to the network. Each validator node received LARNYX token on verification or validation work done by them & the dispersal of token will happen immediately after the verification-validation round is completed. 
- **Verification** : The validators verify the claim by a storage node by downloading and verifying the size of files hosted by storage nodes. This process is defined as verification.
- **Validation**: Once a  validator node verifies a claim by a storage node, it has to be validated by 2 more validators in the network to reach consensus & compete claim approval. For this each validator that performs the verification, stores the data to the blockchain which can then be picked by other validators and validate the claim. When 2 validator nodes validates a verification proposal, the claim is approved and sent to the blockchain for payout processing.
- **Payouts**:
  - A storage node receives rewards in LARNYX proportional to the SPEAK staked upon a claim is validated by 3 validator nodes
  - A validator node received rewards in LARNYX proportional to the SPEAK staked upon either its verification of a claim is validated by two other validator nodes or if it performed validation, upon the verification, validation round completes.
  - Since the selection of file claim is random, it may also happen that a storage node will never get paid or won't get paid for a long period of time. This situation can be changed by ensuring hosting rare files, new files and hosting larger percentage or even the entire storage network.

**Proof of Storage** : claim and proof need do define (TODO)



### 2. Storage Nodes



register > active > maintenance > unregister



## 3.1 Validator nodes

Any 3SPEAK network user can register themselves as a validator & run a validator node. 



A validator node can have the following 4 states. 

- *register*
- *active*
- *maintenance* 
- *un-register*

### 3.1.1 registration

A 3speak network user can stake SPEAK tokens of certain pre-defined miner-denominations and become a validation node. Until the user announces his readiness to take part in the network by broadcasting a heart, the node will remain in registered mode. The only earning might be the earning that will be possible from the SIP which will be introduced later. Once registered a validator node may choose to copy a part of the IPFS network to assist with verification and validation of storage claims.

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

Each storage node who wants to participate in the LARNYX mining be accessible to the validator nodes in the network. Registered and active storage nodes will be considered for LARNYX mining if they have SPEAK staked.  Every 300 seconds, the validator nodes will look up the NodeID, fetch the DLT id and the list of all files hosted by all the eligible storage nodes in the speak network.

A data structure with NodeID, DLT_id and unique_PeerIDs will be created. From this data structure, the following will be identified.

[CATEGORY 1] files which are stored by smaller number of nodes (find the rarest)
[CATEGORY 2 ] files which are pinned by all nodes or most nodes
(CATEGORY 3) A total random file

[CATEGORY 4] Newest files

one node hosting the files in CATEGORY 1, CATEGORY 2  , CATEGORY 3, CATEGORY 4  will  be selected for the reward for that period with extra weights for CATEGORY 2 and CATEGORY 4.

*ie*

```pascal
***Random_Select(CAT1, CAT2, CAT3) = potential_reward_winner***


```

This will provide us with a list of potential reward winner storage node(s). Now we need a second iteration of checks to ensure the files sizes published by the member nodes in potential_reward_winner list is same as they are claiming. Randomly select a node from the potential_reward_winner and then download the previously announced file from the node. The file should meet all the data or other parameters published by the node. This can be done for one or more than one of the potential_reward_winners if the first step fails.

```pascal
*Verify_file(potential_reward_winner) = final_winner_before_validation*


```

winner can be then given certain number of LARNYX based on the SPEAK miner (stake) they have.

The random number generator itself will be a provable fair on chain random number generator.

To incentive newer files, we can find files which are added newly to the IPFS DLT and in the above reward process provide additional weight to them. 

## 3.3 Selecting Validator nodes

Validator nodes who wants to earn rewards must publish their intention to do so and must get elected by 3SPEAK network users to earn rewards. The rewards earned will proportional to the votes received and SPEAK staked in to the LARNYX miners. The validator nodes will be considered for mining rewards only if they receive minimum 2 votes & has SPEAK staked. This requirement combined with the need to complete the verification or validation process in a time window of 30 minutes will ensure that no single node can earn rewards without providing active contribution and acceptance from the network. Even a certain user amasses large amounts of SPEAK, unless she stakes and also participates in the network by contributing work, she can't earn the rewards. 



TODO : max number of validator nodes, consensus nodes, how to ensure there are backup validator nodes

## Validator node Blockchain communication

The validator nodes also should operate 3PSEAK SONs to communicate with the Peerplays blockchain. The selection of validator nodes will also elect the 3SPEAK SONs on the Peerplays blockchain. 



The 3SPEAK SONs will act similar to the Peerplays - Bitcoin SONs and received well formatted, predefined data from the Validators nodes and raise proposals on the Peerplays blockchain which will result in crediting LARNYX tokens to the storage miners. 

