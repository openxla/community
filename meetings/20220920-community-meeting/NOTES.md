# SIG OpenXLA Meeting Minutes 09/20 8AM PT

Please see the [slide deck](https://github.com/openxla/community/blob/main/meetings/20220920-community-meeting/%5BPublic%5D%20SIG%20OpenXLA%20Meeting%202022.9.20.pdf) for in-depth content.

# Notes

## James Rubin provides overview and refresher on:
 * The OpenXLA Project
 * Refresher on meeting policies
   * Monthly on Zoom
   * Rotating meeting host & scribe
   * Proposed agenda shared by host week prior in community wiki
   * Meeting minutes & slides shared publicly on community wiki by host day after
 * Refresher on collaboration channels

## Eugene Burmako provides an update on StableHLO:
 * Lots of OSS momentum (74 issues and 83 PRs in only a month).
 * Main areas of development: spec/interpreter, completeness of verification/shape inference, compatibility proposal, integration into MLIR-HLO.
 * Integration into MLIR-HLO: [StableHLO now ships as part of MLIR-HLO](https://github.com/tensorflow/mlir-hlo/tree/master/stablehlo) to simplify experiments/adoption for existing MHLO users.
 * Overall, StableHLO is ready to supersede MHLO as a compiler interface. It ships in the same repo, has the same ops but additionally comes with compatibility guarantees.
 * [Compatibility RFC](https://github.com/openxla/stablehlo/pull/115): 6 months backward compatibility, 3 weeks forward compatibility, lots of details of how this will work. Let us know what you think!
 * Next steps: 
   * 1) bootstrapping governance/RFC process
   * 2) adoption by *HLO producers: JAX, PyTorch/XLA, TensorFlow\
   * 3) conversations with ONNX-MLIR and Torch-MLIR
   * 4) collaboration & integration with TCP.

### StableHLO Q&A

**Are the ONNX and Torch requests for feature publicly available?**
 * ONNX-MLIR discussion is on [GitHub](https://github.com/tensorflow/mlir-hlo/issues/44). 
 * PyTorch/XLA discussion is currently internal, we'll be posting details [on GitHub](https://github.com/pytorch/xla) soon.
 * Torch-MLIR discussion is in the #torch-mlir channel on LLVM discord.

**So JAX will create graph in StableHLO instead of MHLO?**
 * Yes, that's the plan.
 * Same for the TF/XLA bridge.
 * For other producers, the conversations are ongoing, but I think this will likely be the case as well.

**What is the plan for StableHLO forward compatibility?**
 * See [Compatibility RFC](https://github.com/openxla/stablehlo/pull/115) - it goes into a lot of details on how we propose to define forward compatibility and how we're planning to uphold it through various dialect evolution scenarios.

**Today, we produce MHLO which is then converted to HLO. How is this going to work with StableHLO?**
 * StableHLO has been bootstrapped from MHLO, our plan to keep it close to MHLO.
 * MHLO is currently a superset of HLO (supports the same features + unbounded dynamism + quantization), in the future we're planning to achieve MHLO/HLO parity.
 * Therefore, if the MHLO => HLO => ... workflow is working for you today, it's going to work with StableHLO as well.

## Eugene Zhulenev provides a deep dive on XLA Runtime (see slide deck for in-depth content): 
 * What did XLA use for a runtime before XLA Runtime?**
   * XLA:CPU compiles to a native X86 function pointer
   * XLA:GPU compiles to a ThunkSequence which is interpreted sequentially
   * New XLA Runtime aims to unify the “executable artifact” produced by different XLA backends
 * Overview of XLA Runtime
   * XLA programs (HLO modules) compiled to native functions with a help of LLVM JIT compiler
   * XLA Runtime provides high level C++ API to the user and takes care of matching ABI of the compiled XLA program so that users do not need to know any of the internal details
   * XLA Runtime provides a small runtime that supports executing compiled XLA programs, similar to how libc (standard C library) provides a small “runtime” that supports executing C programs
 * XLA Runtime workflow
   * Compilation pipeline
   * Executable
   * Runtime
 * PjRT, XLA, and XLA Runtime overview
 * XLA Runtime is an implementation detail of the XLA:GPU executable, not visible to the XLA users
 * XLA Runtime roadmap

### XLA Runtime Q&A

**Is there a persistent format for storing xla executable and loading and running them later?**

ELF file (or PE on Windows) + metadata (all likely stored in a protobuf message) will be the format for saving/loading XLA programs

**How is the shape/dim checking done at runtime in thx runtime?**

Function signature (entrypoint) is dynamically shaped, and XLA programs can be specialized and re-compiled for new shapes. We also support symbolic shapes (dimension sizes are not know, but we know equalities between them). Shape checks can be added as asserts in the IR, and the will be lowered to safe checks at runtime (no crashes).

**Does HSACO not serve the same purpose as CUBIN in the ROCm case? @Rohit**

Yes, compiled XLA program will have constant section with device kernels in whatever format the device driver wants them.

**What will drive the XLA RT decision to run parts in cpu / gpu? will the user pass a hint? will the device backend be able to say what is support?**

Probably will be explicit initially, because experience with TF shows that automatic partitioning is very hard.

**Is there a persistent format for storing xla executable and loading and running them later?**

Answered above. 

**What about windows? and in the future do you have plans for heterogenous host/accelerator configs?**

Windows is a supported platform, and everything should work. We rely on LLVM ORC and it’s well tested on Windows.

**Thoughts on Arm CPU support?** 

Yes we plan to support ARM, if there is a compiler, and LLVM ORC AFAIK supports ARM. 

## Next Steps

 * Google to send out update on OpenXLA workstreams:
 * Project and product messaging proposal (Sept 22)
 * Standalone repository progress (week of Sept 26)
 * Governance model proposal (week of Sept 26)
 * New OpenXLA logo proposal  (week of Sept 26)
 * Follow-up GitHub discussion on XLA Runtime (Sept 20)
 * Request for marketing approvals to announce the SIG launch
 * Community feedback for next SIG meeting and technical deep dive
