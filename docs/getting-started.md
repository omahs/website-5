---
slug: /
displayed_sidebar: GettingStartedSidebar
---
# Getting Started

## Just Starting Out

If you're new to the RISC Zero zkVM, these examples and explanations will get you oriented.
Below is a tutorial that'll help you build our version of "Hello, World!" and an introduction to the default RISC Zero project template.

* [**Hello, Multiply!**](examples/hello_multiply.md) -
Think of this as "Hello, World!" for the RISC Zero zkVM.
By following this tutorial, you'll create a program that demonstrates a number is composite (and that you know its factors).
If you're just getting started writing code for the zkVM, we recommend starting here.

* [**Understanding the Project Template**](examples/understanding_template.md) -
Here we'll take a closer look at the template we provide for starting your own RISC Zero zkVM project.
You'll understand which parts are necessary and which can be changed, and get a feel for how the project components work together.
(And if you like understanding the structure of a project before diving in, feel free to start here instead!)

## Project Examples

For more ideas about what's possible with RISC Zero, take a look at [examples](https://github.com/risc0/risc0/tree/main/examples).
We also provide detailed explanations for the factors example (in [Hello, Multiply](examples/hello_multiply.md) above) and for the password-checker example:

* [**RISC Zero Password Validity Checker**](examples/password_checker.md) -
In this example, you'll see Alice convince Bob's Identity Service that her password meets Bob's validity requirements.
This example makes use of public shared outputs that Alice can write to the RISC Zero zkVM's `journal`.

## Video Tutorials

We presented a workshop teaching the RISC Zero zkVM at ZK Hack III.
You can view the full presentation [on Youtube](https://youtu.be/wECQcmk-5ss),
or watch individual segments from [our playlist](https://youtube.com/playlist?list=PLcPzhUaCxlCgig7ofeARMPwQ8vbuD6hC5),
including examples for
* [proving factors](https://youtu.be/nWxL21hKV9s),
* [checking passwords](https://youtu.be/Yg_BGqj_6lg),
* [parsing JSON](https://youtu.be/6vIgBHx61vc), or
* [proving checkmate](https://youtu.be/vxqxRiTXGBI).

## Reference Documentation

Reference documentation for our Rust code is available on [docs.rs](https://docs.rs/).
This includes [documentation for our primary zkVM crate, risc0-zkvm](https://docs.rs/risc0-zkvm/latest/risc0_zkvm/), which includes tools for host-guest communication, proving, and receipt verification.
The full list of our crates, including links to their documentation, is available [here](https://github.com/risc0/risc0#rust-libraries).

## Source code

Our source code is available on GitHub.
Our main repository is [risc0](https://github.com/risc0/risc0).
We have created the [`cargo risczero` tool](https://crates.io/crates/cargo-risczero) to help people start their own projects using the RISC Zero zkVM,
and have a variety of [Rust examples](https://github.com/risc0/risc0/tree/main/examples).

We also have packaged Rust crates available, listed [here](https://github.com/risc0/risc0#rust-libraries).

## Connect with us

If you want to report a bug or contribute to our code, you can do so on [GitHub](https://github.com/risc0/risc0).

You're welcome to join [our Discord community](https://discord.gg/risczero) to discuss RISC Zero, ask questions, and see how other people use RISC Zero!

Follow us on [Twitter](https://twitter.com/risczero) and [YouTube](https://www.youtube.com/@risczero), and [sign up for our mailing list](https://fmree464va4.typeform.com/to/X3KJB85v) to get our latest announcements.
