# Moving TSL to XLA
| Status        | Proposed                                                |
| :------------ | :------------------------------------------------------ |
| **RFC #**     | [100](https://github.com/openxla/community/pull/100) |
| **Authors** | David Dunleavy (ddunleavy@google.com) |
| **Sponsor**   | Puneith Kaul (puneith@google.com)                        |
| **Updated**   | 2023-12-12

## Objective
Move [TSL](https://github.com/google/tsl) to [XLA](https://github.com/openxla/xla).
## Proposal
TSL was originally utility and support libraries in TensorFlow needed by XLA.
Instead of moving the utility and support libraries directly to the openxla/xla repo, TSL was created anticipating
that other projects might want to move out of TensorFlow. In this case, TSL would provide common support code for
potentially many projects, not just XLA.
However, since TSL's creation over a year ago, XLA is the only direcet dependent of TSL, so we are in the process
of planning to move to TSL into XLA under the `tsl/` subdirectory.
We will use `bazel query` or similar to enforce that TSL remains independent on XLA,
such that projects who wish to depend on only TSL, but not XLA won't experience bloated binary sizes.
This work is currently planned to start in early Q1, so it would be great to hear any feedback or concerns with this
plan before January 12th, 2024.
Thanks!

