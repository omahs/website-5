---
sidebar_position: 1
slug: ./
---

# Proof System Overview

When the RISC Zero [zkVM] executes, it produces a [SessionReceipt] that serves as a proof of validity of a given [Session]. 

To confirm that a [SessionReceipt] was honestly generated, use [SessionReceipt::verify] and supply the [ImageID] of the code that should have been executed as a parameter. 

The SessionReceipt includes a [journal], which contains the public outputs of the Session. 
The contents of the [journal] are specified by calling [env::commit()] and [env::commit_slice()] in the [guest] code. 

Cryptographically speaking, the [SessionReceipt] is a collection of [ZK-STARKs], each of which proves a single [Segment]. 

The details of the RISC Zero ZK-STARK are described in our [ZKP Whitepaper] and in this [IOP Sequence Diagram].

## Learn More
### About the zkVM
- [Video Explainer from zkHack](https://www.youtube.com/watch?v=8hwY88xJoyM&list=PLcPzhUaCxlCgig7ofeARMPwQ8vbuD6hC5&index=8)
- [Written Explainer](../zkvm/zkvm_overview.md)

### About STARKs
- [STARKs reference doc](../../reference-docs/about-starks.md)
- STARK by Hand Tutorial
  - [Website version](stark-by-hand.md)
  - [Google Sheet version](https://docs.google.com/spreadsheets/d/1Onr41OozD62y-B0jIL7bHAH5kf771-o4xvmnHUFpOyo/edit?usp=sharing) 
  - [Printable Version](assets/fibonacci-stark.pdf)

### About RISC Zero
- All our public talks and podcasts are available on our [YouTube channel]. 
- [RISC Zero Study Club] is intended to help make the technology underpinning RISC Zero more accessible. Past sessions include: 
  - [What is RISC-V and how does it relate to RISC Zero?](https://www.youtube.com/watch?v=11DIflEwx50&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=5)
  - [Intro to Finite Fields](https://www.youtube.com/watch?v=11DIflEwx50&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=2)
  - [Intro to Reed-Solomon Codes](https://www.youtube.com/watch?v=11DIflEwx50&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=3)
  - [Intro to Number Theoretic Transforms](https://www.youtube.com/watch?v=11DIflEwx50&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=4)
  - [Intro to the FRI Protocol](https://www.youtube.com/watch?v=11DIflEwx50&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=1)
  - [Finite Field Implementation Options: Barrett & Montgomery Multiplication](https://www.youtube.com/watch?v=hUl8ZB6hpUM&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=6)

[zkVM]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/
[SessionReceipt]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/receipt/
[Session]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/struct.Session.html
[SessionReceipt::verify]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/receipt/#usage
[ImageID]: https://docs.rs/risc0-build/latest/risc0_build/
[journal]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/receipt/struct.SessionReceipt.html#structfield.journal
[env::commit()]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/guest/env/index.html#functions
[env::commit_slice()]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/guest/env/index.html#functions
[guest]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/guest/index.html
[ZK-STARKs]: ../../reference-docs/about-starks.md
[Segment]: https://docs.rs/risc0-zkvm/latest/risc0_zkvm/struct.Segment.html
[ZKP Whitepaper]: https://www.risczero.com/proof-system-in-detail.pdf 
[IOP Sequence Diagram]: proof-system-sequence-diagram.md
[RISC Zero Study Club]: https://risczero.com/studyclub
[YouTube Channel]: https://www.youtube.com/watch?v=MYYb5TXdm4c&list=PLcPzhUaCxlCgCvzkkaBWzVuHdBRsTNxj1
