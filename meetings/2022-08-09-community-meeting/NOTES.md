# SIG OpenXLA Community Meeting
## Meeting Info

Date/time: 2022-08-09 9-10AM PDT

Host: Thea Lamkin (Google)

Scribe: James Rubin (Google)

## Notes

* [Thea Lamkin] kicks off the first Public SIG OpenXLA meeting. Thanks everyone involved for making this possible.
  * Housekeeping: Overview of OpenXLA meeting cadence, structure, and tools
    * Rotating host and scribe: host will have expectation of agenda and managing meeting minutes
    * What meetings should include: Roadmaps
  * Introductions: Thea asks new members to introduce themselves?
    * Raghavan: part of ML Compiler team at Cruise. He is here as an observer.
    * Hongbin: compiler engineer from Amazon. He has been using XLA for Inferentia and Trainium and would like to collaborate to improve XLA.
    * Rohit: Is part of the TensorFlow group at AMD and is here in Jason’s place (Jason is OOO).
  * Thea: introduces herself and then introduces technical presentations.
* [Mehdi Amini] introduces TensorFlow/XLA refactoring presentation and shares design of the new repositories. He describes:
  * Work to cut the dependences on TensorFlow and other code
  * Work to separate TensorFlow/XLA into 3 repositories:
    * XLA
    * TensorFlow
    * Tensor Standard Libraries (TSL)
  * Code contents of the repositories including:
    * Stream Executor and JitRT in XLA
    * Utilities and profiler service in TSL
    * XProf, TensorFlow-to-XLA bridge in TensorFlow
  * The new GitHub user and repository where issue tracking will take place: https://github.com/openxla/xla
  * **Ashok (ARM)**: “What will happen to TFRT? Will it no longer exist because of JitRT in XLA?”
    * **Mehdi**: “No, TFRT will exist as it does today. We extracted a very low level piece of TFRT called JitRT that is used by XLA and put it in the XLA repository. JitRT is a compiler specific part of TFRT and isolated. TFRT will remain intact for the most part: threadpool remains in TFRT, etc. I believe we are renaming JitRT to the “XLA runtime” in the future and we are planning deep dives to cover what this component is. Right now it is in development under tensorflow/compiler/xla/mlir/.”
  * **Vinod (NVIDIA)**: Is PJRT the base for the XLA runtime?
    * **Mehdi**: “PJRT is a public API that is a facade for clients like TensorFlow or JAX. For example, how to set-up a device, initialize it, execute code on the device. It is an abstract class that can be subclassed. The XLA runtime (JitRT) is not publicly visible, it is the interface for XLA generated code to talk to C++ utilities (like TFRT AsyncValue). XLA will generate code where sometimes kernels need to asynchronously wait on each other, which will be possible with this thin runtime component. GPU back-end for XLA is currently “Thunk”, which is a custom data structure that describes the sequences of kernels to GPU. XLA runtime will replace this mechanism and unify it between CPU, GPU, and other things.”
  * **Vinod**: “Will PJRT be part of JAX or XLA?”
    * **Mehdi**: “PJRT will remain part of XLA. We want to evolve it. This work will be discussed in public from now on. We want to make a plan for what is the public interface for XLA.”
  * **Vinod**: “It could be useful to share the evolutionary direction for all these XLA components on a high-level.”
    * **Mehdi**: “Stephan will present our roadmap plans later (see below) and we will also have a deep dive on technical aspects in a future meeting.”
  * **[UNKNOWN]**: Will MHLO be part of XLA repo?
  * **Mehdi**: Yes, MHLO has been moved under /xla in the TensorFlow repository so that MHLO will come with XLA when we move it into a standalone repository within the OpenXLA GitHub org. StableHLO will be covered later in the presentation [see the notes below].
  * **Rich (Amazon)**: Asking from the perspective of someone who wants to ship a compiler that is common to PyTorch, JAX, and TensorFlow, what are the dependencies on TensorFlow?
  * **Mehdi**: This has been designed so that we can build JAX and PyTorch/XLA without cloning TensorFlow code. There are no dependencies on TensorFlow. No TensorFlow code will be built at runtime.
  * **Kushan (NVIDIA)**: From the comments in the StableHLO repo, it sounds like it is a version of MHLO and not just replicating MHLO inside of OpenXLA.
  * **Mehdi**: The section about StableHLO is later in the presentation. Mehdi then passes on to Stephan.
