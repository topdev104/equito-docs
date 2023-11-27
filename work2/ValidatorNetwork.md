# Equito Finace Bridge Document

## Explore Equito Finance Bridge

### Network Architecture

#### Equito Brdige Network

The Equito Bridge Network is controlled by on-chain smart contracts powering the protocol, oracles that transfer data from one network to another and validators that authenticate transactions on the network. The network is uncontrolled and maintains security by ensuring validators run the same process upon receiving the various chains events. Only when two-thirds of validators have signed the same transaction with their key collectively, the network achieves consensus.

![Equito Bridge Network](./images/equito-bridge-network.png)

#### Protocol Layers

The Bridge Network protocol consists of three main layers:

1. Application Layer - Made up of all the cross-chain tools
   Any cross-chain tool can be built on the Bridge Network application layer and plugged into the blockchain and protocol layer. The Application layer supports different kinds of applications like the token bridge, cross-chain messaging, and others in the works.
2. Blockchain Layer (smart contracts) - Contains contracts for supported blockchains and oracles that act as data relayers.
3. Protocol Layer (validator network) - Combines the blockchain layer with the validators.
   Every cross-chain transaction initiated through bridge contracts is assigned a unique identifier (hash). Bridge validators track every transaction that passes through the smart contract of the protocol and soon as the transaction achieves its entirety, each validator is required to sign the transaction by its private key, all the while the oracle transfer the data to different chains.

### Benefits of Equito Bridge

Equito Bridge offers several advantages over traditional cross-chain transaction methods:

- **Cost-Efficiency**: The protocol significantly reduces gas fees by verifying only one multi-signature transaction, making cross-chain transactions more affordable.

- **Enhanced Scalability**: Equito Bridge's approach enhances the scalability of cross-chain transactions, allowing for increased throughput and faster processing times.

- **Security**: Ed25519 signatures and Zero-Knowledge Proofs provide a high level of security, ensuring the integrity and privacy of transactions.

- **Interoperability**: Equito Bridge promotes seamless interoperability between different blockchain networks, fostering a more connected blockchain ecosystem.

### Use Cases

Equito Bridge can be applied to various use cases, including:

- **Asset Bridging**: Facilitating the transfer of assets between different blockchain networks.

- **Cross-Chain DeFi**: Enabling cross-chain decentralized finance (DeFi) transactions, lending, and yield farming.

- **Interconnected Applications**: Supporting the exchange of data and information between decentralized applications (dApps) on different blockchains.

## Validator Network

The Equito Bridge is an innovative protocol designed to enhance the security and efficiency of cross-chain transactions by leveraging Zero-Knowledge Proofs (ZKPs). In the world of blockchain interoperability, the verification of validator signatures can impose significant gas fees, making it impractical for frequent cross-chain transactions. Equito Bridge addresses this challenge by adopting an optimistic approach, wherein it verifies a single multi-signature transaction through Ed25519 signature verification using ZKPs. This innovative approach substantially reduces gas fees and enhances the scalability of cross-chain transactions.

### Problem Statement

When conducting transactions between different blockchain networks, it is essential to verify the signatures of validators. Validator signature verification typically incurs substantial gas fees, making it economically infeasible for frequent cross-chain transactions. Equito Bridge addresses this issue by adopting an optimistic approach, allowing it to verify only one multi-signature transaction instead of numerous individual validator signatures.

### Zero-Knowledge Proofs in Equito Bridge

Zero-Knowledge Proofs (ZKPs) play a pivotal role in securing the Equito Bridge protocol. ZKPs enable the verification of transactions on-chain without revealing sensitive information. In Equito Bridge, ZKPs are employed to validate multi-signature transactions off-chain, ensuring the integrity of the transaction data while preserving privacy.

### Security Measures

Security is paramount in Equito Bridge. The use of Ed25519 signatures and Zero-Knowledge Proofs ensures that transactions are not only efficient but also highly secure. Validators play a crucial role in maintaining the security of the bridge, and their signatures are protected against unauthorized access.

### Smart Contract Implementation

Equito Bridge implements smart contracts to enable cross-chain transactions. These contracts utilize Zero-Knowledge Proofs to validate multi-signature transactions. This on-chain verification process ensures that the transactions are executed securely and without the need for extensive signature validation.

### Validator Roles

Validators in the network are responsible for:

