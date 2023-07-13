---
id: tech_faq
---
# FAQ

-------------------------------
## Contents
- [FAQ](#faq)
  - [Contents](#contents)
  - [ZK Basics](#zk-basics)
  - [Building on the zkVM](#building-on-the-zkvm)
    - [Code Troubleshooting](#code-troubleshooting)
    - [zkVM Application Design](#zkvm-application-design)
    - [Features, Performance, and Limitations](#features-performance-and-limitations)
  - [The RISC Zero Circuits](#the-risc-zero-circuits)
  - [Security](#security)

-------------------------------

## ZK Basics
<details closed>
<summary>Q:
What is a zero-knowledge proof?
</summary>
A:
A zero-knowledge proof (or ZKP) is <a href="https://en.wikipedia.org/wiki/Zero-knowledge_proof">"a method by which one party (the prover) can prove to another party (the verifier) that a given statement is true [without] conveying any additional information"</a>. 
RISC Zero's zkVM makes it easy to produce ZKPs to prove the correct execution of arbitrary code. <br/>
<br/>
When Alice executes code inside the zkVM, Alice gets back a <a href="https://dev.risczero.com/terminology#receipt">receipt</a>. 
Alice can pass the receipt to Bob, who can then <a href="https://dev.risczero.com/terminology#verify">verify</a> the receipt.
<br/>
<br/>
By verifying the receipt, Bob can confirm that the expected code executed and produced the asserted results. 
Any inputs Alice passes to the program during execution will be private unless Alice chooses to share them.
</details>
 <br/>

## Building on the zkVM
### Code Troubleshooting
<details closed>
<summary>
Q: I'm running into build errors. Where should I look for help?
</summary>
A: Some known issues and workarounds are tracked on GitHub under the <a href="https://github.com/risc0/risc0/issues?q=is%3Aissue+is%3Aopen+label%3A%22rust+guest+workarounds%22">"rust guest workarounds"</a> tag. 
If you can't find your problem here you can open a <a href="https://github.com/risc0/risc0/issues">new issue</a> or reach out to us on <a href="https://discord.gg/risczero">Discord</a>.
</details>
<br/>

### zkVM Application Design
<details closed>
<summary>
Q:
What do I do with the receipt once I’ve created it?
</summary>
A:
After Alice creates a <a href="https://dev.risczero.com/terminology#receipt">receipt</a>, she'll typically pass it to Bob who will want to <a href="https://dev.risczero.com/terminology#verify">verify</a> its authenticity. 
At a minimum, Bob will need access to the <a href="https://dev.risczero.com/terminology#image-id">image ID</a> of the expected program.
For most cases, Bob will want to know what code was run, and will therefore also want the <a href="https://dev.risczero.com/terminology#elf-binary">ELF file</a> or the source code that generated it.
Bob can verify the receipt was created by this code by constructing the <a href="https://dev.risczero.com/terminology#image-id">image ID</a> from the given ELF file and using it for verification. <br/>
<br/>
In our <a href="https://github.com/risc0/risc0/tree/v0.16.0/examples">examples</a>, the receipt is generated and verified within the same program, but typically the receipt will be passed to a third party for verification.
</details>

<details closed>
<summary>
Q:  When can information be shared with the guest zkVM? How do you prevent buffer overflows?
</summary>
A: 
Data can be sent during program execution from the host to the guest via a memory map. 
The host-writeable memory is write-once, meaning that adjacent memory regions cannot be overwritten and executed.
</details>

<details closed>
<summary>
Q:
How do I know which computations should be performed in the guest zkVM, and which can be offloaded to the host?
</summary>
A: If you don't need to perform a computation securely, if others don't rely on it, and if it doesn't produce outputs that others rely on, it can probably be performed outside of the zkVM. <br/>
<br/>
However, consider that code run in the RISC Zero zkVM can be shown to behave as expected even on a host that is entirely untrusted. 
To get the most value out of this guarantee, we recommend dividing the computational labor with an untrusted host in mind. 
That is, other parties should not need to trust the host's output or operations in order to benefit from the work done in the zkVM.
</details>

<details closed>
<summary>
Q:
What exactly is the image ID?
</summary>
A: The image ID uses hashing to relate the receipt to the code that produced the receipt. 
Specifically, the image ID is a Merklization of the image of the initial zkVM memory state.  
For more details, see <a href="https://www.youtube.com/watch?v=QwzrBHHkzFE&list=PLcPzhUaCxlCirUkJY0ltpjdtzWcz5U_6y&index=4">this clip from Study Club</a>.
</details>
<br/>

### Features, Performance, and Limitations
<details closed>
<summary>
Q: Are performance benchmarks available?
</summary>
A: Yes. We have a <a href="https://dev.risczero.com/datasheet.pdf">datasheet</a> with performance benchmarks, and you can also generate your own benchmarks. More details are available on the <a href="https://dev.risczero.com/zkvm/benchmarks">benchmarks page</a>.
</details>

<details closed>
<summary>
Q: What languages can I use to develop zkVM applications?
</summary>
A: We recommend Rust for writing zkVM applications. 
Although technically the zkVM can execute any RISC-V code, we only have documentation and API support for Rust development. 
Development in C++ is also possible, but proceed at your own risk. 
You can reference the <a href="https://github.com/risc0/risc0/tree/v0.11.0/examples/cpp">examples in C++</a> that were included in the 0.11 release, although we've made substantial changes since that release, and we're available to answer questions on <a href="https://discord.gg/risczero"> Discord</a> as needed.
</details>

<details closed>
<summary>
Q: What is the maximum execution length for a program running on the zkVM?
</summary>
A: Since we added support for <a href="https://risczero.com/blog/continuations"> continuations</a>, the execution length can be very large. 
So far, we've made proofs for executions that exceed 4 billion cycles, and there's plenty of room to expand that further. 
</details>

<details closed>
<summary>
Q: I have a specific Rust crate I'd like to use. Will it work inside the zkVM?
</summary>
A: Each night, we check the top 1000 Rust crates for zkVM compatibility. 
You can see the results <a href="https://risc0.github.io/ghpages/dev/crate-validation/index.html"> here</a>. 
As of this writing, 71% of the top 1000 Rust crates work inside the zkVM. <br/>
<br/>
If the crate you'd like to use isn't working, there may be a workaround <a href="https://github.com/risc0/risc0/issues?q=is%3Aissue+is%3Aopen+label%3A%22rust+guest+workarounds%22">here</a>. 
If there's not already a workaround, please <a href="https://github.com/risc0/risc0/issues/new">open an issue</a> or reach out on <a href="https://discord.gg/risczero">Discord.</a>
</details>

<details closed>
<summary>
Q:
If I want the guest to process large volumes of data during execution, I might be constrained by space limitations. What are my options?
</summary>
A:
If data is loaded from the host to restrict guest program size, the most significant limitation on zkVM data processing is a constraint on instruction cycles. 
Loading data into the guest costs instruction cycles, as does data processing.

There are workarounds for data limitations if the data is only included to ensure that its integrity becomes part of the proof of computation. 
If the data can be processed externally and simply needs to be verifiably unchanged, consider processing data externally and sending the guest a Merkle proof or (if no processing is needed) generating a SHA of a large dataset.

In the future, we plan to lift these processing limitations using continuations and recursion.
</details>

<details closed>
<summary>
Q:
I’d like to speed up the processing done inside the zkVM. What are my options?
</summary>
A:
For cryptographic operations, it is possible to build ‘accelerator’ circuits such as our implementation of SHA26. 
Fast cryptography is sufficient to support many ‘DeFi’ applications. 
For many other applications, it is possible to perform most computation on the host (outside the zkVM) and then verify the results in the zkVM.
</details>

<br/>



## The RISC Zero Circuits
<details closed>
<summary>
Q: Do I need to write a ZK circuit to build on RISC Zero?
</summary>
A: No! 
We take care of the circuit building so that you can focus on building applications. 
Everything you'll need to build is outlined in the <a href="https://dev.risczero.com/zkvm">zkVM docs</a> and the <a href="https://dev.risczero.com/bonsai">Bonsai docs</a>.
</details>

<details closed>
<summary>
Q: What do RISC Zero's circuits do?
</summary>
RISC Zero has three circuits: one that executes RISC-V code, one that's used for recursion, and one that is used for a STARK-to-SNARK conversion.

* The RISC-V circuit receives an ELF binary file as a public input and private inputs from the host; the output of the RISC-V circuit is a receipt.
* The recursion circuit is specialized to prove the verification of RISC Zero receipts; this circuit is used in order to compress many RISC Zero receipts into a single receipt. 
* The STARK-to-SNARK circuit is used to translate a STARK proof into a SNARK proof, which enables on-chain verification. 

</details>

<details closed>
<summary>
Q: How did you make your RISC-V circuit?
</summary>
A: The RISC-V circuit is found in step.cpp.inc and is generated by the make-circuit program. It consists of:

* Code to emulate RISC-V, including decoding RISC-V instructions and constructing the execution trace.
* Code to evaluate the constraint polynomials that check the execution trace.
* Auxiliary data to support structures such as ‘taps’.

Because the data structures supporting all three of these need to match very carefully, we created a ‘circuit compiler’ program that generates code for all three of these systems.
</details>

<br/>

## Security
<details closed>
<summary>
Q:
How can we use the image ID to determine if program code is altered before execution?
</summary>
A: The image ID can be determined from the compiled ELF source code. 
Someone wishing to confirm that a receipt corresponds to Rust source code can compile that code targeting the RISC Zero zkVM and verify that the image ID resulting from this compilation matches the image ID in the receipt. <br/> <br/>

*Note: We plan to enable a deterministic connection between the Rust source code and the image ID. 
At the moment, the conversion from Rust source code to ELF binary is non-determinstic (because `cargo` builds are non-determinstic).  
What this means for zkVM application design is that checking the correctness of the ImageID requires access to the compiled ELF file. 
For the latest status on this issue, check the discussion on the <a href="https://https://github.com/risc0/risc0/issues/116">GitHub issue</a>.*
</details>
<details closed>
<summary>
Q: If the guest zkVM lives on the host machine, can’t the host still tamper with the compiled code?
</summary>
A: Like other zk-STARKs, RISC Zero’s implementation makes it cryptographically infeasible to generate an invalid receipt:

* If the binary is modified, then the receipt’s seal will not match the image ID of the expected binary.
* If the execution is modified, then the execution trace will be invalid.
* If the output is modified, then the journal’s hash will not match the hash recorded in the receipt.

</details>
