# Testing Guide

This guide will teach you how to run a Validator node locally using Docker. The Validator node will be configured to connect to the Goerli testnet.

# Requirements

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

# Using Docker

## Run PostgreSQL

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

## Run Validator node

1. Create a local directory to hold the Equito Protocol data

```sh
mkdir ~/.equito-node
```

2. Run the following command to create .env file and set environment variables.

```sh
echo "
PORT=3000
NODE_ENV=production
" > ~/.equito-node/.env
```

You can confirm that the variables are set correctly in .env file.

```sh
cat ~/.equito-node/.env
```

3. Start the Equito Node by running the Docker image.

```sh
cd ~/.equito-node && docker run --env-file ~/.equito-node/.env -d --platform linux/x86_64/v8 --name equito-bridge -it -p 7890:7890 robindev912/equito-validator-node
```

4. Confirm that the container is running. Note the 7890 port is published 0.0.0.0:7890->7890/tcp and therefore accessible outside of Docker.

```sh
docker ps -a -f name=equito-bridge
```

If the container is running successfully, the output shows a healthy status:

```
CONTAINER ID   IMAGE                               COMMAND                  CREATED         STATUS         PORTS                                       NAMES
63318f25608e   robindev912/equito-validator-node   "/sbin/tini -- npm s…"   7 minutes ago   Up 7 minutes   0.0.0.0:7890->7890/tcp, :::7890->7890/tcp   equito-bridge
```