* **Stephan Herhut** introduces himself. He is the overall tech lead for XLA CPU/GPU. He will discuss Google’s proposed contributions to the OpenXLA roadmap over the next couple of years. The roadmap aims to describe what Google is working on, but it is subject to change. What he is presenting is open to discussion and feedback. Please see the slide deck for the full details of his presentation.
  * Performance & Scalability
    * 2022 Goals: (1) Deliver out-of-the-box performance that satisfies users needs (2) Build out MLIR-based infrastructure to scale to meet future needs
    * Performance initiatives for 2022 include: (1) Improved fusion and use of shared memory on GPU (2) Improved performance on SoftMax
    * Scalability initiatives for 2022 are missing because we finished our scalability work for 2022, specifically, SPMD on CPU/GPU
  * **Vinod**: “When OpenXLA goes into the repository will TensorFlow use the new XLA or old XLA? I have the same question for other frameworks.”
    * **Mehdi**: “There will only be one XLA. OpenXLA is not a fork. The work that Stephan is presenting is our plan for XLA CPU/GPU codegen. This is the direction that the Google XLA CPU/GPU team wants to go in, but we want to get input from the community. Google will contribute this work to OpenXLA.”
  * **Vinod**: “When this repo split happens will the OpenXLA functionality and performance will be on par with the original XLA?”
    * **Mehdi**: “We’re going to take the TensorFlow/XLA codebase and move it into a new standalone repository under OpenXLA. The existing XLA codebase will be deleted from the TensorFlow repository. The existing XLA codebase is the starting point for this work that Stephan is presenting.”
    * **Stephan**: “This is not a new compiler. We are taking XLA as it is and evolving it. The changes are mainly to the development model.”
  * **Rich**: “How should we interpret the use of GPU in the roadmap speaking as a non-GPU platform? There are accelerators like Trainium that are not classically GPU or CPU-based.”
    * **Stephan**: Skips to the Hardware & Framework Optionality slide. “I naturally speak about CPU/GPU, but we are aware that this is not the entire ecosystem. Hardware optionality: (1) We want to unlock device optionality. How do we do this? One thing we want to do is improve the layering of XLA to get better reuse of components so you don’t have to build an entirely new compiler to support your hardware. We are unifying the runtime for CPU/GPU so that it is not strictly a CPU or GPU runtime. We want to enable more floating point formats, which is something different hardware platforms care about. We’re also developing feature parity between MHLO and HLO. Enable different device runtimes that different parties are interested in. Framework optionality: (1) Interoperability between compiled and non-compiler code.”
  * **Vinod**: “OpenXLA will support StableHLO?”
    * **Stephan**: StableHLO is an input dialect. OpenXLA will accept StableHLO.
  * ** Stephan**: Goes back to the “Usability” slide. “OSS developer productivity is a priority for us.”
    * Describes Google efforts around processes, tooling, metrics, and documentation including: (1) “Metrics dashboard v1.0 will give us visibility into how contributions have an impact on compiler, workload, and hardware performance.”
    * Moves on to 2024 and beyond slide and discusses long term goals and initiatives for XLA including: (1) AOT machine learning compiler for mobile (2) device-specific optimizations via extension mechanisms and more
* **Eugene Burmako** introduces StableHLO presentation.
  * Outlines short-term and long-term workstreams (see slide deck):
  * **Vinod**: What do you mean by StableHLO being an "input format"? The specification of MHLO? Or maybe a binary format of some kind? Something else?
  * **Eugene**: Proposes that we have a new dialect called StableHLO, separate from MHLO. This dialect can then provide a binary serialization format through MLIR upstream work on binary serialization for dialects.  There is also ongoing work in MLIR upstream on versioning for dialects, and this dialect can leverage that too. Versioning is why I propose that we have two separate dialects - this way StableHLO can be versioned, and MHLO can evolve more or less freely without the technical and organizational overhead of versioning.
  * **ONNX Workshop**: Are you looking to make a standard? ONNX is doing something similar, so what do you think about bootstrapping from ONNX?
  * **Eugene**: Proposal is to bootstrap StableHLO from MHLO
    * Indeed, MHLO is just one of the ML compute opsets in the community - you mentioned ONNX, there are also TOSA, MIL and others.
    * HLO/MHLO have historically been XLA's input formats, so there's a natural alignment, hence the proposal.
    * I have further thoughts about this, but I don't think we have the time to discuss this at the moment. If you're interested in talking more, please reach out at GitHub Discussions or on [Discord](https://discord.gg/qmYw59RzwC).
* **Thea**: introduces SIG collaboration presentation. She proposes:
  * The different channels for discussions and collaboration
  * Scheduled synchronous meetings. We could make this an option if that is potentially more useful.
