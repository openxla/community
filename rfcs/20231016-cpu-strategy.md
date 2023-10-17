# OpenXLA CPU Strategy

| Status        | Proposed                                                |
| :------------ | :------------------------------------------------------ |
| **RFC #**     | TBD |
| **Authors** | Matt Walsh (walshmatt@google.com), Eugene Zhulenev (ezhulenev@google.com), Penporn Koanantakool (penporn@google.com), Benjamin Kramer (kramerb@google.com), Sara Smoot (sarasmoot@google.com)  |
| **Sponsor**   | Andrew Leaver (andrewleaver@google.com)                        |
| **Updated**   | 2023-10-16

## Objective

OpenXLA CPU, in cooperation with extensions that the community can effectively use with it, performs well for the majority of DNN workloads on common CPU architectures.

## Proposal

In order to achieve the objective we would like to:
* Adopt XLA:CPU (sometimes known as “XLA CPU:Current”) as-is to be the basis for OpenXLA CPU and gradually evolve it to address performance disadvantages and integration inconveniences.
* Potentially incrementally adopt desirable features from our companion compilers (e.g. IREE)
* Improve our MLIR infrastructure through a MLIR integration point and potentially MLIR-ify some of our passes, particularly those that come ahead of said integration point
* Increase GPU & CPU compiler infrastructure unification as much as possible.

More specifically, this RFC proposes these changes to XLA:CPU:
* Improving direct (in-tree) integration with state-of-the-art 3rd-party (3P) libraries – most commonly but not exclusively from hardware vendors.
* Enabling plugging in a codegen toolchain and 3P library-based implementation through a stable ABI.
* Adopting XLA:GPU’s runtime components: Thunks++ as the runtime and StreamExecutor as the HAL.
* Implementing cost-model-based operation fusion heuristics, similar to XLA:GPU.  We are referencing, but not specifying this aspect here as it is being developed and will be covered in detail in its own RFC.  There is a hope and intention that the CPU compiler will be able to take advantage of this “for free” building on top of the primary GPU uses.  

## Detailed Design

Please refer to this public [Google Document](https://docs.google.com/document/d/1ZzMcrjxITJeN2IjjgbzUjHh-4W1YgDUus3j25Dvn9ng/edit?usp=sharing).
