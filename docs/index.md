---
template: landing.html
hide:
  - navigation
  - toc

title: OpenXLA project
subtitle: |
  An open ecosystem of portable and extensible machine learning infrastructure
  projects that simplify ML development by defragmenting the tools
  between frontend frameworks and hardware backends. Built by industry leaders
  in ML software and hardware.
buttons:
  - text: StableHLO
    href: https://github.com/openxla/stablehlo
  - text: XLA Compiler
    href: https://github.com/openxla/xla
  - text: IREE
    href: https://github.com/openxla/iree
---

<section class="oxla-section" markdown>
<div class="oxla-section-inner" markdown>
<div class="oxla-features" markdown>

## StableHLO

An operation set spec that provides a shared abstraction for ML programs between
different ML frameworks and compilers.

+ <span class="material-icon">drafts</span>
  **Portable**
  All major ML frameworks (JAX, PyTorch, TensorFlow) can produce models
  in StableHLO.

+ <span class="material-icon">more_time</span>
  **Stable**
  StableHLO programs can be serialized into MLIR bytecode that provides
  long-term stability and backward-compatibility guarantees.

## XLA Compiler

An ML compiler that optimizes models for high-performance execution across
hardware platforms including GPUs, CPUs, and ML accelerators.

+ <span class="material-icon">terminal</span>
  **Builds anywhere**
  Build and compile your models optimally across leading ML frameworks such as TensorFlow, PyTorch, and JAX.

+ <span class="material-icon">speed</span>
  **Scales your performance**
  Maximize and scale performance through a wide range of production-tested optimization passes and automated partitioning for model parallelism.

+ <span class="material-icon">developer_board</span>
  **Runs anywhere**
  Run your models anywhere with support for all leading ML backends including GPUs, CPUs, and ML accelerators.

+ <span class="material-icon">home_repair_service</span>
  **Simplifies your tools**
  Eliminate the complexity of managing diverse domain-specific compilers. OpenXLA leverages the power of MLIR to bring the best capabilities into a single compiler toolchain.

## IREE

A next-generation compiler technology focused on low-overhead, latency-sensitive ML compilation and serving.

+ <span class="material-icon">extension</span>
  **Modular**
Provides a reusable and extensible architecture, built from the ground up in MLIR.

+ <span class="material-icon">open_with</span>
  **Scalable**
  Scales up to meet the needs of datacenters and down to meet the constraints of mobile and embedded systems.

</div>
</div>
</section>

<section class="oxla-section black" markdown>
<div class="oxla-section-inner" markdown>
<div class="oxla-community" markdown>

## Contributors

The OpenXLA project is developed collaboratively by leading ML hardware
and software organizations.

+ Alibaba
+ Amazon Web Services
+ AMD
+ Apple
+ Arm
+ Google
+ Intel
+ Meta
+ NVIDIA

We welcome contributions to any of our projects on GitHub. If you'd like to
contribute, check out our
[OpenXLA community resources](https://github.com/openxla/community#readme).

</div>
</div>
</section>
