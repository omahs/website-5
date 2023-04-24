---
slug: lisbon
title: Reflection on ZK Hack & ZK Summit 
authors: [paul]
tags: [zkhack, zksummit, lisbon]
---

First off: huge thanks to all the organizers and participants at ZK Hack & ZK Summit!
Both events were fantastic; I'm already looking forward to next time. 

Now that the jetlag is behind me, I wanted to share some zero-knowledge research threads that I'm excited to keep thinking about and talking about. 

## Folding Schemes: Nova, Supernova, and Sangria
[Video Reference](https://www.youtube.com/watch?v=D7rQbHpxl7Q) <br/>
[Blog Reference](https://geometry.xyz/notebook/sangria-a-folding-scheme-for-plonk)

This is perhaps the most important emerging idea in zk research right now. 
These schemes achieve Incrementally Verifiable Computation (IVC) by *combining instances that haven't been proven*. 
This contrasts with the more familiar approach of proving each instance and then rolling up the results. 

Nova introduced a technique for combining R1CS instances. 
Supernova generalized Nova to support arbitrary instruction sets. 
Sangria uses the same technique in order to combine (relaxed) PLONK instances. 

A natural research question arises: can we apply this approach to AIR-FRI STARKs? 
The answer isn't obvious, as this technique depends on a homomorphic encryption scheme such as KZG. 

## The Red Wedding 
[Video Reference](https://www.youtube.com/watch?v=O1puSvcwAps) <br/>

This idea, proposed by the team behind [TritonVM](https://triton-vm.org/), aims to reduce the verification time (and thus, the recursion time) in a STARK system by shifting work from the Verifier to the Prover. 
Specifically, the Prover can generate a SNARK proof in order to alleviate the need for the Verifier to evaluate the AIR constraints at the DEEP query point. 

Some research questions:
- How does the computational cost of the inner SNARK verification compare to the cost of the AIR evaluation that it aims to replace? 
- What commitment scheme should be used for this inner SNARK? 
- What's the right scope for the SNARK verification? Should it include arithmetic or hashing operations in addition to the AIR constraint evaluation? 

## LogUp: Batched Lookup Arguments
[Video Reference](https://www.youtube.com/watch?v=qv_5dF2_C4g) <br/>
[ePrint Reference](https://eprint.iacr.org/2022/1530.pdf)

In contexts where the Prover is repeatedly doing the same lookup, LogUp reduces the number of columns necessary in lookup tables by ~50%, relative to PLOOKUP.
About 30% of the witness-generation in RISC Zero is spent generating columns for a PLOOKUP-based lookup argument; we're looking into switching to LogUp for future versions. 

The premise here is that by making use of logarithmic derivatives, we can transform a grand product accumulation into a (cheaper) grand sum accumulation. 
The LogUp paper (linked above) frames this technique in terms of a multivariate IOP; the [Tip5 paper](https://eprint.iacr.org/2023/107.pdf) describes a version of this technique that's better suited to the univariate context. 


## The Mersenne Prime $2^{31}-1$
[Video Reference](https://www.youtube.com/watch?v=giFA3UXbu_s&t=305s) <br/>
[Slides](https://drive.google.com/file/d/1JaoqFUARyUXuaz4PBUG0R64_Yuzc5O-_/view?usp=sharing)

In Denver last month, Daniel Lubarov discussed the idea of using the finite field of order $2^{31} - 1$ for building Plonky3.
This field is particularly nice for handling finite field arithmetic, since $2^{31} = 1$. 
The major obstacle is that the multiplicative group of this field isn't good for NTTs, since $2^{31} - 2$ doesn't have many 2s in its prime factorization. 

There are a number of options for how to make this work: 
- changing from a FRI-based commitment scheme to one based on [Orion](https://eprint.iacr.org/2022/1010.pdf) or [Brakedown](https://eprint.iacr.org/2021/1043.pdf)
- using a mixed-radix version of FRI that doesn't depend on high 2-adicity
- doing NTTs in a quadratic extension field (note that the multiplicative group of the quadratic extension has order $2^{62} - 2^{32}$ and therefore has 2-adicity of $2^{32}$)

Looking forward to seeing what the Polygon Zero team is brewing up on this front. 

## Don't be a Stranger!
We'd love to hear what you're thinking about, in regards to these questions or otherwise. Continue the conversation on Discord at [ZKHack](https://discord.gg/KprSfyTDvt) or [RISC Zero](https://discord.gg/risczero). 
