# ZKWasm Service CLI Guide

[Repo](https://github.com/DelphinusLab/zkWasm-service-cli)

## Overview

The Service Helper CLI is a Node.js command-line interface designed to interact with the ZKWasm Playground (ZKP) platform. It
allows users to manage WASM images, submit proving tasks, handle payments, query tasks and users, and manage task statuses.

This CLI is primarily intended for developers interacting with the ZKP for managing proofs, tasks, and node statistics
efficiently. Additionally, it provides examples of creating platform functions and serves as a foundation for automating tests and
scripts.

Key Features:

- Image Management: Add new images (addimage) or reset existing ones (resetimage) with optional metadata and submission settings.
- Proving Tasks: Create proving tasks (addprovingtask) with manual or auto submit modes.
- Payments: Add credits to account (addpayment).
- Node Statistics: Generate and compare prover profiles (prover-profile) to monitor node performance.
- Queries: Retrieve detailed information about tasks (querytask), images (queryimage), or users (queryuser).
- Task Control: Manage task states including forcing unprovable or dry-run failed tasks to retry (forceunprovabletoreprocess,
  forcedryrunfailstoreprocess).
- External Data: Fetch task-specific external host tables (gettaskexternalhosttable).

## Usage

Install dependencies:

```bash
npm install
```

View the available usage via "help" argument:

```bash
node dist/index.js --help
```

Refer to the [README.md](https://github.com/DelphinusLab/zkWasm-service-cli/blob/main/README.md) for more documentation.

## Testing

Update all of the variables in the `tests/config.json` with your details.

`tests/config.json`:

```json
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

Example `tests/config.json`:

```json
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

### Understanding Usage

The best way to understand the usage of the CLI is to view the `scripts` directory which contains examples for common use cases.

```text
scripts/
|__ add_auto_proof_task.sh
|__ add_image.sh
|__ add_manual_proof_task.sh
|__ add_payment.sh
|__ add_payment_with_tx.sh
|__ force_dryrun_fails_to_reprocess.sh
|__ force_unprovable_to_reprocess.sh
|__ generate_current_node_stats.sh
|__ generate_prover_profile_report.sh
|__ get_task_external_host_table.sh
|__ pressure_test
    |__ add_multiple_auto_submit_task.sh
    |__ README.md
|__ query_image.sh
|__ query_prove_done_task.sh
|__ query_task.sh
|__ query_user.sh
|__ reset_image.sh
```

### Power User Usage

The CLI truly shines when you want to automate setup, reset, and prove tasks.

The best example of this can be found in E2E repo
[`TEST-BRANCH-PRODUCTION-IMAGES`](https://github.com/ZhenXunGe/playground-e2e-tests/tree/TEST-BRANCH-PRODUCTION-IMAGES) branch.

This [folder](https://github.com/ZhenXunGe/playground-e2e-tests/tree/TEST-BRANCH-PRODUCTION-IMAGES/scripts/cli/scripts) contains
scripts of automating tasks and highlights it's flexibility. Understanding these scripts will help a great deal in helping with
your usage of the CLI.

For more documentation please this
[README](https://github.com/ZhenXunGe/playground-e2e-tests/blob/TEST-BRANCH-PRODUCTION-IMAGES/README.md#running-zkwasm-service-cli-tests).
