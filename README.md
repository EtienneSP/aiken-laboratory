# aiken-laboratory

Playground project to experiment with Aiken and Cardano smart contracts

## Local Node Setup (optional)

The following instructions are optional and can be used to start a Cardano node locally using Docker Desktop.  
One simple alternative to running your own node is to use and existing API such as Blockfrost.  
The following procedure was only tested on Windows.  
Run the following commands from the local folder (`aiken-laboratory/local`).

### 1. Requirements

- Docker Desktop

### 2. Start Dependencies

The dependencies docker-compose will create the shared docker network used by the other containers and start the Prometheus and Gradana containers, used to monitor the Cardano nodes.

```shell
docker compose -f ./docker-compose.dependencies.yml up -d
```

### 3. Start the Cardano node

Run either the mainnet or testnet docker-compose, based on the environment you want to use.

```shell
docker compose -f ./docker-compose.testnet.yml up -d
```

Monitor the container logs to validate that the node started correctly.  
Once the node is 100% sync, you will be able to interact directly with it using the cardano-cli

```shell
docker exec -it cardano-node cardano-cli query tip --testnet-magic 2
```

### 4. Interact with the cardano node from another container

This is a simple separated container that runs one cardano-cli commands, as a demo, to demonstrate the interaction with the Cardano node from an other container.

```shell
docker compose -f ./docker-compose.testnet-client.yml up -d
```

### 5. Shutdown local setup

```shell
docker compose -f ./docker-compose.testnet-client.yml down
docker compose -f ./docker-compose.testnet.yml down
docker compose -f ./docker-compose.dependencies.yml down
```
