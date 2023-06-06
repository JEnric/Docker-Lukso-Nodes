# JeTson's unofficial LUKSO Docker containers

This repo provides Docker images to run different kinds of LUKSO nodes (validator and non validator nodes).

Note: Containers have been tested on Ubuntu 22.04.

LUKSO network configs were fetched from the official repository: [lukso-network/network-configs](https://github.com/lukso-network/network-configs).

It is provided "as is" and you are encouraged to adjust the configuration files for your own needs. The most important configuration files are the genesis files:

- `genesis.ssz`
- `genesis.json`
- `config.yaml`

For more information, check the [LUKSO Docs](https://docs.lukso.tech/networks/mainnet/running-a-node/).

## How to use

1. Log into your node.
2. Install [Docker](https://docs.docker.com/engine/install/ubuntu/).
3. Install [Docker Compose](https://docs.docker.com/compose/install/linux/).

3. Clone the repo with the following:

```sh
git clone https://github.com/JEnric/Docker-Lukso-Nodes.git
```

4. Check if the config files in the config directory are equal to the same files found here: [`lukso-network/network-configs`](https://github.com/lukso-network/network-configs/tree/main/mainnet/shared).

5. **IMPORTANT:** Edit the `.env` file in the chosen client folder and adjust the values (NODE_NAME, FEE_RECIPIENT, EXTERNAL_IP/DOMAIN, and more if needed).

---If you want to run a validator proceed with 6. Otherwise go to step 8.---

6. Copy your `keystore-xxx.json` files in the `./<chosen client folder>/keystores/` folder.

7. Write your keystore password in a temporary txt file:

```sh
echo "yourPassword" > /tmp/secrets/password.txt
```

NOTE 1: This password will also be used for the validator wallet.

NOTE 2: You can set your keystore password differently by changing the configuration in the `docker-compose.yml` file for the `prysm_validator_import` service.

---End of validator part---

8. Start the services from the chosen client subfolder with the docker-compose.yml inside:

```sh
docker compose up
```
To run in the background, use detached mode with -d flag

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
```
You can see the logs of each service:

```
docker compose logs -f <container name>
```
Note: Check the exact container names in the docker-compose.yml you have started.

To stop the containers execute the following from the chosen client subfolder with the docker-compose.yml inside:
```sh
docker compose stop
```
[Docker compose reference:](https://docs.docker.com/compose/reference/)
```sh
docker compose up          Create and start containers
docker compose down        Stop and remove containers, networks
docker compose restart     Restart service containers
docker compose start       Start services
docker compose stop        Stop services
```
## Monitoring

Grafana will be available on port 3000

### Execution stats

To add your node on the [execution stats page](https://stats.execution.mainnet.lukso.network/), fill out [this form](https://docs.google.com/forms/d/e/1FAIpQLSf6_vflZkaRh8dgHMiFtZI5g3DrBFKP4Sc2l2DBW95OWRFO9g/viewform) to receive the secret.

You will then need to update these values in the `.env` file:

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
