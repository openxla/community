# RFC template and process for OpenXLA

| Status        | Proposed                                             |
:-------------- |:---------------------------------------------------- |
| **RFC #**     | [NNN](https://github.com/openxla/community/pull/NNN) |
| **Author(s)** | Jacques Pienaar (jpienaar@openxla.org)               |
| **Sponsor**   | Thea Lamkin (thealamkin@openaxla.org)                |
| **Updated**   | 2023-12-30                                           |

## Objective

Introducing a Request For Comments (RFC) process for proposing and discussing
substantial changes.

## Motivation

RFCs improves visibility and enables early engagement with proposals to inform
design. The process of creating RFCs inside OpenXLA project have been ad hoc.
This has resulted in more effort when creating a RFC, more uncertainty as to
whom reviews what, where and how (including having RFCs lag). The RFC process
and template attempts to address both of these.

The RFC process is not intended to replace the existing workflow of opening and
reviewing pull requests. The existing PR approach is fully sufficient for many
smaller changes.

This process affects all developers and community members but in particular
folks working cross components.

## User Benefit

This should both reduce uncertainty for RFC authors as well as provide a simple
structure to use. For reviewers/maintainers this should reduce mental overhead
by creating a consistent form.

For substantially larger changes (functionality, behavior, architecture), an
RFC even prior to writing any code may help with:

* Gathering and integrating feedback into a proposal from other maintainers and
  users of the component(s).
* Documenting why specific changes and decisions were made.
* Building consensus among community members.

## Design Proposal

The RFC proposal and template will be bootstrapped based on those from TensorFlow
[RFC process](https://www.tensorflow.org/community/contribute/rfc_process). We
expect the process and template may evolve based on usage and community
feedback. 

The process of creating an RFC follows as:

### Submitting an RFC

1. Before submitting an RFC, discuss your aims with project contributors and
  maintainers and get early feedback. Use the developer mailing list for the
  project concerned (openxla-discuss@openxla.org, or the list for the relevant
  component).
    
2.  Draft your RFC.
    
    * Follow the [RFC  template](https://github.com/openxla/community/blob/main/rfcs/yyyymmdd-rfc-template.md).
    * Name your RFC file `YYYYMMDD-descriptive-name.md`, where `YYYYMMDD` is the date of submission, and `descriptive-name` relates to the title of your RFC. For instance, if your RFC is titled _Parallel Widgets API_, you might use the filename `20180531-parallel-widgets.md`.
    * If you have images or other auxiliary files, create a matching directory of the form `YYYYMMDD-descriptive-name` in which to store those files.
    
    After writing the RFC draft, get feedback from maintainers and contributors before submitting it.
    
    Writing implementation code is not a requirement, but it may help design discussions.
    
3.  Recruit a sponsor.
    
    * A sponsor must be a maintainer of the project.
    * Identify the sponsor in the RFC, before posting the PR.
    
    You _may_ post an RFC without a sponsor, but if within a month of posting the PR there is still no sponsor, it will be closed.
    
4.  Submit your RFC as a pull request to [openxla/community/rfcs](https://github.com/openxla/community/tree/main/rfcs).
    
    Include the header table and the contents of the _Objective_ section in the
    comment of your pull request, using Markdown. For an example, please see [this
    example RFC](https://github.com/openxla/community/pull/5). Include the GitHub
    handles of co-authors, reviewers, and sponsors.
    
    At the top of the PR identify how long the comment period will be. This
    should be a _minimum of two weeks_ from posting the PR.
    
5.  Email the developer mailing list with a brief description, a link to the PR
    and a request for review.
    
6.  The sponsor will request a maintainer review meeting, no sooner than two
    weeks after the RFC PR is posted. If discussion is lively, wait until it has
    settled before going to review. The goal of the review meeting is to resolve
    minor issues; consensus should be reached on major issues beforehand.
    
7.  The meeting may approve the RFC, reject it, or require changes before it
    can be considered again. Approved RFCs will be merged into
    [community/rfcs](https://github.com/openxla/community/tree/main/rfcs), and
    rejected RFCs will have their PRs closed.

### RFC participants

Many people are involved in the RFC process:

* **RFC author** — one or more community members who write an RFC and are
  committed to championing it through the process.
* **RFC sponsor** — a maintainer who sponsors the RFC and will shepherd it
  through the RFC review process.
* **review committee** — a group of module maintainers who have the
  responsibility of recommending the adoption of the RFC (in rare cases, core
  maintainers would also serve this role).
* Any **community member** may help by providing feedback on whether the RFC
  will meet their needs.

A sponsor is a project maintainer responsible for ensuring the best possible
outcome of the RFC process. This includes:

* Advocating for the proposed design.
* Guiding the RFC to adhere to existing design and style conventions.
* Guiding the review committee to come to a productive consensus.
* If changes are requested by the review committee, ensure these are made and
  seek subsequent approval from the committee members.
* If the RFC moves to implementation:
  - Ensuring proposed implementation adheres to the design.
  - Coordinate with appropriate parties to successfully land implementation.

### Community members and the RFC process

The purpose of RFCs is to ensure the community is well represented and served
by new changes to OpenXLA. It is the responsibility of community members to
participate in reviewing RFCs where they have an interest in the outcome.

Community members who are interested in an RFC should:

*   **Provide feedback** as soon as possible to allow adequate time for consideration.
*   **Read RFCs** thoroughly before providing feedback.
*   Be **civil and constructive**.

### Alternatives Considered

We considered different prior art and processes, in particular from LLVM, TFX
and Swift evolution, but chose the most familiar to existing folks involved
with expectation that it may evolve with community.

### Performance Implications

N/A.

### Dependencies

N/A.

### Engineering Impact

N/A.

### Platforms and Environments

N/A.

### Best Practices

This RFC does not introduce the bar for when a change is deemed substantial. As
a rough guide a change is [substantial](https://mozac.org/rfc/0001-rfc-process) if it

* Affects multiple components;
* Affects how components interact through either their public or internal APIs;
* Fndamentally changes how a component is implemented, how it manages state or reacts to changes, in a way that isn’t self-explanatory or a direct result of a bug fix.

### Tutorials and Examples

While this RFC itself serves as an example of the RFC process, there are many other
[TensorFlow RFCs](https://github.com/tensorflow/community/tree/master/rfcs) to consult.

### Compatibility

N/A.

### User Impact

N/A.

