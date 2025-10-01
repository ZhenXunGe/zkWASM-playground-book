# Prover Node Docker Guide

[repo](https://github.com/DelphinusLab/prover-node-docker)

## Overview

The Prover Node Docker is a containerized environment for running the prover node, which performs proving tasks from the ZKWasm
Playground server.

## Quick Start

### 1. Update Configs

#### Docker Compose

The following are the key variables that must be updated in the docker compose config:

- Device ids must be set to a GPU that is not is use, check using `nvidia-smi`.
- (Optional) Volume should be given a unique name.

`docker-compose.yml`:

```yaml
services:
  prover-node:
  ...
          devices:
          ...
              device_ids: ["2"]
    ...
    volumes:
    ...
      - $YOUR_NAMED_PROVER_LOGS_VOLUME:/home/zkwasm/prover-node-release/logs/prover
 ...
 volumes:
  $YOUR_NAMED_PROVER_LOGS_VOLUME:
```

#### Prover Config

Only the Rest server URL and your private key need to be updated in the prover config.

`prover_config.json`:

```json
{
  "server_url": "http://localhost:$REPLACE_WITH_REST_SERVER_PORT",
  "priv_key": "$REPLACE_WITH_YOUR_METAMASK_NODE_PRIVATE_KEY",
  ...
}
```

#### Prover System Config

Only the Rest server URL needs to be updated in the prover system config.

`prover_system_config.json`:

```json
{
  "server_url": "http://localhost:$REPLACE_WITH_REST_SERVER_PORT",
  ...
}
```

### 2. Run with Scripts

```bash
sudo bash scripts/start.sh
```

## Tips

### Upgrading Prover Image

Whenever there is a change to docker image on [docker hub](https://hub.docker.com/u/zkwasm) you must upgrade the local version.

```bash
git stash && git pull && git stash pop

sudo bash scripts/stop.sh && sudo bash scripts/upgrade.sh
```

### Cleaning Old Images

You may need to delete old images to free up space or to ensure only the correct image is on the machine. This can be done with
the

```bash
docker rmi $(docker images -q) --force
```

### Accessing Logs

You should always update the config with a unique log volume so it can easily be distinguished on the dev machine.

Logs are stored in the following folder:

```bash
/var/lib/docker/volumes/prover-node-docker_$YOUR_NAMED_PROVER_LOGS_VOLUME
```

Example:

```bash
sudo vi /var/lib/docker/volumes/prover-node-docker_oscar-prover-logs-volume/_data/prover_2025-09-15-07-43-03.log
```
