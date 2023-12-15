# Testing Guide

This guide will teach you how to run a Validator node locally using Docker. The Validator node will be configured to connect to the Goerli testnet.

## Install docker

1. Update your existing list of packages.

```sh
sudo apt update
```

2. Install a few prerequisite packages which let apt use packages over HTTPS.

```sh
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

3. Add the GPG key for the official Docker repository to your system.

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker repository to APT sources.

```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

4. Install Docker.

```sh
sudo apt install -y docker-ce
```

Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running.

```sh
sudo systemctl status docker
```

## Using Docker

### Run PostgreSQL

There are three ways to connect PostgreSQL.

1. Connect to PostgreSQL docker.
2. Connect to local PostgreSQL.
3. Connect to remote PostgreSQL.

In order to connect to a remote database, you must obtain information about the database and the server. Note the following database details so you can use them to configure your Equito node later.

- Server hostname or IP
- Port
- Username
- Password
- Database name

The user must be the owner of the database.

This **DATABASE_URL** should be set in .env file of Equito Node.

```sh
DATABASE_URL=postgresql://[POSTGRES_USER]:[POSTGRES_PASSWORD]@[DB_HOST]:[DB_PORT]/[POSTGRES_DB]?sslmode=[SSL_MODE]
```

- [POSTGRES_USER]: The username for the database owner account.
- [POSTGRES_PASSWORD]: The password for the database owner account.
- [DB_HOST]: The server hostname or IP address of the database server.
- [DB_PORT]: The port that the database is listening on. The default port for PostgreSQL is 5432.
- [POSTGRES_DB]: The name of the database to use for the Equito node.
- [SSL_MODE]: If you are testing on a database that does not have SSL enabled, you can specify disable so that you don't need to go through the process of configuring SSL on your database. On a production node, set this value to require.

#### Connecting to PostgreSQL docker

1. Run PostgreSQL in a Docker container. You can replace mysecretpassword with your own password.

```sh
docker run --name eqt-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
```

2. Confirm that the container is running. Note the 5432 port is published 0.0.0.0:5432->5432/tcp and therefore accessible outside of Docker.

```sh
docker ps -a -f name=eqt-postgres
```

If the container is running successfully, the output shows a healthy status:

```sh
CONTAINER ID   IMAGE      COMMAND                  CREATED         STATUS         PORTS                    NAMES
dc08cfad2a16   postgres   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:5432->5432/tcp   eqt-postgres
```

This is an example of PostgreSQL setting.

```sh
DATABASE_URL=postgresql://postgres:postgres@host.docker.internal:5432/postgres?sslmode=disable
```

#### Connecting to local PostgreSQL

This is an example of PostgreSQL setting. It is the same with PostgreSQL docker's setting.

```sh
DATABASE_URL=postgresql://postgres:postgres@my.postgre.com:5432/equito_node?sslmode=disable
```

#### Connecting to remote PostgreSQL

This is an example of PostgreSQL setting.

```sh
DATABASE_URL=postgresql://postgres:mypassword@myserver.com:5432/equito_node?sslmode=prefer
```

### Run Validator node

1. Create a local directory to hold the Equito Protocol data

```sh
mkdir ~/.equito-node
```

2. Run the following command to create .env file and set environment variables. It includes setttings of wallet and API keys. The wallet should be include more than 100 ALGO, 1 Goerli ETH and 1 BNB.

These are the faucets to get test tokens.

