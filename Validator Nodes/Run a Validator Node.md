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
docker run --name cl-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
```

2. Confirm that the container is running. Note the 5432 port is published 0.0.0.0:5432->5432/tcp and therefore accessible outside of Docker.

```bash
docker ps -a -f name=cl-postgres
```

If the container is running successfully, the output shows a healthy status:

```bash
CONTAINER ID   IMAGE      COMMAND                  CREATED         STATUS         PORTS                    NAMES
dc08cfad2a16   postgres   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:5432->5432/tcp   cl-postgres
```

## Run Validator node

### Configure your node
