# Running a Validator Node

This guide will teach you how to run a Validator node locally using Docker. The Validator node will be configured to connect to the Ethereum Sepolia or Goerli testnet.

# Requirements

- As explained in the requirements page, make sure there are enough resources to run a Validator node and a PostgreSQL database.
- Install Docker Desktop. You will run the Validator node and PostgreSQL in Docker containers.
- Validator nodes must be able to connect to an Ethereum client with an active websocket connection. See Running an Ethereum Client for details. In this tutorial, you can use an external service as your client.

# Using Docker

## Run PostgreSQL

1. Run PostgreSQL in a Docker container. You can replace mysecretpassword with your own password.

```bash
docker run --name eqt-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
```

2. Confirm that the container is running. Note the 5432 port is published 0.0.0.0:5432->5432/tcp and therefore accessible outside of Docker.

```bash
docker ps -a -f name=eqt-postgres
```

If the container is running successfully, the output shows a healthy status:

```bash
CONTAINER ID   IMAGE      COMMAND                  CREATED         STATUS         PORTS                    NAMES
dc08cfad2a16   postgres   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:5432->5432/tcp   eqt-postgres
```

## Run Validator node

### Configuring node

The following services offer Ethereum clients with websockets connectivity known to work with the Validator node.
<br />
[PureStake](https://developer.purestake.io/)
<br />
[Alchemy](https://www.alchemy.com/)
<br />
[Infura](https://www.infura.io/)
<br />
[QuickNode](https://www.quiknode.io/)

These are the only environment variables that are required for a Validator node to run.
Configure the necessary environment variables in the .env file by obtaining API keys from relevant external services.
We recommend you to use premium API key for optimal performance and high quality.

```bash
ALGOD_API_KEY=3HlRUk5h3G3UZeOWq3DN42boBkQ7yGI679WerzQN
INFURA_API_KEY=cb876f7f7ed64fb98108a51fac39f934
ALCHEMY_API_KEY=cpW9bVq33Ac3lBiI2pwc269AKbGvl9MF
QUICKNODE_RPC_URL=https://spring-summer-crater.bsc.discover.quiknode.pro/b3879f82a5ba1cf011021703133fddfde26a59a2
```
