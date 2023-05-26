# RFC - Creating an openxla-compiler-release repository

We are starting to assemble the minimal set of components that make up the
fully instantiated, new OpenXLA Compiler. To date, we have largely been
focused on bootstrapping the individual components, but it is time to start
working towards releasing them as a unit.

This RFC proposes that we create a new, capstone GitHub project
`openxla-compiler-release` which depends on all included component repositories,
contains release scripts/automation, and produces authoritative binaries
which can be subjected to more rigorous testing and release.

Since we will be aggregating multiple components and processes, the following
RFCs and issues can be a reference:

* [OpenXLA PJRT Plugin](https://github.com/openxla/community/blob/main/rfcs/20230123-pjrt-plugin.md): Described the PJRT Plugin API and proposed
creation of the [openxla-pjrt-plugin](https://github.com/openxla/openxla-pjrt-plugin)
repository. This plugin has been implemented for CPU/CUDA on top of the IREE
compiler and runtime API and has been integrated with Jax.
* [IREE RFC to create a compiler plugin mechanism](https://github.com/openxla/iree/issues/12520): Created a facility for extending the compiler with in/out of tree,
standalone plugins.
* [Creation of the openxla-nvgpu project](https://github.com/openxla/community/blob/main/rfcs/20230327-nvgpu-repo.md): Created the [openxla-nvgpu](https://github.com/openxla/openxla-nvgpu) project, consisting of compiler/runtime plugins enabling interop
with various NVIDIA libraries (cuDNN, cuBLAS, etc) and Triton on NVIDIA GPUs.
* [Creation of the openxla-devtools project](https://github.com/openxla/community/blob/main/rfcs/20230426-devtools-repo.md): The [openxla-devtools](https://github.com/openxla/openxla-devtools) repository contains pip installable development tools for
managing OpenXLA project, bumping dependencies, etc. It has been used for the
last month to automate the dependency and release management of the
[openxla-pjrt-plugin](https://github.com/openxla/openxla-pjrt-plugin) project,
and it has begun to be used on the [openxla-nvgpu](https://github.com/openxla/openxla-nvgpu) as we instantiate its CI and release process.
* [Isolation of the HLO partitioner](https://github.com/openxla/openxla-pjrt-plugin/issues/82): A standalone CLI, C and Python API have been created to house the
existing HLO partitioner and adapt it to operate on StableHLO. A future
evolution of this is planned to provide the container for an as-yet to be
developed global HLO cost model and optimizer pipeline that can be re-used by
the various projects in the OpenXLA umbrella (we will likely rename this to
the `OpenXLA Optimizer` to accomodate this expansion of role). This is presently
maintained in the [partitioner/](https://github.com/openxla/openxla-pjrt-plugin/tree/main/partitioner) directory of the `openxla-pjrt-plugin` project, and it is
integrated into the plugin as an optimizing pre-processor.

As envisioned in the overall OpenXLA Compiler architecture, these components
provide a minimum set of functionality needed to instantiate an industrial
strength AOT/JIT compiler, supporting framework interface infrastructure,
and testing facilities for using the OpenXLA Compiler in an optimized
configuration on NVIDIA GPUs and a variety of CPU targets.

## Architecture Diagram

TODO: Enlist the help of someone who is competent with visuals to draw a new
diagram that illustrates the relationships:

* `openxla-compiler-release` project taking a transitive dependency on:
  * Version stabilized set of compiler components:
    * `iree` (`libIREECompiler.so`)
    * `openxla-nvgpu` (various `--iree-plugin=` compiler plugins linked into
      the compiler).
    * `openxla-optimizer` (nee `openxla-partitioner`)
      (`libOpenXLAOptimizer.so`).
  * Note that this represents a promise for the project to produce multi-target
    compiler binaries that include all supported/committed plugins (of which
    `openxla-nvgpu` is the first).
  * We do not call out the criteria for inclusion of compiler plugins into
    the default compiler release, but there needs to be some support and
    continuity guarantee made to the overall organization.
  * Versioned set of runtime components (for compiler features that require
    a runtime component):
    * `iree` runtime
    * `openxla-nvgpu cuDNN` runtime dylib
    * `openxla-nvgpu cuBLAS` runtime dylib
    * `openxla-nvgpu triton-jit` runtime dylib (does not yet exist: for
      example).
  * Framework plugins provided via tha `openxla-pjrt-plugin` project, with
    individual plugins exported as Python packages (e.g.
    [openxla_cpu_plugin](https://github.com/openxla/openxla-pjrt-plugin/tree/main/python_packages/openxla_cpu_plugin) and [openxla-cuda-plugin](https://github.com/openxla/openxla-pjrt-plugin/tree/main/python_packages/openxla_cuda_plugin)).
  * Framework PJRT plugins dynamically load an appropriate compiler dylib,
    optimizer dylib, and runtime extension dylibs, exporting sensible defaults
    and various configuration mechanisms to tweak or activate different feature
    sets.

Note that the above mostly exists today with some forward looking renames and
alterations made to signal near term direction.

## Packages

An OpenXLA Compiler release will consist of a number of packages. In most cases,
these are derived/augmented from component specific packages but configured
with global version and dependency metadata. Specifics are likely to change
as the project evolves, and the following represent what we can see as likely
for a 2023 end state.

### Python Packages

* `openxla-compiler`: Main Python package of the compiler. This is a
  re-packaging/extension of the more elemental `iree-compiler` with the
  following changes:
    * Exposes Python interfaces for all OpenXLA supported dialects.
    * Lives in the namespace `openxla.compiler`.
    * Embeds compiler binaries that link all supported OpenXLA organizational
      compiler plugins that are qualified for release (i.e. it can multi-target
      to the full set of targets and extensions that are deemed release-quality
      in the OpenXLA org).
    * Can contain additional tooling relevant to overall OpenXLA use cases.
* `openxla-optimizer`: Shared library and
[ctypes Python API](https://github.com/openxla/openxla-pjrt-plugin/tree/main/partitioner/bindings/python) API for integrating the OpenXLA optimizer into larger
assemblies.
* [`openxla-pjrt-plugin-cpu`](https://github.com/openxla/openxla-pjrt-plugin/blob/main/python_packages/openxla_cpu_plugin/setup.py):
PJRT plugin bringing together the OpenXLA CPU compiler, OpenXLA optimizer and
generic runtime support.
* [`openxla-pjrt-plugin-cuda`](https://github.com/openxla/openxla-pjrt-plugin/blob/main/python_packages/openxla_cuda_plugin/setup.py):
PJRT plugin bringing together the OpenXLA CUDA compiler, OpenXLA optimizer,
supported compiler plugins and facilities to activate supported CUDA runtime
components.
* [`openxla-runtime-plugin-cudnn`](https://github.com/openxla/openxla-nvgpu/tree/main/runtime/src/openxla/runtime/nvgpu/cudnn):
cuDNN runtime extensions (can be loaded/activated by the `openxla-pjrt-plugin-cuda`).
* [`openxla-runtime-plugin-cublas`](https://github.com/openxla/openxla-nvgpu/tree/main/runtime/src/openxla/runtime/nvgpu/cublas):
cuBLAS and adjecent runtime extensions (can be loaded/activated by the `openxla-pjrt-plugin-cuda`).
* `openxla-runtime-plugin-triton-jit`: Runtime plugin for Triton based
JIT/auto-tuning (does not yet exist).

We will also release some component specific packages that are intended
for more limited audiences but are useful to keep in version lock with the
overall release flow.

* `iree-compiler`: Elemental IREE compiler which only contains support for
  pure compiler based targets and essential tooling. This is released as a
  convenience to lower level integrators.
* `iree-runtime`: Elemental IREE runtime components and tooling, which can be
  used for various development and deployment activities in AOT settings.

### Source and development packages

We will also release source and development packages for the low level
compiler and runtime (i.e. headers, libraries, etc) as needed.

## Versioning

We will adopt a standard semver (`MAJOR`.`MINOR`.`PATCH`) scheme with a typical
Python aligned `.devYYYYMMDDBBB` style suffix for pre-release packages. All
packages will have embedded version information, queryable from APIs, and
Python packages will also embed their source and revision map for easy
correlation with sources.

For compatibility with existing flows, we will maintain a checked in
[`version_info.json`](https://github.com/openxla/iree/blob/31900d956ba93ca05f4ee58936c6b51769e10837/.github/workflows/build_package.yml#L91)
in the `openxla-compiler-release` repository. Release flows will be
conditioned to either produce a regular release with the exact version info
or a pre-release with an appropriate `.dev*` suffix. At HEAD the checked in
`version_info.json` will always be for the next official version. Each
officially cut official version will have a corresponding tag and release
in the repository.

Pre-releases will also be published as a release but will be more aggressively
gc'd.

## Dependency Management

The dependency management for the `openxla-compiler-release` repository will
be based on the same style of `openxal-devtools` roll schedules as are used
to automatically sync sub-components (e.g.
[instructions](https://github.com/openxla/openxla-pjrt-plugin#project-maintenance)
and example [automatic bump](https://github.com/openxla/openxla-pjrt-plugin/pull/139)).

We anticipate needing a slightly more advanced version determination heuristic
which calculates an appropriate/green set of compatible revisions, and we
will develop this incrementally once a simple heuristic and/or manual action
has produced results.

## Build environment

Where at all possible, Linux builds will be done in an appropriate
[`manylinux`](https://github.com/openxla/iree/blob/main/build_tools/docker/dockerfiles/manylinux2014_x86_64-release.Dockerfile)
container with auditwheel and other standard tricks applied to make them
relocatable. Specialty containers may be used for various exotic runtime
component builds.

As it is already for the sub-components, the entire process will be scripted
without reliance on CI-only actions.

We will leave space for MacOS, Windows, and ARM Linux releases but will not
enable them in the first step.

## Followon work

We expect that the production of standard/stable binary releases will unlock
many follow-on testing flows, and these can be incorporated into the CI such
that releases can be qualified prior to being taken out of draft mode.

This initial spike will also not handle actual upload of releases to packaging
repositories (like PyPi). That will be a manual process and automated at an
appropriate time.

## Timeline

Since this is mostly re-mixing scripts and packaging setups that already exist,
we expect that instantiating the basic spike to produce binary packages is a
task that can be completed within ~a week of actual development time. However,
with multi-tasking and approvals, it may take 1-2 months to instantiate the
entire flow in a minimally usable state.