[Algorand faucet](https://bank.testnet.algorand.network/)

[Goerli ETH faucet](https://goerlifaucet.com/)

[BNB faucet](https://testnet.binance.org/faucet-smart)

See how to get the API keys in [Configuring node](#configuring-node)

```sh
echo "
NODE_URL=<your-node-url>
PORT=7890
ALGO_WALLET_MNEMONIC=<algorand-wallet-mnemonic>
ETH_WALLET_PRIVATE_KEY=<ethereum-wallet-private-key>
BNB_WALLET_PRIVATE_KEY=<binance-wallet-private-key>
ETH_MAINNET_ENDPOINT=<your-mainnet-endpoint>
ETH_TESTNET_ENDPOINT=<your-testnet-endpoint>
BNB_MAINNET_ENDPOINT=<your-mainnet-endpoint>
BNB_TESTNET_ENDPOINT=<your-testnet-endpoint>
" > ~/.equito-node/.env
```

This is an example of .env setting.

```sh
echo "
NODE_URL=https://node.mycompany.com
PORT=7890
DATABASE_URL=postgresql://postgres:postgres@host.docker.internal:5432/postgres?sslmode=disable
ALGO_WALLET_MNEMONIC=gift only mouse goddess city benefit obtain evoke excite predict safe neither purpose route sock unfold boil pass battle agent body what abandon finish anchor
ETH_WALLET_PRIVATE_KEY=756b7f2f95346df4767041da97be8f8c6cbd3cab9de46ef31c85b4af1c507c5a
BNB_WALLET_PRIVATE_KEY=40325b340a0755405f6e13c297511a793c29db6b91ed2f9d6999d5624caccf3c
ETH_ENDPOINT=https://goerli.infura.io/v3/cb206f7f7ed64fb98108a56fac39f934
BNB_ENDPOINT=https://dark-wandering-tree.bsc-testnet.quiknode.pro/58aaf9b78f359d477e060faf24bb51c4c2d2389c/
" > ~/.equito-node/.env
```

These are the examples of endpoints.

**Infura** (Ethereum Mainnet & Testnet)

```sh
https://mainnet.infura.io/v3/cb206f7f7ed64fb98108a56fac39f934
https://goerli.infura.io/v3/cb206f7f7ed64fb98108a56fac39f934
```

**Alchemy** (Ethereum Mainnet & Testnet)

```sh
https://eth-mainnet.g.alchemy.com/v2/cpW9bVq33Ac6lBjI2pwc266AKbGvl9MF
https://eth-goerli.g.alchemy.com/v2/ldhqIo8W9kfM6jHV31W4Xuvk2O2PMYP8
```

**QuickNode** (Binance Mainnet & Testnet)

```sh
https://spring-summer-crater.bsc.quiknode.pro/b3119f82a5ba1cf011021703136fddfde26a69a2/
https://dark-wandering-tree.bsc-testnet.quiknode.pro/58aaf9b78f359d477e060faf24bb51c4c2d2389c/
```

You can confirm that the variables are set correctly in .env file.

```sh
cat ~/.equito-node/.env
```

3. Start the Equito Node by running the Docker image.

```sh
cd ~/.equito-node && docker run --env-file ~/.equito-node/.env -d --platform linux/x86_64/v8 --name equito-node -it -p 7890:7890 --add-host=host.docker.internal:host-gateway robindev912/equito-validator-node
```

4. Confirm that the container is running. Note the 7890 port is published 0.0.0.0:7890->7890/tcp and therefore accessible outside of Docker.

```sh
docker ps -a -f name=equito-node
```

If the container is running successfully, the output shows a healthy status:

```
CONTAINER ID   IMAGE                               COMMAND                  CREATED         STATUS         PORTS                                       NAMES
63318f25608e   robindev912/equito-validator-node   "/sbin/tini -- npm s…"   7 minutes ago   Up 7 minutes   0.0.0.0:7890->7890/tcp, :::7890->7890/tcp   equito-node
```

## Configuring node

### Blockchain API endpoints

The following services offer Ethereum and Binance API endpoints to work with the Validator node.
It is necessary to get API endpoints and set them in .env file.

#### Alchemy

Visit [Alchemy](https://www.alchemy.com/) and create API endpoints.

![Alchemy](./alchemy.png)

![Alchemy Endpoint](./alchemy-endpoint.png)

#### Infura

Visit [Infura](https://www.infura.io/) and create API endpoints.

![Infura](./infura.png)

![Infura Endpoint](./infura-endpoint.png)

#### QuickNode

Visit [QuickNode](https://www.quicknode.com/) and create API endpoints.

![QuickNode](./quicknode-endpoint.png)

![QuickNode Endpoint](./quicknode-endpoint.png)

These are the only environment variables that are required for a Validator node to run.
Configure the necessary environment variables in the .env file by obtaining API endpoints from relevant external services.
We recommend you to use premium API endpoints for optimal performance and high quality.

### Other Configuration

1. Connect your domain to your hosting. It needs to use SSL for the Domain URL.

2. Ensure that port 7890 is open for communication with the Equito Node APIs.
   Redirect your Node URL to this 7890 port using Nginx.

3. Check all env variables are set correctly.

```
~/.equito-node docker ps -a
CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS          PORTS                    NAMES
c4a9a8a83a6d   equito-validator-node   "docker-entrypoint.s…"   13 seconds ago   Up 13 seconds   0.0.0.0:7890->7890/tcp   gifted_lovelace
d039fc4c24d7   postgres                "docker-entrypoint.s…"   22 seconds ago   Up 21 seconds   0.0.0.0:5432->5432/tcp   eqt-postgres
```

```
Application has started on 7890
--- dev --- Ethereum block number: 10216462
--- dev --- Binace block number: 35978290
--- dev --- ALGO balance: 2005.337593
--- dev --- ETH balance: 5.941181891029034559
--- dev --- BNB balance: 5.799567389
--- dev --- Success to set all keys.
--- dev --- UUID: 878f0cb5-9f08-40e2-a8c0-f7e87a99ebe8
```

If all containers are running and you get logs of success, the node is working.
