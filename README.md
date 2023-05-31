# JeTson's unofficial LUKSO Docker containers

This repo provides Docker images to run different kinds of LUKSO node (validator and non validator nodes).

Note: it has been tested on Ubuntu 22.04.

LUKSO network configs are fetched from: [lukso-network/network-configs](https://github.com/lukso-network/network-configs).

It is provided "as is" and you are encouraged to adjust the configuration files for your own needs. The most important configuration files are the genesis files:

- `genesis.ssz`
- `genesis.json`

They can be found in our [`lukso-network/network-configs`](https://github.com/lukso-network/network-configs) repo.

For more information, check the [LUKSO Docs](https://docs.lukso.tech/networks/mainnet/running-a-node/).

## How to use

1. Log into your node.
2. Install [Docker](https://docs.docker.com/engine/install/ubuntu/).
3. Install [Docker Compose](https://docs.docker.com/compose/install/linux/)

3. Clone the repo.

```sh
git clone https://github.com/JEnric/Docker-Lukso-Nodes.git
```

4. Check if the config files from [`lukso-network/network-configs`](https://github.com/lukso-network/network-configs) are up to date.

5. **IMPORTANT:** Edit the `.env` file and adjust the values in `.env` file (node name, fee recipient address, etc.).

6. Copy your `keystore-xxx.json` files in the [`./keystores/`](./keystores) folder.

7. Write your keystore password in a temporary txt file:

```sh
echo "yourPassword" > /tmp/secrets/password.txt
```

NOTE 1: This password will also be used for the validator wallet.

NOTE 2: You can set your keystore password differently by changing the configuration in the `docker-compose.yml` file for the `prysm_validator_import` service.

8. Start the services:

```sh
docker compose up

# To run in the background, use detached mode with -d flag
```

### Useful commands

Check the status of the containers:

```sh
docker ps
```
or
```sh
docker stats
```

Check the logs to make sure everything is running fine:

```sh
docker compose logs -f prysm_beacon

# You can see the logs of each service:
# docker compose logs -f prysm_validator
# ...
```

## Monitoring

Grafana will be available on port 3000

### Execution stats

To add your node on the [execution stats page](https://stats.execution.mainnet.lukso.network/), fill out [this form](https://docs.google.com/forms/d/e/1FAIpQLSf6_vflZkaRh8dgHMiFtZI5g3DrBFKP4Sc2l2DBW95OWRFO9g/viewform) to receive the secret.

You will then need to update these values in the [`.env`](./.env) file:

```
NODE_NAME=myNodeName
ETH_STATS_SECRET=xxx
```

## Images

This repo is using the following docker images:

- Geth: [ethereum/client-go](https://hub.docker.com/r/ethereum/client-go)
- Erigon: [thorax/erigon](https://hub.docker.com/r/thorax/erigon)
- Prysm: [prysmaticlabs/prysm-beacon-chain](https://hub.docker.com/r/prysmaticlabs/prysm-beacon-chain)
- Prysm validator: [prysmaticlabs/prysm-validator](https://hub.docker.com/r/prysmaticlabs/prysm-validator)
- [macht/eth2stats-client](https://hub.docker.com/r/macht/eth2stats-client)

## Resources

- [LUKSO Docs](https://docs.lukso.network)
- [Genesis Validators, start your clients!](https://medium.com/lukso/genesis-validators-start-your-clients-fe01db8f3fba)
- [GitHub repo: lukso-network/network-configs](https://github.com/lukso-network/network-configs)
- [Deposit launchpad](https://deposit.mainnet.lukso.network/)