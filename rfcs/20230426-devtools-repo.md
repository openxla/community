# RFC - Creating an openxla/dev-tools repo and building automation

(imported from https://github.com/openxla/community/issues/72)

I would like to contribute a variant of my in-progress development tools repository to the `openxla` organization: https://github.com/stellaraccident/openxla-dev-tools. I suggest simply shortening it to `dev-tools` once brought into the organization-proper.

The above represents a few hours of coding to build the boilerplate tooling that we can use for managing repositories, dependencies, and corresponding automation in the OpenXLA projects, and is a first step to helping us build workflows that bump dependencies and enable release automation.

In consultation with various folks, I concluded that a dedicated tools project was in order, and I chose to make that a cohesive python package that can be installed by anyone with a one liner. In addition, we wanted to make it straight-forward for folks (and CI) to check out individual projects and have a single script to run that would update their deps (without requiring installation of more advanced dev tooling packages like this). That way, we should be able to have a flow where advanced, cross-repo users can use this tools package as their daily driver, while people focused on a single project get exactly what they need (by being able to run `sync_deps.py` locally and always be up to date).

As an example (not yet completely refactored but to show the idea), here is a draft of the openxla-pjrt-plugin project using this tools package to manage its deps: https://github.com/openxla/openxla-pjrt-plugin/pull/29

Regardless of where we take such dev-tools and automation in the future, it seems that we definitely need a centrally accessible dev-tools project, and I therefore propose that we bootstrap it with the code I have started writing.