- Providing uptime to relay transactions
- Monitoring bridging events on the source chain.
- Transfer messages from source chain to destination chain.
- Approving, siging bridge transactions with multi-sig, and execute them.
- Detecting frad validators and actions and blocking them.
- Updating validators when new one is added.

### How does it work

An Equito Finance validator participates in verifying transactions and multi-signing them.

The transaction process in Equito Bridge is streamlined to maximize efficiency and minimize gas fees. All bridge transactions are approved and signed off-chain by validators using multi-sig. The primary feature of validator network is to use multi-sig that requires signatures from multiple validators to authorize transactions. Network consensus is reached when at least two-thirds of validators collectively sign the same transaction using their keys. Once signed, the multi-signature transaction is submitted to a smart contract on the respective chains. The smart contract uses ZKPs to verify the transaction on-chain, significantly reducing gas fees and enhancing scalability.

**Multi-Signature (Multi-Sig) Technology**
Multi-signature technology is a fundamental component of Equito Bridge's transaction process. It's used to enhance security and establish consensus among a network of validators before a transaction proceeds to the smart contract on the destination chain.

1. **Implementation**: Equito Bridge employs a network of validators, each of whom holds a cryptographic key. To initiate a cross-chain transaction, the sender's blockchain interacts with these validators. A predetermined quorum, typically two-thirds of the validators, must sign off on the transaction to achieve consensus.

2. **Consensus Establishment**: Validators review the transaction details and, if everything aligns with predefined criteria, they sign the transaction with their respective keys. This multi-signature requirement ensures that no single validator can unilaterally authorize a transaction. This enhances security by preventing rogue validators from compromising the network.

3. **Transaction Authorization**: Once the required number of validators have signed off on the transaction, it is considered authorized. This authorization is a critical checkpoint before the transaction proceeds further, assuring all involved parties of its legitimacy.

**Zero-Knowledge Proofs (ZKPs), Specifically zk-SNARKs**
Zero-knowledge proofs, particularly zk-SNARKs, are instrumental in Equito Bridge for achieving efficient and secure on-chain verification without revealing sensitive transaction details.

1. **Generation of zk-SNARKs**: When a multi-signature transaction is submitted to Equito Bridge's smart contract on the destination chain, the originating chain generates a zk-SNARK proof. This proof is derived from the complete transaction data, but it doesn't disclose the specifics.

2. **Efficient Verification**: Equito Bridge's smart contract is equipped with a zk-SNARK verification mechanism. Upon receiving a transaction along with its zk-SNARK proof, the smart contract can swiftly verify the proof without needing to access or reveal the underlying transaction data. This process is highly efficient and minimizes computational resources.

3. **Transaction Privacy**: The beauty of zk-SNARKs is that they preserve transaction privacy. Despite the smart contract verifying the transaction's authenticity, it does not gain access to transaction amounts, sender/receiver addresses, or other confidential details. This ensures that user privacy is maintained at a high level.

**Implementation within Equito Bridge**
The integration of these technologies is at the heart of Equito Bridge's functionality, ensuring secure, efficient, and privacy-preserving cross-chain transactions.

1. **Transaction Initiation**: When a user initiates a cross-chain transaction on Equito Bridge, it first goes through a multi-signature validation process involving the network of validators. This step establishes consensus and verifies the transaction's authenticity.

2. **Authorization**: Once the multi-signature requirement is met, the transaction is considered authorized and is then sent to the smart contract on the destination blockchain.

3. **Zero-Knowledge Proof Verification**: On the destination blockchain, the smart contract receives the transaction along with the accompanying zk-SNARK proof. The smart contract swiftly verifies the proof's authenticity, ensuring that the transaction adheres to all necessary criteria without exposing sensitive information.

4. **Gas Fee Reduction and Scalability**: The use of zk-SNARKs significantly reduces the gas fees associated with on-chain verification. Traditional on-chain verification processes can be resource-intensive and costly. However, zk-SNARKs streamline this process, resulting in substantial savings for users. Additionally, this efficiency contributes to the scalability of Equito Bridge, allowing it to handle a higher transaction volume without congestion.

5. **Privacy Enhancement**: By employing zk-SNARKs, Equito Bridge enhances user privacy. Transaction details remain confidential, preventing exposure of sensitive financial information to external observers.

![Validators](./images/validators.png)

### Validator Registration and Participation

Validators in the Equito Bridge network are registered automatically upon hosting, and all registered validators have the opportunity to actively participate in signing transactions. To ensure a dynamic and responsive network, new validators are periodically onboarded. New validator registrations are processed every 2 weeks.

