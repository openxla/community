# RFC - Creating an openxla-nvgpu project

(imported from https://github.com/openxla/community/issues/71)

Now that [RFC - Proposal to Build IREE Compiler Plugin Mechanism](https://github.com/openxla/iree/issues/12520) has been implemented and is minimally working with both in-tree and [an early adopter](https://github.com/nod-ai/SHARK-Runtime/pull/48) out of tree implementation, we are ready to propose the official creation of a new `openxla-nvgpu` project to house:

* Compiler plugins aimed at vendor specific integrations for NVIDIA GPUs.
* Runtime extensions for advanced use cases of NVIDIA parts.
* Project scaffolding and development flow tooling.

Since this will be the first plugin project of note, we expect that to a certain extent, it will co-evolve with the mechanisms.

## Proposed Directory Structure

`openxla-nvgpu` will have a similar directory layout to IREE, upon which it depends:

```
compiler/
  src/
    openxla_nvgpu/
      Dialects/
runtime/
  src/
    openxla_nvgpu/
build_tools/
```

The build setup will use `bazel_to_cmake` for consistency and interop with the upstream IREE project (now that https://github.com/openxla/iree/pull/12765 has taken the steps to allow it to be used out of tree). The corresponding IREE build macros will be extended as needed.

## Dependencies

This project depends directly on:

* [IREE](https://github.com/openxla/iree) for the core platform.
* [openxla-pjrt-plugin](https://github.com/openxla/openxla-pjrt-plugin) for implementing an NVIDIA specific PJRT plugin.

It transitively depends on:

* LLVM/MLIR via IREE (will be disaggregated as a standalone dep at a future time to be determined).
* [xla](https://github.com/openxla/xla) via openxla-pjrt-plugin for plugin and runtime support.
* [stablehlo](https://github.com/openxla/stablehlo) via IREE.

## Releases

In the very short term, this project will not produce independent releases and will aim to be usable by project developers who are willing to build it from HEAD.

In the longer term, we would like to introduce a new top-level `openxla-compiler` releaser project which is responsible for packaging the platform (IREE) with stable versions of all supported vendor compiler plugins and making available as a standalone binary release. Such a project would eventually depend on this one and would effectively be the plugin-aggregated release of the present day `iree-compiler` packages (which will continue to be released as the "vanilla" platform without out-of-kind platform specific dependencies).

Also in the longer term, as the PJRT plugin support evolves, we anticipate releasing `openxla-nvgpu-pjrt` binary packages that can be used to interface NVIDIA GPUs to supported ML frameworks via `pip install`.

## Versioning and CI

Adding this top-level project pushes us firmly into a "many-repo" layout for OpenXLA projects. This will be further reinforced as IREE's dependencies and build tools are disaggregated over time and the top-level releaser projects are established.

As part of this, we will introduce a side by side workspace layout where dependencies are found relative to each other based on parent directory. Example:

```
iree/
xla/
openxla-pjrt-plugin/
openxla-nvgpu/
openxla-compiler-releaser/
```

Such a layout will be called an "OpenXLA workspace" and we will provide a `sync` script and CI tooling to help manage it. Each project will pin to green release tags in its parent (or other form of stable commit tracking) by maintaining a local metadata file of its openxla dependencies. The `sync` script will be both a simple way for developers to track known-good sync points for the workspace and for CIs to advance. There will be a CI bot which advances dependent projects to next stable sync points automatically. We expect that for projects that already have a strong release cadence like IREE, this will update pins to new nightly releases, and others will cascade from at-head commits.

This process of versioning will be developed over time with an eye towards being the one way to manage openxla project dependencies. It will likely be somewhat manual to start with. This will be derived in spirit from [the PJRT plugin sync script](https://github.com/openxla/openxla-pjrt-plugin/blob/main/build_tools/sync.py) and enhanced to provide better release tracking and version bump capabilities.

## Benchmarking

Benchmarks of the NVIDIA toolchain will be largely inherited and leveraged from the IREE project but run independently so as to provide a continuous view of the performance deltas and characteristics of the platform-independent upstream and the vendor-specific downstream.

## Next steps

As a very next step, the `openxla-nvgpu` project will be bootsrapped in the [iree-samples](https://github.com/iree-org/iree-samples) repository. It will be relocated, with history, to a new git repository once this RFC has matriculated.

## Project Ownership

The project will be set up as a collaboration between Google and NVIDIA, and per OpenXLA governance, will share maintainer responsibility between contributors from both companies with the goal of NVIDIA engineers taking on core maintainer responsibility as the project bootstraps and evolves.
