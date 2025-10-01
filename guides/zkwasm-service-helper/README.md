# ZKWasm Service Helper Guide

[Repo](https://github.com/DelphinusLab/zkWasm-service-helper/)

## Overview

The Service Helper is a TypeScript library designed to facilitate communication with the ZKWasm service backend. It provides a
`ZkWasmServiceHelper` class that exposes APIs for managing WASM images, adding proving tasks, and querying tasks or images. The
library also includes example scripts and testing utilities to help developers interact with the service and automate workflows.

Key Features

- API Access: Methods for querying images, loading tasks, adding new WASM images, and submitting proving tasks.

- Task Management: Supports both manual and auto submit proofs.

- Testing Utilities: Includes scripts to test utility functions, query APIs, task APIs, and archive server interactions.

- Examples: Ready-to-run examples for adding images, submitting proofs, verifying tasks, and performing queries.

- Configurable: Example scripts can be customized using environment variables for server URL, private keys, chain IDs, task IDs,
  and proof submission modes.

## Usage

Install in your `package.json` by adding the following dependency and running `npm install`:

```json
{
  ...
  "dependencies": {
    ...
    "zkwasm-service-helper": "git+https://github.com/DelphinusLab/zkWasm-service-helper.git"
  },
  ...
}
```

## Testing

### 1. Install dependencies

```bash
npm install
```

### 2. Update Configs

Update all of the variables in the `tests/config.json` file with your values.

`tests/config.json`:

```json
{
    "details": {
        "server_url": "$REPLACE_WITH_REST_SERVER_PORT",
        "private_key": "$REPLACE_WITH_YOUR_METAMASK_NODE_PRIVATE_KEY",
        "chain_id": $REPLACE_WITH_TEST_NET_CHAIN_ID_NUMBER,
        "pedantic_checks": false
    },
    "verify": {
        "provider_url": "$REPLACE_WITH_TEST_NET_RPC_URL",
        "manual_task_id_to_verify": "$REPLACE_WITH_YOUR_MANUAL_TASK_ID_TO_VERIFY"
    },
    "query": {
        "task_id": "$REPLACE_WITH_YOUR_TASK_ID_TO_QUERY",
        "md5": "$REPLACE_WITH_YOUR_MD5_TO_QUERY",
        "node_address": "$REPLACE_WITH_YOUR_NODE_ADDRESS_TO_QUERY"
    },
    "auto_submit": {
        "round1_id": "$REPLACE_WITH_YOUR_ROUND1_ID_TO_QUERY",
        "round2_id": "$REPLACE_WITH_YOUR_ROUND2_ID_TO_QUERY",
        "task_id_in_auto_submit_batch": "$REPLACE_WITH_YOUR_TASK_ID_IN_AUTO_SUBMIT_BATCH_TO_QUERY"
    },
    "archive": {
        "server_url": "$REPLACE_WITH_YOUR_ARCHIVE_SERVER_URL",
        "id": "$REPLACE_WITH_YOUR_ARCHIVE_ID_TO_QUERY",
        "archived_task_id": "$REPLACE_WITH_YOUR_ARCHIVED_TASK_ID_TO_QUERY",
        "archive_volume_name": "$REPLACE_WITH_YOUR_ARCHIVE_VOLUME_NAME_TO_QUERY",
        "archive_auto_submit_volume_name": "$REPLACE_WITH_YOUR_ARCHIVE_AUTO_SUBMIT_VOLUME_NAME_TO_QUERY"
    },
    "tasks": {
        "image": "./tests/data/image.wasm"
    }
}
```

Example of `tests/config.json`:

```json
{
  "details": {
    "server_url": "http://138.217.142.94:8108",
    "private_key": "0x...",
    "chain_id": 97,
    "pedantic_checks": false
  },
  "verify": {
    "provider_url": "https://data-seed-prebsc-1-s3.binance.org:8545",
    "manual_task_id_to_verify": "68709dcc0a7b4ac8c109b12a"
  },
  "query": {
    "task_id": "68ae8cbfdf33b6098975c518",
    "md5": "D2144252F3C9DDCA5CA86C23D2EE97E9",
    "node_addresses": [
      "0x3552f5e0bfccf79a87a304e80455b368af9b56f6",
      "0x30aa366E578F80dD7C20EB5f4F68B80A514fb188"
    ]
  },
  "auto_submit": {
    "round1_id": "689181253fef6b4931d611fa",
    "round2_id": "689181a43fef6b4931d611fb",
    "task_id_in_auto_submit_batch": "689167093fef6b4931d611c8"
  },
  "archive": {
    "server_url": "http://138.217.142.94:8108",
    "id": "68709dcc0a7b4ac8c109b12a",
    "archived_task_id": "68709dcc0a7b4ac8c109b12a",
    "archive_volume_name": "vol_1",
    "archive_auto_submit_volume_name": "auto_submit_vol_1"
  },
  "tasks": {
    "image": "./tests/data/image.wasm"
  }
}
```

### 3. Run all test scripts

Run query related tests:

```bash
npm run test queries
```

Run task sequential tests:

```bash
npm run test tasks
```

## Tips

### Rust Example

This [repo](https://github.com/qozymandias/zkp-service-helper) provides the same provides utilities and interface for interacting
with the ZKWasm service backend, similar to the TypeScript library.

This crate demonstrates how to implement platform functions in Rust and can be used for scripting and testing workflows with the
ZKWasm service.

```bash
git clone https://github.com/qozymandias/zkp-service-helper

cd zkp-service-helper
```

Example testing config `test.json`:

```json
{
    "details": {
        "server_url": "http://138.217.142.94:8108",
        "private_key": "0x...
        "chain_id": 97,
        "pedantic_checks": false
    },
    "verify": {
        "provider_url": "https://data-seed-prebsc-1-s3.binance.org:8545",
        "manual_task_id_to_verify": "68709dcc0a7b4ac8c109b12a"
    },
    "query": {
        "task_id": "68ae8cbfdf33b6098975c518",
        "md5": "D2144252F3C9DDCA5CA86C23D2EE97E9",
        "node_addresses": [
            "0x3552f5e0bfccf79a87a304e80455b368af9b56f6",
            "0x30aa366E578F80dD7C20EB5f4F68B80A514fb188"
        ]
    },
    "auto_submit": {
        "round1_id": "689181253fef6b4931d611fa",
        "round2_id": "689181a43fef6b4931d611fb",
        "task_id_in_auto_submit_batch": "689167093fef6b4931d611c8"
    },
    "archive": {
        "server_url": "http://138.217.142.94:8108",
        "id": "68709dcc0a7b4ac8c109b12a",
        "archived_task_id": "68709dcc0a7b4ac8c109b12a",
        "archive_volume_name": "vol_1",
        "archive_auto_submit_volume_name": "auto_submit_vol_1"
    },
    "tasks": {
        "image": "./tests/data/image.wasm"
    }
}
```

Run query tests:

```bash
cargo test tests::queries
```

Run task (POST requests) tests:

```bash
cargo test tests::tasks
```
