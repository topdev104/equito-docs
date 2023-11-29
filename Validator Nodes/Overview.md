# Validator Nodes

## Overview

Operating a validator node allows you to be part of the Equito Bridge Network, building cross-chain messaging. Learn more about validator nodes with our step-by-step tutorials and documentation.

## Blockchain API Providers

### What is Blockchain API Providers

Blockchain API providers are third-party services that offer application programming interfaces (APIs) to interact with blockchain networks, enabling integration of blockchain functionality into applications. Blockchain API providers act as intermediaries, abstracting the complexities of running and maintaining blockchain nodes, allowing developers to focus on building applications rather than managing the underlying infrastructure.

### How to use

Validator Nodes integrate blockchain APIs into their services by making HTTP requests to the provided endpoints, receiving responses with blockchain data.

- [Infura](https://www.infura.io/) is a widely used blockchain API provider that offers Ethereum API access. It allows developers to connect to the Ethereum network without the need to run a full node, providing scalable and reliable access to blockchain data.

- [Alchemy](https://www.alchemy.com/) is another prominent blockchain API provider focused on Ethereum. It offers a developer platform that includes APIs for Ethereum, allowing developers to build and scale decentralized applications (DApps) with features like real-time updates and analytics.

- [QuickNode](https://www.quiknode.io/) is a blockchain infrastructure-as-a-service provider that offers API access to multiple blockchain networks, including Ethereum, Binance Smart Chain, and others. It provides scalable and reliable access to blockchain nodes for developers.

Infura, Alchemy, and QuickNode often implement security measures such as rate limiting, authentication, and encryption to protect the integrity of their API services.
Validator Nodes use these API providers to decentralize getting blockchain information.

### Modules

Validator node has several modules of the following

- Verifiable Random Function Module: Enables the selection of validators through a Verifiable Random Function.

- Consensus Module: Manages the consensus process among validator nodes.

- Blockchain Data Retrieval Module: Retrieves blockchain data from designated blockchain API providers.

- Multi-signing and Transaction Execution Module: Enables multi-signing and execution of transactions by validators.

- Transaction Validation Check Module: Validates transactions to ensure their compliance with specified criteria.

- Verification Module: Verifies the integrity and authenticity of data within the validator nodes.

- Validators Update Module: Handles the process of updating information related to validators.
