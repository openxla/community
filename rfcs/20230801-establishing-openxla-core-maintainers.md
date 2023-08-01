# RFC: Establishing OpenXLA Core Maintainers

**Authors:** Thea Lamkin, Eugene Burmako, Jaques Pienaar, Stephan Herhut

**Last updated:** 2023-08-01

## Background

Earlier this year, we established the
[OpenXLA Interim Steering Committee](https://github.com/openxla/community/blob/main/governance/INTERIM-STEERING-COMMITTEE.md),
whose primary role was to bootstrap
[OpenXLA Governance](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md)
and work to establish OpenXLA's first group of Core Maintainers.

For more context on OpenXLA's project hierarchy, see
"[Hierarchical Structure](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#hierarchical-structure)"
in project governance.

## Goals

In our proposal for an initial set of Core Maintainers, we are hoping to fulfill
the following goals:

*   Provide continuity to OpenXLA OSS community leadership
*   Follow OpenXLA Governance guidelines for Core Maintainer roles &
    responsibilities (see
    [Core Maintainers](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#core-maintainers))
*   Follow OpenXLA Governance guidelines for Core Maintainer criteria of having
    a demonstrated track record of OSS contributions in multiple areas of the
    OpenXLA project and "strong and continued alignment with the overall OpenXLA
    principles". (see
    [Core Maintainers](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#core-maintainers)
    and Maintainer
    [Principles](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#the-principles))
*   Achieve representation from contributors from all major components in the
    OpenXLA project
*   Make incremental steps towards organizational diversity in the Core
    Maintainer group

## Proposed Members

We propose to largely pull from the existing membership of the OpenXLA Interim
Steering Committee, with additional member(s) from outside Google.
[Previous members](https://github.com/openxla/community/blob/main/governance/INTERIM-STEERING-COMMITTEE.md#committee-members)
of the OpenXLA Interim Steering Committee not represented below have elected not
to move forward as OpenXLA Core Maintainers.

Member          | GitHub     | Role
--------------- | ---------- | --------------------
Eugene Burmako  | burmako    | Core Maintainer
Jacques Pienaar | jpienaar   | Lead Core Maintainer
Mehdi Amini     | joker-eph  | Core Maintainer
Stephan Herhut  | sherhut    | Core Maintainer
Thea Lamkin     | theadactyl | Core Maintainer

### Additional Notes on Core Maintainer Membership

We recognize that the proposed set of Core Maintainers are primarily from
Google. This is a natural reflection of the criteria that OpenXLA Maintainers
have demonstrated sustained upstream contributions to and expertise in OpenXLA
project components, and that Core Maintainers have additionally demonstrated
broad contributions to project health beyond individual components.

If there are individuals who should be considered for membership in this group,
please provide recommendations below with the information outlined in the
OpenXLA Governance
[nomination guidelines](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#core-maintainers).

It is our goal to grow the diversity of the Core Maintainer group over time by
providing clear paths and opportunities for project leadership and mentorship.
We believe there will be additional opportunities for leadership from multiple
organizations at the Module Maintainer level, where membership criteria are
specific to contributions to and expertise in individual OpenXLA components. As
defined by OpenXLA Governance, most technical decision-making should happen at
the
[Module Maintainer](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#module-maintainers)
level, and escalation to Core Maintainers from the module level should be the
exception.

## In-scope responsibilities

The high-level role of the Core Maintainers is to fulfill the group's
responsibilities and decision-making mechanisms outlined in OpenXLA Governance
(see
[Core Maintainers](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#core-maintainers)).
Given that these are abstract, and particular governance mechanisms are yet to
be defined, this first set of Core Maintainers should work to charter and
establish clear responsibilities and processes. (Eg, there are many TODOs in the
governance model that should be resolved.)

Examples of responsibilities and governance processes that need further
definition:

*   Establishing module maintainer governance
*   Nomination, election, and tenure process for Core and Module Maintainers
*   RFC / design review process
*   Escalation process
*   Code of Conduct and process
*   General contribution guidelines
*   OpenXLA development & design principles

## Delegated responsibilities

As previously established in GitHub Organization Management
([RFC 80](https://github.com/openxla/community/pull/80)), the OpenXLA Core
Maintainers delegate GitHub Organization management, and "GitHub Owners" roles,
to Google employees as required by Google's internal policies. This
responsibility will revert to the Core Maintainer group when the OpenXLA GitHub
organization is no longer owned and administered by Google. To the furthest
extent possible under Google GitHub policy, OpenXLA GitHub Owners will align
OpenXLA GitHub roles and access policy to the OpenXLA Governance model.

The Core Maintainers may identify additional delegate responsibilities as they
see fit.

## Mechanisms for transparency

Core Maintainers will follow OpenXLA Governance guidelines on
[Transparency](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#transparency)
and Core Maintainer
[decision-making](https://github.com/openxla/community/blob/main/governance/GOVERNANCE.md#transparency):

```
"The Core Maintainers should publicly articulate their decision-making, and
give a clear reasoning for their decisions, vetoes and dispute resolution."
```

Additional mechanisms for transparency are yet to be defined as part of the
OpenXLA Core Maintainers charter. In the interim, all decisions made by the Core
Maintainers impacting project governance should be accompanied by
publicly-shared documentation, rationale, and RFCs.

## Next steps

This RFC will be open for comment by the community until August 14, 2023. Any
community feedback will be incorporated or resolved with clear rationale from
the OpenXLA Interim Steering Committee.

Once established, OpenXLA Core Maintainers should promptly move to propose RFCs
for Module governance and a Core Maintainer charter.
