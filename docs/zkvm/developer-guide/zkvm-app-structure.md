# The Structure of a RISC Zero zkVM Application
Like other virtual machine applications, a [zkVM application] consists of two components: a [host] and a [guest]. 
The [guest] contains the code to be proven. 
The [host] provides any required data to the guest, executes the guest code, and handles the guest's output. 

To start building the host and guest for your zkVM application, check out our [zkVM Quick Start] and the [`risc0-zkvm` crate].

## Directory Structure
It is possible to organize the files for these components in various ways. 
However, in the [`cargo risczero`](https://docs.rs/cargo-risczero/0.16/cargo_risczero/) starter template we use a standard directory structure for zkVM applications, and we recommend you use this structure as well. 


```
project_name
├── Cargo.toml
├── host
│   ├── Cargo.toml
│   └── src
│       └── main.rs                        <-- [Host code goes here]
└── methods
    ├── Cargo.toml
    ├── build.rs                           
    ├── guest
    │   ├── Cargo.toml
    │   └── src
    │       └── bin
    │           └── method_name.rs         <-- [Guest code goes here]
    └── src
        └── lib.rs                       
```

To learn more about the structure of a zkVM application, check out our [Annotated guest code].

[Annotated guest code]: ./annotated-guest-code.md
[guest]: ../key-terminology.md#guest
[host]: ../key-terminology.md#host
[zkVM Quick Start]: ../quickstart
[`risc0-zkvm` crate]: https://docs.rs/risc0-zkvm/0.16/risc0_zkvm/guest/index.html
[zkVM application]: ../zkvm_overview.md

