# Consensus

## Verifiable Random Function (VRF)

Equito Protocol employs a Verifiable Random Function (VRF) to select validators for transaction signing. This cryptographic mechanism takes into validator's EQT tokens when determining its probability of being selected. The more EQT tokens a validator holds, the higher its chances of being chosen. This method eliminates any advantage gained by creating multiple validators, promoting fairness and preventing centralization.

## Equito Protocol Consensus

The Equito Protocol consensus leverages the VRF to establish a secure and efficient method for selecting validators to sign transactions. When a transaction is proposed to the validator network, a committee of validators is randomly selected. This committee's composition is based on the amount of EQT tokens held by each validator. Validators that have more EQT tokens will have a greater influence within the committee. Essentially, it's as if every EQT token participates in its own lottery, ensuring a decentralized and fair selection process. This approach maintains high network performance while allowing all validators in the network an opportunity to be involved.

## Transaction Verification Process

Validator network runs the VRF to determine validators that verify and sign transaction. The selected validators verify and sign the transaction using multi-sig. This signed transaction is then propagated throughout the validator network.

## Validator Rewards

In each transaction verification process, seven validators are selected to participate. As a reward for their contribution to the network's security and consensus, every validator involved in the verification process receives 10% of the transaction fees associated with that transaction. This incentivizes validators to actively participate in maintaining the Equito network's integrity and efficiency.

The Equito consensus mechanism, driven by the EQT token and VRF technology, ensures a fair and decentralized network where all stakeholders have a chance to contribute and be rewarded for their efforts. This innovative approach solidifies the Equito network's ability to finalize transactions efficiently while promoting transparency and fairness within the ecosystem.
