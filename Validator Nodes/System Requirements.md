# System Requirements

## Hardware

The requirements for running a validator node scale with the as the number of jobs that your node services. CPUs with the x86 architecture is recommended for production environments, but you can use Apple M1 systems for development if you run the Validator node in Docker.

- Minimum: At least 2 CPU cores and 4 GB of RAM will allow you to get a node running for testing and basic development.
- Recommended: For nodes in a production environment with over 100 jobs, you will need at least 4 CPU cores and 8GB of RAM.

If you run your PostgreSQL database locally, you will need additional hardware. To support more than 100 jobs, your database server will need at least 4 cores, 16 GB of RAM, and 100 GB of storage.

If you run your node on AWS or another cloud platform, use a VM instance type with dedicated core time. Burstable Performance Instances and VM instances with shared cores often have a limited number of CPU credits, which do not perform well for Validator nodes that require consistent performance.

## Software

- Validator nodes have the following software dependencies:
  - Operating System: Linux, MacOS, or the WSL (Windows Subsystem for Linux)
    - For production environments, Linux is recommended.
- Docker: Although it is possible to build Validator nodes from source, the best practice is to use the Validator Docker Images without -root.
- PostgreSQL versions >=11 <16 (Version 11 through 15. Not version 16 or later).
  - If you use a database as a service, your database host must provide access to logs.
  - If you run the database on a separate system, secure the TCP/IP connection with SSL.

## Blockchain connectivity

Validator nodes require a fully-synced network client so that they can run on-chain transactions and interact with deployed contracts. For Ethereum, see the list of supported clients. Other L1s, L2s, and side-chains use different clients. See your network's documentation to learn how to run a client for your specific network.

The client must meet the following requirements:

- You can use a provider like Alchemy or Infura, but running your own client can provide lower latency and greater decentralization.
- Run your Validator nodes on their own separate VM or system. Hardware and storage requirements for these clients will change over time, so you will likely need to scale their capacity separately from the system where you run your Validator nodes.
- The client must provide both HTTP and WebSocket connections secured with SSL. Most providers give you https:// and wss:// connections by default. If you run your own client, you must create a reverse proxy for your client using a web server like Nginx. The web server handles the SSL encryption and forwards the connection to your client.
