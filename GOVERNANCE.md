# OpenXLA Governance

Our governance process is heavily influenced by the great work done at formalizing these mechanism by other existing projects like PyTorch and Carbon, as well as our experience with the LLVM culture. The structure we adopt is inspired from the PyTorch governance model.

This document introduces the core values that underlie our project governance, before defining the main governance rules we use to make decisions. This document does not go into the details of the process associated with every change (for example how to write and RFC, where to post it, how to get it approved, etc). The Contribution Guide (TODO) describes how we develop the project and how we handle contributions. The remainder of the current document defines how we organize governance instances.

## Core Values

An open, inclusive process for OpenXLA changes. The community needs to be able to effectively engage in the direction and evolution of the project and language, while keeping the process efficient and effective. That means we need an open, inclusive process where everyone feels comfortable participating. Community members should understand how and why decisions are made, and have the ability to both influence them before they occur and give feedback afterward. We want to use this process to also ensure we stick to our project goals and have clear rationales for all of our technical designs and decisions.

Being inclusive is different from including everyone. We want to avoid excluding or marginalizing members of the community. However, project leaders will inevitably make choices that are desired by some OpenXLA community members more than others. Maintainers will provide justification for these decisions, but achieving OpenXLA's goals -- including that of a healthy community -- will be the guiding rule.

### Equal footing

OpenXLA is a community driven project: everyone can get involved, contribute and impact the project. This includes people working on OpenXLA across a wide range of companies as their full time job, but also people contributing in small fractions of their time, or as students, teachers, or as a hobby.

People are recognized for their contributions, and maintainer positions are associated with individuals, regardless of affiliation. That is, there are no seats reserved for specific companies, and membership is associated with the person rather than the company employing that person.

### Code of Conduct

The community and project needs a code of conduct. We want OpenXLA’s community to be welcoming and respectful, with a deep commitment to psychological safety. We need consistent expectations for how every community member should behave, regardless of their position in the community. These expectations around conduct and behavior need to be clearly articulated both to set expectations for people joining, and to help remind and anchor us to consistent standards. It is also important that we hold ourselves accountable to these expectations and have real and meaningful mechanisms to moderate the community. There should be clear mechanisms for reporting behavior that does not meet our community expectations, consistent processes for addressing these reports, eg via a committee responsible for handling Code of Conduct, and documented consequences for Code of Conduct violations.

### Consensus-driven decision

OpenXLA favors a consensus-driven approach to development. Contributors are expected to engage in discussions and attempt to resolve all blockers raised by other contributors, either through RFCs or during code reviews discussions. We are using blocking consensus to ensure “equal footing” and to act as a forcing-function to keep the community whole.

Consensus is employed by many other projects, some like LLVM don’t define a structure around it and operate like a do-ocracy. We recognize that there are limits to consensus with respect to scaling a project, and as such we also adopt a technical governance structure that is hierarchical. This will:
- avoid ambiguity about who must be involved in a consensus-based decision,
- ensure that groups size remain limited,
- provide escalation paths in the rare cases a blocking situation can’t be resolved by a group. 

Our Contribution Guide(TODO) defines the expectation around blocking a decision.

###  Transparency

We will explain why and how we make decisions, and as such decisions are public with the rationale for that decision documented.

## Hierarchical Structure

We distinguish between the following levels of decision making:

* A community of **contributors** who file issues, make pull requests, proposals, and contribute to the project.
* A small set of **Module Maintainers** drive each module of the OpenXLA project.
* They are overseen by **Core Maintainers**, who drive the overall project direction.
* The Core maintainers have a **Lead Core Maintainer** who is the catch-all decision maker.

All maintainers are expected to have a strong bias towards OpenXLA’s design philosophy(TODO). All decisions taken at any of these levels are expected to be clearly motivated and explained publicly.

Beyond the maintainers, the community as a whole is encouraged to contribute code and documentation, file issues, make proposals, review pull requests and be present in the community. Given contributions and willingness to invest effort, anyone can be accepted as a maintainer and own parts of the codebase.

Technical governance is strictly separated from business governance. Membership in the technical governance process is for **individuals**, not companies. That is, there are no seats reserved for specific companies, and membership is associated with the person rather than the company employing that person.

## Module Maintainers

Modules are defined as GitHub repositories within the OpenXLA org, or as well-identified directories within the core repository `openxla/xla`.

Each module will have its own group of maintainers, who are responsible for reviewing and approving commits, improving design, and refining the scope of the module. Module maintainers decide on each particular issue brought to them based on a blocking consensus. 

