# ZKWASM Playground End-to-End Tests

[Repo](https://github.com/ZhenXunGe/playground-e2e-tests)

## Overview

This repository contains comprehensive end-to-end (E2E) tests for the ZKWASM Playground, setup images, proof generation,
auto-submit tasks, verification, user charges, subscriptions, and failure scenarios.

The E2E testing framework is a customizable solution for testing majority of the features of ZKWasm Playground (ZKP).

This suite ensures robustness of ZKP workflows, verifying normal operation, failure handling, and edge-case behavior,
while serving as a reference for writing new tests and scripts for custom scenarios.

For complete documentation please see repo's [README](https://github.com/ZhenXunGe/playground-e2e-tests/blob/main/README.md)

Key Features

- Test Coverage:

  - Setup and reset images (simple, DB-related, context-specific)
  - Proof tasks for various images, including edge-case and buggy images
  - Auto-submit proof functionality
  - Proof verification
  - User charge and subscription workflows
  - Failure tests for setup, reset, and proof tasks, including dry run failures

- WASM Files: Multiple WASM files provided for different test cases (e.g., equality.wasm, context.wasm, merkledb.wasm, write_benchmark.wasm)

- Custom Scripts: Scripts for smoke tests, failure tests, Merkle DB verification, production regression tests, and benchmarks

- Edge Case Testing: Supports testing scenarios like insufficient user balance, unprovable proofs, rejected prover results, and dry run failures

- Docker Testing: Includes instructions for testing upgrades and behavior with dockerized prover nodes

- Extensible: Test handlers are located in src/index.ts; users can add new test cases and scripts

## Quick Start

### 1. Install dependencies

```
npm install
```

### 2. Update Configs

`.env`

```
CHAIN_IDS="$REPLACE_WITH_TEST_NET_CHAIN_ID_NUMBER ..."
```

`src/config.ts`

```
server_url: "http://localhost:$REPLACE_WITH_REST_SERVER_PORT",
privateKey: "$REPLACE_WITH_YOUR_METAMASK_NODE_PRIVATE_KEY",

export const NetworkConfigs = [
  {
    chainId: 97,
    name: "bsctestnet",
    rpcUrl: "https://data-seed-prebsc-1-s3.binance.org:8545",
  },
];
```

Example

```
export const NetworkConfigs = [
  {
    chainId: 97,
    name: "bsctestnet",
    rpcUrl: "https://data-seed-prebsc-1-s3.binance.org:8545",
  },
];
```

### 3. Run all test scripts

```
bash scripts/all_tests.sh
```

## Tips

### Automating Testing of Production Sample Images

[`TEST-BRANCH-PRODUCTION-IMAGES](https://github.com/ZhenXunGe/playground-e2e-tests/tree/TEST-BRANCH-PRODUCTION-IMAGES) 
branch of the E2E repo provides many previous production images that can be used to test local deployment.

```
git clone git@github.com:ZhenXunGe/playground-e2e-tests.git e2e

cd e2e

git checkout TEST-BRANCH-PRODUCTION-IMAGES

bash scripts/cli/run_cli_tests.sh
```

For more documentation please this
[README](https://github.com/ZhenXunGe/playground-e2e-tests/blob/TEST-BRANCH-PRODUCTION-IMAGES/README.md#running-zkwasm-service-cli-tests).
