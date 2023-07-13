# Deploy Bonsai ETH Relay Projects

Welcome! If you're here, we're assuming you've already built your app contract and zkVM program using the [ETH Relay](../eth-relay/eth-relay-overview.md). If you've finished development on the Bonsai Foundry template, you have a working standalone project (using infrastructure mocked in [Foundry](https://github.com/foundry-rs/foundry)) for the ETH Relay. It should contain:
* A finished app contract
* A working provable program for the zkVM

## Flexible deployment options

The final steps in deploying your project are to:

* Get access to the Bonsai proving service API
* Upload your compiled zkVM program using the Bonsai API
* Deploy your smart contract
* Point it at our on-chain relay contract

However, deploying an app contract and calling a live service at the same time is a lot to troubleshoot if needed. As an intermediate step, we offer you the option to make real calls to the Bonsai proving service using your mock services and locally deployed app contract.

## Deployment with a local chain: Call Bonsai using your local setup

Once you've obtained access to the Bonsai API and uploaded your compiled zkVM program, you'll be able to run your off-chain computation on Bonsai simply by setting an environment variable.

## Goerli deployment: add your app contract to the blockchain

Once you're ready to deploy your app contract, you'll be able to seamlessly transition to using the on-chain relay contract to use Bonsai via the Bonsai ETH Relay.

## Can my project be deployed?

If you're reading this outside of a hackathon or special event, please sign up for the [Bonsai access waitlist](https://fmree464va4.typeform.com/to/t6hZD54Z) for announcements on the public release of the Bonsai proving service and the Bonsai ETH Relay. In the meantime, we'll keep you up to date on Bonsai project updates in our [Bonsai overview](../bonsai-overview.md).

For hackers and early explorers, you'll be given special instructions on how to obtain [Bonsai](../bonsai-overview.md#bonsai-alpha-a-zero-knowledge-proving-service) API access at your event so you can connect to our live proving service. If you're here because you're working on a hackathon project, be sure to connect via [Discord]

## What is required for deployment?

Once you've developed your app contract and provable off-chain zkVM program, you can complete a few post-development deployment steps to start working with our ETH relay service. Keep in mind that this project is pre-alpha, so for now you'll only be able to complete these steps at special pre-release events. 

If you've obtained access to the Bonsai API, you're ready to test out your interaction with the Bonsai proving service. For everyone else, we'd like to give you a sneak preview of deployment, so you know what you'll be getting into before ever touching code.

Our final set of required integration steps may change, but we'll do our best to keep it clean and simple.