In cases where a group of Module Maintainers cannot come to a conclusion themselves, at least one Core Maintainer is selected by the Core Maintainers using the process described in the "Core Maintainers" section to act as facilitator and help drive a path towards a consensus resolution between the Module Maintainers. In the exceptional case where no consensus can be reached, the issue is escalated to the group of Core maintainers for decision making.

Other responsibilities of the Module Maintainers includes:
* Triaging issues of the module and assigning priorities.
* Triaging and reviewing and landing pull requests of the module.
* Supporting public documentation related to the module
* Running public developer meetings (if any)
* Providing quarterly and yearly plans for inclusion in the overall 
OpenXLA roadmap(TODO)

## Core Maintainers

The Core Maintainers are expected to have a deep understanding of the OpenXLA code base and design philosophies. Their responsibilities include:

* Articulating a cohesive long-term vision for the project
* Negotiating and resolving contentious issues in ways acceptable to all parties involved
* Receiving broad requests for changes from stakeholders of OpenXLA and evaluating / accepting them (small module-level requests are handled by Module Maintainers)
* Confirm or remove Core Maintainers.

The Core Maintainers as a group have the power to veto any decision made at a Module Maintainer level. The Core maintainers have power to resolve disputes as they see fit.
The Core Maintainers should publicly articulate their decision-making, and give a clear reasoning for their decisions, vetoes and dispute resolution. The decision from the Core Maintainers are done using a blocking consensus.

## Lead Core Maintainer

There may be decisions in which the Core Maintainers cannot come to a consensus. To make such difficult decisions, the Core Maintainers elects a publicly declared Lead Core Maintainer (LCM) amongst them.

The LCM should publicly articulate their decision-making, and provide a documented rationale for their decisions. In practice, we expect the LCM to play a central role seeking consensus amongst the Core Maintainers so that ideally it never comes to a LCM decision.

## Nominating, Confirming and Removing Maintainers

### The Principles

* Membership in module maintainer groups is given to **individuals** on **merit basis** after they demonstrated strong expertise of the component through contributions, reviews and discussions and are aligned with how the component fits in the overall project direction.
* For membership in the Core Maintainer group the individual has to demonstrate strong and continued alignment with the overall OpenXLA principles.
* Membership is yearly (TBD) for each position (Module Maintainers or Core Maintainers)
* Light criteria of moving module maintenance to ‘emeritus’ status if they don’t actively participate over long periods of time. Emeritus status is granted by the Core Maintainers based on the proposal of any community member.
* The membership is for an individual, not a company.

### The Process for Nomination

Each module will follow OpenXLA's central guidelines (TODO) on how to apply for nomination, but can add additional criteria at the module level. The existing Module Maintainers decide on the nomination for a particular module like they decide on any other issue. In the absence of published point of contact for a module, you can contact the Core Maintainers group (TODO).

Nomination requests should include the following items:

  * The nominees depth and breadth of code, review and design contributions on the module
  * At least 3 contacts of existing contributors or maintainers that would support the nomination.

The Module Maintainers then evaluate all information and make a decision to Confirm or Decline the nomination. The decision will be made public with documented rationale.

### The Process for Removal

* Similar to the process for nomination, anyone in the community can nominate a person to be removed from a Module Maintainer position or a Core Maintainer position.
* A person may self-nominate to be removed.
* The Core Maintainers (excluding persons with a conflict of interest) will request or put together more information around the following:

  * Their activity (or lack of) on the project
  * Their changing thinking of the space, which results in
    conflict with the overall direction of the project
  * Other information that makes them unfit to be a maintainer,
    such as Code of Conduct issues, their activity outside the
    scope of the project that conflicts with the project’s values
  * **Conflicts of interest**: see "Conflicts of Interest" below

* The Core Maintainers then evaluate all information and make a final decision to Confirm or Decline the removal. The decision will be made public with a documented rationale.

### Nominating Core Maintainers

The lead maintainer requests or puts together more information around the strength of the candidate to be a Core Maintainer:

  * Statement of support from other Core and Module Maintainers
  * General statement of support from stakeholders within the
    OpenXLA community
  * Any new relevant information that is befitting for the candidacy

The Core Maintainers are responsible for evaluating the Nomination, with a clear public articulation of their reasoning behind the decision.

### Removing the Lead Core Maintainer and Nominating a New Lead Core Maintainer

* A super-majority of Core Maintainers (75%) can choose to
  remove the Lead Core Maintainer before their term.
* After a removal of the Lead Core Maintainer or in unforeseen
  circumstances (such as permanent unavailability of the Lead Core
  Maintainer), the Core Maintainers follow a Ranked-Choice voting
  method to elect a new Lead Core Maintainer.
