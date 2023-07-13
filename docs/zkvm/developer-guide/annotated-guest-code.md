# Annotated Guest Code
This page offers some annotations of RISC Zero [guest code], in order to elucidate what's happening at a line-by-line level. 
- For a more step-by-step guide to writing guest code, check out our [zkVM Quick Start]. 
- To better understand what we mean by the term guest code, check out our [zkVM Overview]. 
 
## The Simplest Possible Guest
The code shown here is the simplest possible guest code; its guest [method] does nothing:
```
#![no_std]
#![no_main]
risc0_zkvm::guest::entry!(main);
pub fn main() {
    // TODO: Implement your guest code here
}
```

## Line-by-line Analysis
Let's see what each of these lines does.


`#![no_std]` <br/>
The guest code should be as lightweight as possible for performance reasons. So, since we aren't using `std`, we exclude it.
<br/>

`#![no_main]` <br/>
The guest code is never launched as a standalone Rust executable, so we specify `#![no_main]`.
<br/>

`risc0_zkvm_guest::entry!(main);` <br/>
We must make the guest code available for the host to launch, and to do that we must specify which function to call when the host starts executing this guest code. We use the `risc0_zkvm_guest::entry!` macro to indicate the initial guest function to call, which in this case is `main`.
<br/>

`pub fn main(){ }` <br/>
Here is the where we put the actual guest code. 
Notice that the function is named `main`, matching the name specified in `entry!`, so this is the function that will be called when the host launches the guest. 
In real use cases, you would do more than nothing in this function.

## Other Important Functions
- The `env::read`, `env::read_slice`, and `env::stdin` commands are used to read input data to the guest (from the host). 
- The `env::write`, `env::write_slice`, `env::stdout`, and `env::stderr` commands are used to write output data from the guest to the host.
- The `env::commit` and `env::commit_slice` commands are used to write output data from the guest to the [journal].

All of the guest functionality is described in the [`guest` module] of the [`risc0-zkvm` Rust crate].

## A Slightly More Complex Example
To see guest code for a zkVM application that involves host-guest communication and journal commitments, check out the [factors demo], where the [guest] receives two inputs from the [host] and commits their product to the [journal].

[guest]: ../key-terminology.md#guest
[guest code]: ../key-terminology.md#guest
[`guest` module]: https://docs.rs/risc0-zkvm/0.16/risc0_zkvm/guest/index.html
[host]: ../key-terminology.md#host
[`risc0-zkvm` Rust crate]: https://docs.rs/risc0-zkvm/0.16/risc0_zkvm/index.html
[journal]: ../key-terminology.md#journal
[method]: ../key-terminology.md#method
[zkVM Quick Start]: ../quickstart.md
[zkVM Overview]: ../zkvm_overview.md
[factors demo]: https://github.com/risc0/risc0/tree/v0.16.0/examples/factors#step-6-guest-multiply-two-values-and-commit-their-result