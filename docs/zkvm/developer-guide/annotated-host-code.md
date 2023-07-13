# Annotated Host Code
This page offers some annotations of RISC Zero [host] code, in order to elucidate what's happening at a line-by-line level. 
- For a more step-by-step guide to writing host code, check out our [zkVM Quick Start]. 
- To better understand what we mean by the term host, check out our [zkVM Overview]. 
- **Note**: If you're writing an application for [Bonsai], you don't need to write [host] code.
 
## A Very Simple Host
The code shown here is the `main()` function for a very simple host program. 
```
fn main() {
    let env = ExecutorEnv::builder().build().unwrap();
    let mut exec = default_executor_from_elf(env, METHOD_NAME_ELF).unwrap();
    let session = exec.run().unwrap();
    let receipt = session.prove().unwrap();
    receipt.verify(METHOD_NAME_ID.into()).unwrap();
}
```
In this example, the host: 
- constructs an [Executor] for a [guest program], 
- runs the [Executor] to construct a [session],
- [proves] the [session] to construct a [receipt], and 
- [verifies] the [receipt]. 

All of the host functionality is described in the [`risc0-zkvm` Rust crate].

## More Complex Examples
For examples of host code in applications that involve guest-host communication, check out the [factors demo] and the [JSON demo].

[Bonsai]: ../../bonsai/
[executor]: ../key-terminology.md#executor
[guest]: ../key-terminology.md#guest
[guest program]: ../key-terminology.md#guest-program
[session]: ../key-terminology.md#session
[receipt]: ../key-terminology.md#receipt
[proves]: ../key-terminology.md#validity-proof
[verifies]: ../key-terminology.md#verify
[host]: ../key-terminology.md#host
[`guest` module]: https://docs.rs/risc0-zkvm/0.16/risc0_zkvm/guest/index.html
[host]: ../key-terminology.md#host
[`risc0-zkvm` Rust crate]: https://docs.rs/risc0-zkvm/0.16/risc0_zkvm/index.html
[journal]: ../key-terminology.md#journal
[method]: ../key-terminology.md#method
[zkVM Quick Start]: ../quickstart.md
[zkVM Overview]: ../zkvm_overview.md
[factors demo]: https://github.com/risc0/risc0/tree/v0.16.0/examples/factors#step-5-host-share-two-values-with-the-guest
[JSON demo]: https://github.com/risc0/risc0/blob/main/examples/json/src/main.rs