* The Lead Core Maintainer is nominated for a 1 year term (TBC).

### Add, Remove, and Re-Scope Modules and Projects

The Core Maintainers together are responsible for taking decisions on adding, removing and re-scoping new modules in the OpenXLA org, either as new repositories in the OpenXLA GitHub org, or by scoping new or existing folders in the [openxla/xla](https://github.com/openxla/xla) repository.

They invite proposals from members in the community (including themselves) for such changes.
The proposals are open-ended, but should have some basic ground-work to make a convincing case for change. The following is an example approach to this process:

* Interview contributors / stakeholders, talk to community, gather issues;
* Read papers, attend conferences, build example pipelines based on experience;
* Create a state of the world - make sure this change is necessary,
   for example adding a new project or module is worth the maintenance
   cost; or removing a project or module will not remove too much value
   from OpenXLA;
* Create a proposal; the proposal covers the maintainership, development
   and community plan once the proposal is approved.

The Core Maintainers take final decisions on the proposal, articulating the reasoning behind the decision publicly.

## Other governing bodies

It is important that there are also pathways to project leadership for non-code contributors, whether through representation in the Core Maintainers or in groups scoped to non-code areas of the project. Furthermore, in addition to technical oversight groups, the project may need separate bodies to lead areas of the project, such as:

* Project governance
* Code of conduct enforcement 
* Trademark policy 
* Marketing & community management 
* Infrastructure, testing, & release 

When instituting additional governing bodies, care should be taken to preserve clear processes for technical and non-technical decision-making, and avoid creating project areas where governing bodies have unclear or overlapping responsibilities.

TBD: What group approves creation of additional governance bodies. 


## Conflicts of interest

In any open source project where many contributors are sponsored by their employers, conflicts of interest are bound to arise. In most situations, disclosures of employment and business relationships are encouraged/expected and should be sufficient. However, any Maintainer should recuse themselves from decisions where they are acting within their responsibility as a Core or Module Maintainer AND they have a conflict of interest that would compromise the legitimacy of that particular decision. 

These conflicts of interest may arise in decisions impacted by:

1. Personal relationships - Maintainer has a romantic or familial relationship with involved party
2. Escalation process - Maintainer is an involved party to an escalation being brought to Maintainers for resolution
3. Competitive advantage - Maintainer or their employer/organzation's competing commercial product or open source project stands to gain in a project decision at the expense of the OpenXLA project

Potential conflicts of interest should be clearly defined by the project community, with expected processes for disclosure and recusal. Consequences for failure to disclose COIs and follow the recusal process will be covered under the project Code of Conduct. 


## FAQ


**Q: What if I would like to own (or partly own) a part of the project such as a feature area or domain library, for example**  [FOO]() **or** [BAR]() **?**

This is absolutely possible. The first step is to start contributing to the existing project area and
supporting its health and success. In addition to this, you can make a proposal through a GitHub issue for new functionality or changes to improve the project area.

**Q: What if I am a company looking to use OpenXLA internally for development, can I be granted or purchase a board seat to drive the project direction?** 

No, the OpenXLA project is strictly driven by a maintainer project philosophy and clearly separates technical governance from business governance. You can however empower your engineers to invest their time in OpenXLA, becoming important contributors and ultimately becoming maintainers, but this is not guaranteed and is merit-based.

**Q: Does the OpenXLA project support grants or ways to support independent developers using or contributing to the project?** 

No, however companies involved in OpenXLA may be interested to contract work, please reach out on the OpenXLA forums to discuss.

**Q: How do I contribute code to the project?** 

If the change is relatively minor, a pull request on GitHub can be opened up immediately for review and merged by the project committers. For larger changes, please open an issue to make a proposal to discuss prior. Please also see the [Contributions Guide](TODO) for contribution guidelines. 

**Q: Can I become a committer on the project?** 

All contributions are going through pull requests and approved by maintainers. At the moment, the process for landing a pull request into OpenXLA varies with the exact repository. For example StableHLO is purely developed on GitHub and a pull request can be merged through the GitHub UI. On the other hand, the XLA compiler repository involves an interaction with Google internal infrastructure that can only be triggered by Google employees who will play the janitorial role of ensuring prompt merging after approval.

**Q: What if I would like to deliver a OpenXLA tutorial at a conference or otherwise? Do I need to be 'officially' a maintainer to do this?** 

No, we encourage community members to showcase their work wherever and whenever they can.

**Q: What are the conditions to reuse the OpenXLA logo?** TODO
