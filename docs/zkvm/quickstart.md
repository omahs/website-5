---
sidebar_position: 3
slug: ./quickstart
---

# zkVM Quick Start

The quickest way to get started building, managing, and testing RISC Zero projects is with the [cargo risczero] tool. 
The readme on the [factors tutorial] contains step-by-step instructions for building your first project. 

Alternatively, you can start building by using one of these [demo applications], which work out-of-the-box. 

If you're looking to integrate the zkVM into blockchain applications, you'll want to check out the [Bonsai Quick Start]. 

## Building and Running zkVM Applications

You can build and run your zkVM applications using your own hardware, or you can upload your [guest program] to [Bonsai] and make requests for proof generation as needed. 

To run the zkVM on your own machine, we recommend at least 16GB of RAM. 
The readme files on the [zkVM demo applications] show `cargo` commands for local proof generation. 
Options such as GPU acceleration and skipping the proof generation are documented in the [feature flags]. 

[guest program]: ../../terminology#guest-program
[Bonsai]: ../../bonsai/
[feature flags]: https://github.com/risc0/risc0#feature-flags
[zkVM demo applications]: https://github.com/risc0/risc0/tree/v0.16.0/examples/
[cargo risczero]: https://docs.rs/cargo-risczero/0.16/cargo_risczero/
[demo applications]: https://github.com/risc0/risc0/tree/v0.16.0/examples
[factors tutorial]: https://github.com/risc0/risc0/tree/v0.16.0/examples/factors#readme
[Bonsai Quickstart]: ../../bonsai/setting-up-bonsai
