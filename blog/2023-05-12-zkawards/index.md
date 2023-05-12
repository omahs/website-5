---
slug: zkhack
title: Project Awards ZKHack 
authors: [kay]
tags: [zkhack, zksummit, lisbon]
---
# ZKHack Lisbon

We recently participated in [ZKHack Lisbon](https://www.zklisbon.com/), [ZK Hack](https://zkhack.dev/)'s first in-person hackathon.
Thanks to [everyone who contributed projects](https://zk-lisbon.devfolio.co/projects)!

Below is a list of all [RISC Zero prize](https://zk-lisbon.devfolio.co/prizes?partner=RISC+Zero) winners from ZK Hack Lisbon. We've provided longer descriptions for these projects as an added thank you to the four teams that won $2000. 

To support future hackathon participants, we've included *why* our judging team loved the top projects. Our judging criteria will vary from hackathon to hackathon, but we're excited to see development in emerging ZK application spaces, inventive uses of ZK tech, and projects that demonstrate the simplicity and power of ZK. And because doing is teaching, we love submissions that either contain self-explanatory educational content or insightful supplementary docs.

## RISC Zero Prize Categories

We encouraged participants at ZKHack Lisbon to submit two types of project entries:

| | Problem description | 
|---|---|
|Challenge #1 | Build an application that uses the RISC Zero zkVM. |
|Challenge #2| Write code that utilizes data serialization or deserialization crates in the guest. |

# RISC Zero Hackathon Prize Winners

## Winning Team Projects: $2000 Level

### Mindf*ck: Code Obfuscation For Fun And Profit
* Team: Zeroskill
* Category: Serialization and Deserialization (Challenge #2)
* [Project submission](https://devfolio.co/projects/mindfuck-0f98)
* [Project link](https://github.com/hananbeer/mindfuck)

To obfuscate code execution, the Zeroskill team has added a Rust-based [Brainf\*ck](https://esolangs.org/wiki/Brainfuck) interpreter to the guest program. With this addition, the execution of an interpreted program is captured by the guest zkVM.

As an example, the following "Hello, World!" program string might be passed into the guest as program input:

```
--<-<<+[+[<+>--->->->-<<<]>]<<--.<++++++.<<-..<<.<+.>>.>>.<<<.+++.>>.>>-.<<<+.
```

The guest's public outputs consist of the executed "Hello, World!" program's final memory state, the values which the Brainf\*ck program dictates should be written to `stdout`, and a hash of the program source (the string shown above).

Even setting aside code obfuscation, this is a fantastic example of how easily nontrivial Rust code may be written for the zkVM. From an educational perspective, we loved that this team created an example of interpretable code as input (and memory layout as output!).

### Zero-Knowledge Decision Tree Prediction
* Team: Zktex
* Category: zkVM Applications (Challenge #1)
* [Project submission](https://devfolio.co/projects/zero-knowledge-decision-tree-prediction-zkdtp-6b5f)
* [Project link](https://github.com/only4sim/ZK-DTP)

This team tackled a popular use case for ZK in machine learning: how can an ML provider make trustworthy predictions without disclosing their model? This problem arises in applications when the ML model is sensitive enough that releasing it might become a privacy issue.

Categorical classification with decision trees starts with a tree built from labeled data. Starting at the tree root, feature values are used to guide decisions about which path to follow down to a leaf node representing a single category as the outcome.

As a demonstration, this team's guest zkVM program used a hard-coded decision tree based on the IRIS dataset, which categorizes flowers based on their measurements. Measurements for a single flower are passed into the guest, and the classification result is added to the journal as public output.

Building an ML solution is an ambitious hackathon project. We thought that the team made great decisions about algorithms and implementation details to effectively demonstrate ZK's potential for ML in a weekend. The accompanying demonstration elevated this project from an interesting ML submission into a nice educational piece.

### Zero-Knowledge Wordle
* Team: RockawayX
* Category: zkVM Applications (Challenge #1)
* [Project submission](http://zkwordle.rockawayx.com/)
* [Project link](https://github.com/RBFLabs/zk-wordle)

This project implemented a fair version of Wordle, in which a client makes word guesses against a server that generates feedback in the form of receipts. The journal of each receipt contains feedback about the client's word guess (i.e., "right letter, wrong position") as well as a hash of the correct answer. 

The server is considered 'fair' because the client can detect whether the server moves the target during play. To accomplish this, the client confirms that the hashed correct answer has not changed from receipt to receipt.

Although [the idea of playing fair Wordle isn't new](https://github.com/risc0/risc0/tree/main/examples/wordle), the architecture for this project was easily as interesting as the game design. The RISC Zero server uses a RISC Zero prover behind an API server. The gameplay results are stored in a contract on chain. As a working example that demonstrates running a RISC Zero verifier in WASM, we particularly appreciated the browser-based client.

### Proof of Physical Item Using NFC Devices With On-Device AES Keys

* Team: Nvid
* Category: zkVM Applications (Challenge #1)
* [Project submission](https://devfolio.co/projects/proof-of-physical-item-3541)
* [Project link](https://github.com/mvid/nfc_risc_zero)
  
This project used ZK proofs to implement message signature verification. This team used [NTAG 424 chips](https://www.nxp.com/products/rfid-nfc/nfc-hf/ntag-for-tags-labels/ntag-424-dna-424-dna-tagtamper-advanced-security-and-privacy-for-trusted-iot-applications:NTAG424DNA#:~:text=The%20NTAG%20424%20DNA%20is,with%20crypto%2Dsecure%20access%20permissions.) that include an on-device AES key and support for AES-128 encryption operations.

When the NFC device is tapped, NTAG creates a SUN (Secure Unique NFC) message using an AES key, a read count, and a UID. In this project, the signed NFC message is checked by regenerating the SUN message in a guest program and confirming the messages match.

The AES key and UID remain constant for each device and are hardcoded into the guest program. (Note that this means each receipt must be verified with an image ID unique to the device on which it was generated.) The read count and expected SUN message are passed as guest inputs. Within the guest, the read count, hardcoded key, and hardcoded UID are used to generate a fresh SUN message for comparison.

We loved that this project interacts with a hardware solution and presents an interesting proof of concept for proximity-based physical interactions. We especially appreciated the use of AES in the guest.

## Winning Team Projects: $1000 Level
### RISC Zero HMAC Implementation

* Team: Pavlovdog
* Category: Serialization and Deserialization (Challenge #2)
* [Project submission](https://devfolio.co/projects/risk-hmac-implementation-and-miden-amm-emulator-30ab)
* [Project link](https://github.com/pavlovdog/risc0/tree/main/examples/hmac)

### Dread Pirate Roberts Marketplace: A zkReputation-Based Marketplace For High-Value Transactions
* Team: Topsy Kretts
* Category: zkVM Applications (Challenge #1)
* [Project submission](https://devfolio.co/projects/dread-pirate-roberts-marketplace-79b8)
* [Project link](https://github.com/dread-pirate-roberts-fellowship/zk-reputatation-marketplace)


## Winning Team Projects: $500 Level

### Ting Tong: A Turn-Based Guessing Game
* Team: Zerodem
* Category: zkVM Applications (Challenge #1)
* [Project submission](https://devfolio.co/projects/tingtong-2758)
* [Project link](https://github.com/tribuste/risc0/tree/main/examples/ting-tong)


### Whitebox: Composable, Transparent, Configurable, and Verifiable Algorithms
* Team: Alexander Kozlov
* Category: zkVM Applications (Challenge #1)
* [Project submission](https://devfolio.co/projects/whitebox-d0fd)
* [Project link](https://github.com/basedalexander/whitebox-exec)

### Crosschain Escrow on L3 \<\> L1 Validity Rollups
* Team: Wavect
* Category: zkVM Applications (Challenge #1)
* [Project submission](https://devfolio.co/projects/crosschain-escrow-on-l-lessgreater-l-validity-rollups-1614)
* [Project link](https://github.com/wsdt/risc0-bonsai_multichain-escrow)


## Keep on hacking <3
If you missed this zero-knowledge hackathon, you can connect with participants and find out about new events at the [ZKHack Discord](https://discord.gg/KprSfyTDvt). If you're curious about the other ZKHack Lisbon winners, take a peek at this [Twitter megathread](https://twitter.com/__zkhack__/status/1643571990526033920). And while you're at it, stop by the [RISC Zero Discord](https://discord.gg/risczero) and say hello! 