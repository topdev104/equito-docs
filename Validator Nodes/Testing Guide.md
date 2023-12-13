# Testing Guide

This guide will teach you how to run a Validator node locally using Docker. The Validator node will be configured to connect to the Goerli testnet.

# Requirements

## Install docker

Update your existing list of packages.

```sh
sudo apt update
```

Install a few prerequisite packages which let apt use packages over HTTPS.

```sh
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

Then add the GPG key for the official Docker repository to your system.

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker repository to APT sources.

```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

Install Docker.

```sh
sudo apt install -y docker-ce
```

Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running.

```sh
sudo systemctl status docker
```

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

Create a local directory to hold the Equito Protocol data

```sh
mkdir ~/.equito-node
```

Run the following command to create .env file and set environment variables.

```sh
echo "
TEST1=This is test01
TEST2=This is test02
" > ~/.equito-node/.env
```

You can confirm that the variables are set correctly in .env file.

```sh
cat ~/.equito-node/.env
```

Start the Equito Node by running the Docker image.

```sh
cd ~/.equito-node
docker run --env-file ~/.equito-node/.env --platform linux/x86_64/v8 -it -p 7890:7890 robindev912/equito-validator-node
```

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
