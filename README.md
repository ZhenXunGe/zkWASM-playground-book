# ZKWasm Developers Guide

Welcome to the ZKWasm Developer Documentation Hub

This GitBook is the central entry point for exploring and working with the ZKWasm Playground ecosystem.

The ZKWasm Playground (ZKP) project provides a platform for verifying WebAssembly (WASM) programs using Zero-Knowledge Proofs.
Here you'll find documentation not only on ZKP concepts, but also on the supporting libraries, developer tools, and end-to-end
tests that make the Playground practical for real-world development.

## Contents

1. [ZKWasm Playground Guide](./guides/zkwasm-playground/README.md)
1. [ZKWasm E2E Testing](./guides/zkwasm-e2e-testing/README.md)
1. [ZKWasm Service Helper](./guides/zkwasm-service-helper/README.md)
1. [ZKWasm Service CLI](./guides/zkwasm-service-cli/README.md)
1. [ZKWasm Docker Prover Node](./guides/prover-node-docker/README.md)
1. [Other Tools](./guides/other-tools/README.md)

## Who This Is For

This documentation is intended for:

- Developers building on the ZKWasm Playground.
- Contributors writing new helper functions, scripts, or test cases.
- Operators running prover nodes or integrating Playground into production workflows.

## How to Use This GitBook

- Start with the [Playground Guide](./guides/zkwasm-playground/README.md) to understand the platform.
- Use the [E2E Tests section](./guides/zkwasm-e2e-testing/README.md) to understand how workflows are validated and how to add new
  test cases.
- See the [Service Helper](./guides/zkwasm-service-helper/README.md) and [CLI](./guides/zkwasm-service-cli/README.md) if you want
  to script or extend platform functions.
- Use the [Docker Prover Guide](./guides/prover-node-docker/README.md) to understand how to setup a dockerized prover node.
- Each guide contains overview, setup and tips sections.
- Index of relevant links can be found [here](./links/README.md).
- For a guide on understanding the proving technology via this page [here](https://hackmd.io/@qozymandias/rkENXr3na).

## How to Improve This GitBook

- The repo can be found [here](https://github.com/ZhenXunGe/zkWASM-playground-book).
- Please use `mdformat` for formatting.

```bash
pip install mdformat
mdformat . --wrap=130
```
