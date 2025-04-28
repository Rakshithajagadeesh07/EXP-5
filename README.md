# Experiment 5: Zero-Knowledge Proof (ZK) Private Voting System
## Aim:
To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom.

## Algorithm:
Step 1: Voter Registration Each voter generates a secret vote key and submits a commitment (hashed vote) to the contract.

Step 2: Voting Process Voters submit their votes privately using a hash, without revealing their choice.

Step 3: ZK Verification The contract verifies if a vote belongs to a registered voter but does not reveal the actual vote.

Step 4: Vote Counting Once voting ends, the contract reveals the final tally without linking votes to individuals.

## Program:
### Name : Rakshitha J
### Register Number : 212223240135
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZKVoting {
    struct Voter {
        bool registered;
        bytes32 voteCommitment;
    }

    mapping(address => Voter) public voters;
    uint256 public votesForA;
    uint256 public votesForB;

    event VoteCommitted(address voter, bytes32 commitment);
    event VoteRevealed(address voter, uint256 choice);

    function registerVoter(bytes32 commitment) public {
        require(!voters[msg.sender].registered, "Already registered");
        voters[msg.sender] = Voter(true, commitment);
        emit VoteCommitted(msg.sender, commitment);
    }

    function revealVote(string memory secret, uint256 choice) public {
        require(voters[msg.sender].registered, "Not registered");
        require(keccak256(abi.encodePacked(secret, choice)) == voters[msg.sender].voteCommitment, "Invalid proof");

        if (choice == 1) votesForA++;
        if (choice == 2) votesForB++;

        emit VoteRevealed(msg.sender, choice);
    }
}
```
## Expected Output: 
Voters commit their votes privately.

When revealed, the contract verifies correctness but keeps votes anonymous.

Final result is publicly verifiable without exposing individual votes.

## Output:

![Screenshot 2025-04-28 113955](https://github.com/user-attachments/assets/c7b2a015-5571-4ed2-811c-6b3890a9b2ef)

![Screenshot 2025-04-28 114010](https://github.com/user-attachments/assets/f6e76d1f-8280-46fc-9873-c8a994d2357e)

![Screenshot 2025-04-28 114044](https://github.com/user-attachments/assets/5a8061f9-f950-42f2-9096-6fc7c72c2be6)

## High-Level Overview:
Uses ZKPs to ensure anonymous and fair elections.

Prevents vote tampering while maintaining voter privacy.

Mimics real-world ZK voting applications in governance and DAOs.

## Result:
Thus, the execution of Zk Private Voting System has executed Successfully.
