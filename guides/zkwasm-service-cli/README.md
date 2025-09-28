# ZKWasm Service CLI

[Repo](https://github.com/DelphinusLab/zkWasm-service-cli)

## Overview

The Service Helper CLI is a Node.js command-line interface designed to interact with the ZKWasm Playground (ZKP) platform.
It allows users to manage WASM images, submit proving tasks, handle payments, query tasks and users, and manage task statuses.

This CLI is primarily intended for developers interacting with the ZKP for managing proofs, tasks, and node statistics efficiently.
Additionally, it provides examples of creating platform functions and serves as a foundation for automating tests and scripts.

Key Features:
- Image Management: Add new images (addimage) or reset existing ones (resetimage) with optional metadata and submission settings.
- Proving Tasks: Create proving tasks (addprovingtask) with manual or auto submit modes.
- Payments: Add credits to account (addpayment).
- Node Statistics: Generate and compare prover profiles (prover-profile) to monitor node performance.
- Queries: Retrieve detailed information about tasks (querytask), images (queryimage), or users (queryuser).
- Task Control: Manage task states including forcing unprovable or dry-run failed tasks to retry (forceunprovabletoreprocess, forcedryrunfailstoreprocess).
- External Data: Fetch task-specific external host tables (gettaskexternalhosttable).

## Usage

Install dependencies:
```bash
npm install
```

View the available usage via "help" argument:
```
node dist/index.js --help
```

Refer to the [README.md](https://github.com/DelphinusLab/zkWasm-service-cli/blob/main/README.md) for more documentation.

## Testing

Update `test/config.json` with your details

```
{
    "details": {
        "server_url": "REPLACE_WITH_REST_SERVER_URL",
        "private_key": "REPLACE_WITH_YOUR_METAMASK_NODE_PRIVATE_KEY",
        "chain_ids": "REPLACE_WITH_TEST_NET_CHAIN_ID_NUMBER"
    },
    "query": {
        "task_id": "REPLACE_WITH_TASK_ID_TO_QUERY",
        "md5": "REPLACE_WITH_MD5_TO_QUERY"
    }
}
```

Example:

```
{
    "details": {
        "server_url": "http://138.217.142.94:8108",
        "private_key": "0x...",
        "chain_ids": "97"
    },
    "query": {
        "task_id": "68709dcc0a7b4ac8c109b12a",
        "md5": "F4A9101BD7C033F3E57EFB0F9F68C4D8",
    }
}

```

## Tips

TODO
