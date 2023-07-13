---
slug: ./
---

# Bonsai Overview

Bonsai is a collection of tools enabling boundless computation on any blockchain. The Bonsai zero-knowledge proof network will parallelize and scale proving your code. Whether you're looking to take heavy computations off-chain or need zero-knowledge proof for your trustless, verifiable software, check out Bonsai!

Bonsai is still in early development. As such we have concentrated on a few use cases: At the moment, we have the core Bonsai proving service and an ETH Relay for accessing Bonsai from Ethereum. This page will keep you updated on the status of these and other Bonsai tools.

![Bonsai ETH Relay overview](../img/eth-relay-diagram.jpg)

<!-- revise diagram with "you create"/"bonsai creates" colors -->

You can use Bonsai from an Ethereum smart contract with the pictured architecture. In this diagram, all you are responsible for as a developer using Bonsai are:
* The smart contract invoking Bonsai
* The smart contract handling Bonsai's results via callback
* The program you want Bonsai to prove

This architecture utilizes both the ETH Relay and the proving service; **other architectures are possible**, and as we develop and publish further tools we'll update with other example architectures.

## RISC Zero zkVM: the proof engine behind Bonsai

_Status: [Available and open source](https://github.com/risc0/risc0)_

Under the hood, Bonsai uses the RISC Zero zkVM to prove your programs. With the zkVM, you have access to recursive proofs, a general-purpose circuit (with a bespoke circuit compiler), state continuations, and continuous improvements to the proving algorithm.

## Bonsai: A zero-knowledge proving service

_Status: Pre-Alpha, [waitlist] available_

The Bonsai proving service can be used standalone or directly integrated with smart contracts and blockchains. If you're interested in Bonsai, join our [waitlist], and learn more in our [litepaper] and [talks](https://youtu.be/nVAs2i-_Iyo?t=3044).

## Bonsai ETH Relay: Connecting off-chain proofs and on-chain applications

_Status: Pre-Release, [documentation](eth-relay/eth-relay-overview.md) and [Bonsai Foundry template](https://github.com/risc0/bonsai-foundry-template) available_

The Bonsai ETH Relay connects your Ethereum dApps to Bonsai. Smart contract developers can call our proving service through an on-chain relay contract connected to the Bonsai proving service. If you'd prefer to engage with Bonsai proving service directly, we'll be rolling out the means to do so in the near future.

## Where we're headed

We're building technology that allows anyone to generate highly performant zero-knowledge proofs for a variety of applications. We want to make zero-knowledge proof integration into Ethereum, L1 blockchains, Cosmos app chains, L2 rollups, and dApps possible with minimal development effort. To learn more, read our [litepaper].

[waitlist]: https://fmree464va4.typeform.com/to/t6hZD54Z
[litepaper]: ../litepaper