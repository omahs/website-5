# Understanding Waldo

[Where’s Waldo](https://en.wikipedia.org/wiki/Where%27s_Wally%3F) is a [favorite analogy](https://medium.com/swlh/a-zero-knowledge-proof-for-wheres-wally-930c21e55399) for zero-knowledge proofs.
In particular, if you want to prove you know where Waldo is, without revealing his location, you can:

1. Have your friend, the verifier, print a Where’s Waldo puzzle on a big poster board.
2. Take the poster board, turn around and cut out Waldo from the image. Dispose of the rest.
3. Hand the cut out of Waldo to your friend, who makes sure it’s really Waldo.

This is *kind of* like a zero-knowledge proof (with less cryptography and more craft supplies), but why not implement a real zero-knowledge proof to show you know where Waldo is?

This example implements a RISC Zero program which allows a prover to convince a verifier they know Waldo’s location in a public Where’s Waldo puzzle, without revealing Waldo’s coordinates.

You can find the source code for this example in the [waldo project in our examples directory](https://github.com/risc0/risc0/tree/main/examples/waldo).
Browse the code, and run the example yourself, as your read to get a solid understanding for its parts.

## Overview

This example of implementing a proof for Where’s Waldo is designed to help you understand some useful techniques in creating more advanced programs with RISC Zero.

In particular, it should help you understand:

- Using I/O to have the host provide the guest data on request.
- Merkleizing large data to give the guest verifiable access to small parts of it.
- Using external libraries in the guest to avoid reinventing the wheel.

This tutorial will *not* include:

- How to create a project based on the starter template (see [Hello, Multiply](https://www.risczero.com/docs/examples/hello_multiply))
- Project structure and information about the build system (see [Understanding the RISC Zero zkVM Starter Template](https://www.risczero.com/docs/examples/understanding_template))
- The cryptographic theory behind the RISC Zero zkVM (see our [proof system explainers and reference materials](https://www.risczero.com/docs/explainers))
- The internal components of the RISC Zero zkVM (see our [Overview of the zkVM](https://www.risczero.com/docs/explainers/zkvm) article)
- Design considerations for programs that use multiple RISC Zero zkVM guest methods (see our [voting machine example](https://github.com/risc0/risc0-rust-examples/tree/main/voting-machine))

## Implementing Where’s Waldo

The approach for this example is similar to the analogy. It takes the full Where's Waldo puzzle image and “cuts out” just Waldo.

This cutting out operation takes place in the zkVM guest which keeps the inputs, and in particular Waldo’s coordinates, private while allowing the verifier to confirm that computation was done correctly.
In this case, the guest’s journal includes a commitment to the Where’s Waldo puzzle image and the cut out image of Waldo.

Once the verifier has checked the receipt and the source image commitment in the journal, and given the cut out image a look to verify it really is Waldo, they can be sure that Prover knows where Waldo is in the puzzle.

Key to this procedure is that the verifier checks that the Prover did not cut Waldo out of some other source image than the verifier was expecting
(e.g. that they didn't go and cut Waldo out of a different puzzle because they don’t actually know where Waldo is in the puzzle the verifier gave them).
This is a common problem when implementing verifiable programs, and this is what the source image commitment handles in this example.

Now let’s talk about one strategy to tackle this problem, especially for large data such as images, **Merkleization**.

### Merkleization

In the simplest approach, the guest program could create a commitment simply by hashing the whole Where’s Waldo image in memory and use the hash as a commitment.
Unfortunately, hashing the whole image, which we expect to be rather large, is cost prohibitive in the guest.
So how can the guest access the data it needs without giving the host an opportunity to give it inconsistent data (e.g. swapping out the Where’s Waldo puzzle)?

Because we only need access to a relatively small portion of the image to produce the cutout, a viable approach is to split the image into a vector of small image chunks and use a [Merkle tree](https://en.wikipedia.org/wiki/Merkle_tree) to commit to this vector.
As needed, the zkVM guest can then ask the host chunks of the image, and along with each chunk the host can provide a Merkle path that proves the chunk is part of the committed image.
This gives the guest access to the data it needs, while ensuring it is all part of the committed image.

Merkle trees are an example of a _vector commitment_.
Given a Merkle root, which is simply a SHA-256 digest, the guest has a commitment from the prover binding it to the full data vector.
In particular, the guest can then send a request to the host for a specific element in the full vector, and the host will respond with the data _and_ a Merkle path.
With this Merkle path, which is a short chain of hashes leading back to the root, the guest can verify the data came from the committed vector.
This is great because it means the host can commit to very large data vectors, on the order of gigabytes or even terabytes, and the guest can access small portions of it on demand without reading the whole thing.
This trick, of having the prover commit to a large amount of data then the verifier reading a small portion, is actually at the core of the RISC Zero zero-knowledge proof.

In the Where's Waldo example, the data we want to Merkleize is the source Where's Waldo puzzle image.
In order to turn it into a vector, we cut the image up into chunks and the give each an one-dimensional index.
E.g. an image split into four chunks could be numbered 0 as the top-left quadrant, 1 as the top-right, 2 as the bottom-left, and 3 as the bottom-right.
This vector of chunks is then hashed into a Merkle tree and the guest is given the root.

When the verifier wants to check the receipt, they first repeat the same Merkleization procedure as the prover, starting from the source image.
If they started with the same image, they will get the same root.
They can then compare this root with the commitment in the journal.
If it is equal, the can be assured that the prover ran the guest with the same image as the verifier expected.

In the `waldo_core::merkle` module is implemented a wrapper on the `merkle_light` crate with support for using the SHA-256 guest circuit, and providing a `VectorOracle` abstraction.
In the `waldo_core::image` module is implemented a specific `MerkleTree` type for images, and an `ImageOracle` type which can be used in the guest for image operations.
These modules implement the ideas described above.

Similar Merkle tree abstractions can be used to, for example, ensure a secret word is part of a dictionary, a payment destination is not in a list of banned addresses, or that a user is in the set of authorized users.

### Image Manipulation

In order to manipulate the image and cut-out Waldo, and in particular to crop and apply a mask, this example utilizes the popular `image` crate.
This is enabled by implementing `image::GenericImageView` on `ImageOracle`.
With that trait, many of the image operations provided in the `image` crate, and by [others](https://docs.rs/imageproc/latest/imageproc/), can be used on `ImageOracle` inside the guest.
A similar approach could be used to produce a provable blur, image down-scaling, and more.

One the most powerful aspects of RISC Zero is the ability to use your favorite libraries, and avoid reinventing the wheel.

### Get Involved

Just as the current ecosystem of amazing open-source applications is powered on amazing open-source libraries, so will be the zkVM programs you write.
And if you ever try to import a library and it doesn't work for some reason, it would be greatly appreciated it you get us know by filing an issue on [GitHub](https://github.com/risc0/risc0).

## Run this example

You can find this example in the [risc0-rust-examples GitHub repository](Understanding%20Waldo%20f60dd196187241c99aa9bdee885cea54.md). Run it yourself, and use it as a starting point to to create your own projects!
