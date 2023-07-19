---
sidebar_position: 2
slug: ./
---

# Overview of the zkVM
> WARNING: This software is still experimental, we do not recommend it for production use.

_If you're ready to start building, check out our [zkVM Quick Start] and our [zkVM example applications]._

The RISC Zero [zero-knowledge virtual machine] (zkVM) lets you [prove] correct execution of arbitrary Rust code. 
By allowing users to build zero-knowledge applications that leverage existing Rust packages, the RISC Zero zkVM makes it quick and easy to build powerful verifiable software applications. 
For example, users can provably reveal a portion of [JPG and JSON] files, while keeping the remainder of those files fully private. 

## Building a zkVM Application
A zkVM application consists of a [host program] and a [guest program]. 
The [guest program] is the part of the application whose execution will be proven by the [zkVM]. 
The [host program] is responsible for executing and proving the [guest program]. 

To prove correct execution of a zkVM application: 
1. The [guest program] is compiled to an [ELF binary].
2. The [executor] runs the [ELF binary] and records the [execution trace].
3.  The [prover] checks and proves the validity of the [execution trace], outputting a [receipt]. 

Anyone with a copy of the [receipt] can [verify] the [guest program]'s execution and read its [publicly shared outputs]. 

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/cLqFvhmXiD0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center>

To learn how to write the [host] and [guest programs] for your application, check out our [zkVM Quick Start]. 
To see some examples that work out-of-the-box, check out our [zkVM example applications].

## Deploying a zkVM Application
Once you've built a zkVM application, you can generate proofs on your own machine(s) or you can make requests to [Bonsai] to generate proofs as needed. 

For local proof generation, we recommend a machine with at least 16GB of RAM. 
Some performance benchmarks are available from the [performance benchmarks] page, along with information for generating your own benchmarks.
Options for generating proofs using GPU acceleration and skipping proof generation are documented in the [feature flags].

## Next Steps
*Ready to start building zkVM applications?* <br/>
Check out our [zkVM Quickstart](quickstart.md) or our [zkVM example applications]. 

*Looking for information about blockchain integration?* <br/>
Check out [Bonsai].

[Bonsai]: ../bonsai/
[receipt]: ../terminology#receipt
[ELF binary]: ../terminology#elf-binary
[execution trace]: ../terminology#execution-trace
[executor]: ../terminology#executor
[feature flags]: https://github.com/risc0/risc0#feature-flags
[guest program]: ../terminology#guest-program
[guest programs]: ../terminology#guest-program
[host]: ../terminology#host-program
[host program]: ../terminology#host-program
[JPG and JSON]: https://www.risczero.com/news/waldo
[performance benchmarks]: benchmarks
[prove]: ../terminology#validity-proof
[proofs]: ../terminology#validity-proof
[prover]: ../terminology#prover
[publicly shared outputs]: ../terminology#journal
[verify]: ../terminology#verify
[zero-knowledge virtual machine]: ../terminology#zero-knowledge-virtual-machine-zkvm
[zkvm]: ../terminology#zero-knowledge-virtual-machine-zkvm
[zkVM Quick Start]: ./quickstart.md
[zkVM example applications]: https://github.com/risc0/risc0/tree/v0.16.0/examples
