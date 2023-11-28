# System Requirements

## Hardware

The requirements for running a validator node scale with the as the number of jobs that your node services. CPUs with the x86 or AMD architecture is recommended for production environments, but you can use Apple M1 systems for development if you run the Validator node in Docker.

- Minimum for testing and basic development
  - 2 CPU cores
  - 4 GB of RAM
  - 120GB of harddisk.
- Recommended for nodes in a production environment
  - 4 CPU cores
  - 8GB of RAM
  - 120GB of harddisk.

If you run your PostgreSQL database locally, you will need additional hardware. To support more than 100 jobs, your database server will need at least 4 cores, 16 GB of RAM, and 100 GB of storage.

If you run your node on AWS or another cloud platform, use a VM instance type with dedicated core time. Burstable Performance Instances and VM instances with shared cores often have a limited number of CPU credits, which do not perform well for Validator nodes that require consistent performance.

## Software

- Validator nodes have the following software dependencies:
  - Operating System: Linux (Ubuntu, CentOS), MacOS
    - For production environments, Linux is recommended.
- Docker: Although it is possible to build Validator nodes from source, the best practice is to use the Validator Docker Images without -root.
- PostgreSQL versions from 11 to 15.

## Blockchain connectivity

Validator nodes require a fully-synced network client so that they can run on-chain transactions and interact with deployed contracts. For Ethereum, see the list of supported clients. Other L1s, L2s, and side-chains use different clients. See your network's documentation to learn how to run a client for your specific network.

The client must meet the following requirements:

- You can use a provider like Alchemy or Infura, but running your own client can provide lower latency and greater decentralization.
- Run your Validator nodes on their own separate VM or system. Hardware and storage requirements for these clients will change over time, so you will likely need to scale their capacity separately from the system where you run your Validator nodes.
- The client must provide both HTTP and WebSocket connections secured with SSL. Most providers give you https:// and wss:// connections by default.
