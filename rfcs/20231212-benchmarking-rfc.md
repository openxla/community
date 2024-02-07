# OpenXLA Benchmarking
| Status        | Proposed                                                |
| :------------ | :------------------------------------------------------ |
| **RFC #**     | [101](https://github.com/openxla/community/pull/101) |
| **Authors** | David Dunleavy (ddunleavy@google.com) |
| **Sponsor**   | Puneith Kaul (puneith@google.com)                        |
| **Updated**   | 2023-12-12

## Objective
Gather feedback on what benchmarking infrastructure would be helpful for the OpenXLA community.

## Proposal
Previous benchmarking efforts like those described in the
[Benchmarking Strategy RFC](https://github.com/openxla/community/blob/main/rfcs/20230505-benchmarking-strategy.md)
have been disrupted due to changes in broader strategy in the OpenXLA ecosystem.
Since then, there have been some independent discussions about benchmarking for XLA,
but we are interested in getting a pulse on what's most important to the community.

## Questions
What openly available models are most interesting to measure?
Is using models in HLO/StableHLO form sufficient? Or is it preferable to do framework level benchmarks?
What backends/targets/configurations are most important to benchmark? Single vs multi-host?
