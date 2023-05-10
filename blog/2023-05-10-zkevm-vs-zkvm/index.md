---
slug: zkVM
title: 'zkEVM vs zkVM: a Single Letter Can Make a Big Difference!'
authors: [erik]
tags: [zkEVM, zkVM]
---

As the current smart contract landscape increases in complexity, with dapps
becoming more advanced and blockspace more scarce, the costs of running on-chain
code are only increasing. In other words, if your DeFi logic is becoming
computationally expensive or your on-chain game logic needs the extra compute
power, you should be looking at using a zkVM or zkEVM to move the complex
application logic off-chain.

In this blog post, I want to explain the difference a single letter can make in
this context. I’ll start with an overview of EVM, followed by zkEVM, and move on
to zkVM. While zkEVMs allow you to transport Solidity applications off-chain,
RISC Zero’s zkVM and the upcoming Bonsai network allow you to write scalable,
chain-agnostic code using Rust.

## Quick overview of EVM:

EVM stands for Ethereum Virtual Machine, and you can think of it as software
that performs all the transactions on Ethereum. Each node participates in the
Ethereum network by running this software (implementations such as geth). In
Ethereum, the transactions are represented by code in a format called the EVM
bytecode which represents instructions for the EVM. Largely, these instructions
are geared toward mathematical computations, getting information about the
blockchain, and exchanging money. There are many virtual machines out there in
the world and each one has its own specialty. Ethereum’s virtual machine is
critical because it is more specialized towards decentralized finance (DeFi).

## What is “zk” and why is everyone placing it in front of other words?

One of the coolest trends these days is to put “zk” at the front of words where
these letters stand for zero-knowledge proofs. There are many examples on
[wikipedia](https://en.wikipedia.org/wiki/Zero-knowledge_proof) (my favorite
being the “Two balls and the color-blind friend” problem). If you’re unfamiliar
with them, I suggest taking a few minutes at this point to read an example of a
zero-knowledge proof.

Long story short, zero-knowledge proofs enable verifiable computing. You can
think of this as a way to ensure which computation was done and that the result
of the computation is correct. One way for computers to agree on a result of a
computation is for each machine to run the same code and compare the results.
Depending on the computation, this can be expensive for systems with limited
resources. By using zero-knowledge proof frameworks like RISC Zero’s, machines
can ensure that the computation executed correctly by checking the mathematical
validity of the proof instead of running the same code.

Here at RISC Zero, we refer to these proofs as “receipts,” and I’ll use this
terminology for the rest of the blog. Each receipt includes a cryptographic
identifier that indicates which computation was done as well as a log of any
public outputs of the computation. While this may seem like a simple concept, it
means that machines can generate receipts to “prove” that a computation was
done.

## So what happens when you put zk in front of EVM?

The term zkEVM is used to describe software that runs a smart contract on the
EVM bytecode engine and generates a receipt for a particular computation (or
transaction). This software can usually prove that two or more receipts are
valid and generate another receipt. By using this mechanism, zkEVMs can run many
transactions and represent it using a single receipt and this is referred to as
a [“rollup”](https://vitalik.ca/general/2021/01/05/rollup.html). Rather than
doing all computations on-chain, projects written in Solidity can use zkEVMs to
scale transactions by posting a single receipt on the blockchain to represent
many transactions that happen off-chain. There are many types of zkEVM’s and if
you want to learn about them, you can read more in [this
article](https://vitalik.ca/general/2022/08/04/zkevm.html).

## zkVM: Freeing Verifiable Computation by dropping the E

At RISC Zero, we implement a zero-knowledge virtual machine (zkVM) rather than a
zkEVM. The difference between the two is that a “VM”, which stands for “virtual
machine”, is more general than the EVM. On the zkVM, you can run just about any
software that runs on a computer rather than anything that can run on Ethereum.
This computer uses the RISC-V architecture which is a set of instructions used
for general-purpose computing. This means that RISC-V doesn’t have a notion of
wallet addresses or other blockchain constructs built in. The instruction set is
mostly composed of operators that move data between memory locations and do
mathematical operations on data. While this instruction set may seem overly
general, there is no requirement for programmers to know how to program in
assembly language in order to write programs for this zkVM.

In contrast to the EVM, this underlying RISC-V emulator allows programmers to
write in languages such as Rust, C/C++, and Go for the zkVM (note, we currently
support Rust and our C/C++ and Go support is currently in-progress). This means
that programmers for the zkVM can use relevant libraries that others have
developed within the language’s ecosystem. One example is that we can run
programs that play games like
[Wordle](https://github.com/risc0/risc0/tree/main/examples/wordle) or [Where’s
Waldo](https://github.com/risc0/risc0/tree/main/examples/waldo). However, we
aren’t limited to simple games: you can run many other programs that compile to
RISC-V.

## What’s so useful about running RISC-V programs?

If you started reading about this because you wanted to learn more about
frameworks that can help you write better DeFi apps, you might be wondering why
we are working on such a generic computation framework. By allowing users to
write programs using general-purpose languages, we open up the possibilities to
writing code outside of Solidity libraries. This means that the application
logic does not need to be limited to what can be expressed using Solidity and
allow you to write chain-agnostic code. General-purpose languages like Rust
allows developers to write different kinds of programs more easily than
languages that are designed for a specific purpose. For example, you can write
a simple arithmetic calculator using Rust that takes a mathematical expression
as input, runs the mathematical computation, and returns the solution as the
output. If you increase the complexity of this calculator to support common
programming language constructs such as variables, loops, and functions, you’ve
implemented a simple language interpreter that take a program as the input, runs
the program, and returns the solution as the output. These programs can be
compiled to RISC-V and run on RISC Zero's zkVM. With Rust, you could use
existing crates to program your application instead of writing everything from
scratch.

One such library is the revm crate on rust. This crate is an implementation of
EVM that is written in Rust. By using this crate, we can run an EVM bytecode
interpreter on the zkVM. This means that you can run solidity contracts on the
EVM bytecode interpreter that runs on the zkVM! By doing so, the zkVM generates
a receipt that represents execution of the EVM running a smart contract. This
has been explored in [this blog post](https://odra.dev/blog/evm-at-risc0/) by
Odra and has been used by the [zkPoEx team to improve bug
bounties](https://risczero.com/blog/zkpoex).

## How to scale blockchains

As the current smart contract landscape increases in complexity, many people
find that the on-chain code they maintain will only increase in cost as they
develop it. In other words, if your DeFi logic is getting to become
computationally expensive or your on-chain game logic needs the extra compute
power, RISC Zero’s zkVM and the upcoming Bonsai network allow you to write
scalable chain-agnostic code using general purpose programming languages! I’ve
listed a few examples in this blog post, and we are at the very beginning of
truly scalable computation network. If you want to see what this is all about,
[get started today](https://www.risczero.com/docs), [join our
community](https://discord.gg/risczero), sign up for bonsai and help build a
decentralized and scalable internet for all.