## Cross-chain Messaging

Cross-chain messaging (CCM) is a crucial feature in the Equito Bridge ecosystem, allowing users to seamlessly send messages between different blockchain networks. This capability is particularly valuable for applications that require minimal logic or state synchronization across multiple chains, as well as for scenarios where unidirectional data transmission is sufficient.

![Equito Bridge Network](./images/cross-chain-message.png)

### Architecture of CCM

CCM operates through the deployment of specialized contracts on two or more interconnected blockchain networks. At the core of this communication mechanism lies the Equito Bridge, which serves as a reliable relayer responsible for transferring messages between these blockchains.

The process of sending a message via CCM involves several steps:

1. **Message Initiation**: To send a message from one blockchain (the source chain) to another (the destination chain), a user initiates the process by calling the `send()` function of the sender contract on the source chain.

2. **Message Relaying**: Equito Bridge intercepts and facilitates the transfer of the message from the source chain to the destination chain. This inter-chain transfer is executed securely and efficiently, ensuring that the message remains intact and confidential throughout the process.

3. **Message Reception**: Upon reaching the destination chain, the message is received by a designated CCM contract. The CCM contract processes the incoming message through its `onReceiveMessage()` function, which enables the execution of specific actions or interactions on the destination chain.

### Use Cases of CCM

Cross-chain messaging in Equito Bridge is particularly well-suited for a range of use cases, such as:

- **Contract Interaction**: Applications that require seamless interaction with contracts deployed on different chains can benefit from CCM. This includes calling contract functions or sending value to addresses on remote blockchains without the need for complex state synchronization.

- **One-Way Data Transfer**: CCM is ideal for scenarios where data only needs to be transmitted from one chain to another in a unidirectional manner. In these cases, the sender does not require feedback or results from the destination chain, streamlining the communication process.

### Security and Confidentiality

Equito Bridge places a strong emphasis on the security and confidentiality of all cross-chain messages. All message data is encrypted and secured, ensuring that sensitive information remains protected throughout the communication process. This commitment to data privacy and security is essential for maintaining user trust and safeguarding valuable assets.

### Decentralized Validation and Consensus

In Equito Bridge, a network of validators acts as decentralized observers responsible for reaching consensus on relevant external state and events across interconnected blockchains. These validators also have the capability to update external chain state through multi-signature signing, ensuring the integrity and accuracy of cross-chain transactions.

Equito Bridge's approach to decentralized validation and consensus is characterized by its trustless, permissionless, transparent, and efficient nature. By eliminating single points of failure and central authority, Equito Bridge provides a robust infrastructure for cross-chain messaging that users can rely on with confidence.

## Consensus

### Verifiable Random Function (VRF)

Equito Bridge employs a Verifiable Random Function (VRF) to select validators for transaction signing. This cryptographic mechanism takes into validator's EQT tokens when determining its probability of being selected. The more EQT tokens a validator holds, the higher its chances of being chosen. This method eliminates any advantage gained by creating multiple validators, promoting fairness and preventing centralization.

### Equito Bridge Consensus Protocol

The Equito Bridge consensus protocol leverages the VRF to establish a secure and efficient method for selecting validators to sign transactions. When a transaction is proposed to the validator network, a committee of validators is randomly selected. This committee's composition is based on the amount of EQT tokens held by each validator. Validators that have more EQT tokens will have a greater influence within the committee. Essentially, it's as if every EQT token participates in its own lottery, ensuring a decentralized and fair selection process. This approach maintains high network performance while allowing all validators in the network an opportunity to be involved.

### Transaction Verification Process

Validator network runs the VRF to determine validators that verify and sign transaction. The selected validators verify and sign the transaction using multi-sig. This signed transaction is then propagated throughout the validator network.

### Validator Rewards

In each transaction verification process, seven validators are selected to participate. As a reward for their contribution to the network's security and consensus, every validator involved in the verification process receives 10% of the transaction fees associated with that transaction. This incentivizes validators to actively participate in maintaining the Equito network's integrity and efficiency.

The Equito consensus mechanism, driven by the EQT token and VRF technology, ensures a fair and decentralized network where all stakeholders have a chance to contribute and be rewarded for their efforts. This innovative approach solidifies the Equito network's ability to finalize transactions efficiently while promoting transparency and fairness within the ecosystem.
