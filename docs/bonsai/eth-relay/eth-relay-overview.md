# Bonsai ETH Relay

The Bonsai ETH Relay intermediates between your app contract and the Bonsai proving service. Using the Bonsai Eth Relay allows you to write concise Solidity contracts that harness the power of off-chain ZK computation. 

At a high level, here's how it works:

![Bonsai ETH Relay overview](../../img/eth-relay-diagram.jpg)

<!-- TODO: Highlight the relay sections of this diagram -->

The Bonsai ETH Relay consists of a relay contract deployed on chain and an off-chain relay that connects the relay contract to the [Bonsai proving service](../bonsai-overview.md#bonsai-a-zero-knowledge-proving-service). In order to use the Bonsai ETH Relay, dApp developers must have completed the following steps:

1. Deployed a smart contract on chain that calls the relay contract
2. Uploaded a compiled program for the zkVM to the Bonsai proving service

## Getting Started

The [Bonsai Foundry Template] is the best place to get started building on Ethereum. 
You may also want to check out our [Bonsai Quick Start](../quickstart.md) page. As a reminder, projects developed here are not production-ready and the ETH relay is subject to change. 

[Bonsai Foundry Template]: https://github.com/risc0/bonsai-foundry-template
