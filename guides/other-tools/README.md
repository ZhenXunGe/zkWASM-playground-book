# ZKWasm Playground `MongoDB` Tool Guide

[repo](https://github.com/ZhenXunGe/playground-mongodb-tool)

## Overview

The Playground `MongoDB` CLI tool provides maintenance and migration utilities for managing `MongoDB` and related data in the
ZKWasm Playground.

Commands:

- Auto Submit Batch Finalize Script: used to ensure batches are properly finalized during upgrades of the Auto Submit server
  (avoiding proofs of mixed versions).
- Migrate Rest Service Script: used to simplify packaging, backing up, and restoring rest service data (`MongoDB`, `RocksDB`,
  statics, and images).

See documentation [here](https://github.com/ZhenXunGe/playground-mongodb-tool/blob/main/README.md).

# ZKWasm Playground `RocksDB` Tool Guide

[repo](https://github.com/ZhenXunGe/playground-rocksdb-tool)

## Overview

The Playground `RocksDB` CLI tool is a developer utility designed to make it easier to inspect, debug, and maintain RocksDB
workspaces. It provides a set of CLI commands for specific database operations.

Commands:

- Check for a Particular Key: used to query a specific key within a given `RocksDB` column family.
- Count Records in a Column Family: provides a quick way to determine the number of records in a specific column family.
- Flush and Compact Databases: used to clean up and optimize `RocksDB` workspaces by flushing and compacting specific image
  databases.

See documentation [here](https://github.com/ZhenXunGe/playground-rocksdb-tool/blob/main/README.md).

# ZKWasm Playground Workflow CLI Reproduce Guide

[repo](https://github.com/ZhenXunGe/playground-workflow-cli-reproduce)

## Overview

The Playground Workflow Reproduce CLI offers scripts for reproducing issues within the zkWasm continuation-batcher environment.
This environment is the same as the core ZKWasm prover's development setup. To verify that a problem observed in ZKP originates
from ZKWasm itself, you need to reproduce the issue here and provide a concrete example.

See documentation [here](https://github.com/ZhenXunGe/playground-workflow-cli-reproduce/blob/main/README.md).

# ZKWasm Playground Backup Service Guide

[repo](https://github.com/ZhenXunGe/playground-backup-service)

## Overview

The ZKWASM Prover DB Docker Upload service allows you to upload a copy of a ZKWASM Prover database as a Docker image to Docker
Hub.

See documentation [here](https://github.com/ZhenXunGe/playground-backup-service/blob/main/README.md).
