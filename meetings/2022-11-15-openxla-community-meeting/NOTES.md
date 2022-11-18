

##  OpenXLA Community Meeting - 2022/11/15 - 8AM-9AM PST

[Recording here](https://www.youtube.com/watch?v=LIaR7Dtfbxs&list=PLlFotmaRrOzu8TQsTahDo_Cn7QdntFlUL)

Agenda

* Introductions
* OpenXLA OSS channels and resources
* FP8 RFC
* TensorFlow/XLA Refactor Update
* Community Updates

Notes

* gives overview of mission, gives opportunity for introductions, overview of SIG Collaboration channels and meeting structure,
* New attendees:  
    * Vartik from Intel
    * A colleague of Moshe from Habana Labs
    * Slai-nick from Sailence Labs
*  
    * **Background**: FP8 refers to any 8-bit floating point format. Traditionally in machine learning people have mostly used FP16, BF16, and fp32 formats
        * An advantage of using 16-bit formats is that many accelerators running operations faster in them
        * Recently NVIDIA released their new generation of GPUs called Hopper GPUs, they support lower precision format FP8.
        * NVIDIA claims that with FP8 they can run ML models E2E 1.2 to 1.5x faster than 16-bit formats
    * Requests that attendees take a look at the FP8 RFC. Reed emphasized that RFC is not finalized feedback would be appreciated: github.com/openxla/xla/discussions/22
    * RFC is proposing: 
        * Adding FP8 dtypes supported in NVIDIA Hopper and by NVIDIA, Intel, Arm
        * Other vendors are supporting own type of FP8. The dtypes differ in minor details. 
        * For now, Google is just proposing to add the NVIDIA, Intel, Arm dtypes, which there are two of. 
        * If other vendors want to add their FP8 dtype they could create their own proposal and we can consider taking it into StableHLO and XLA. 
    * RFC discusses how the design might involve in the future: 
        * Use special quantized types of ops that exist in StableHLO. 
        * Ops are not ready to be used with FP8 in StableHLO. 
        * RFC doesn’t make recommendation as to whether we should use these special quantized ops
    * Reed provides an overview of FP8 dtypes: E4M3 and E5M2. 
        * E4M3 should be used on the forward pass and E4M3 should be used on the backward pass because that results in the optimal model quality.
        * Note how low dynamic range is.
    * **Scaling**: If you try to use E4M3 in your model or even E4M2 to an extent it will not be the same as for 16-bit formats. Every tensor needs to have a scalar number called a scale associated with it. It is a form of quantization.
    * Unlike inference integer quantization, we cannot compute the scales ahead of time. We have to compute it dynamically because the weights change over time. We need to change our scales during training.
    * The trick we use is that every step the compute the scale for the next step and then we use the scale computed in the previous step.
    * It’s a basic form of pipelining that allows us to get the benefit of the dynamic scale while not paying the performance cost.
    * **FP8 changes to StableHLO/MHLO/HLO**: In IRs StableHLO/MHLO/HLO, the only we’re going to make is add to dtypes and passing tensors of these dtypes to various ops. Raises the question of how we represent scaling.
    * **How we represent scaling**: We use multiply and divide ops.
        * Generic approach: works for any single op. You can run any HLO op with scaled FP8 inputs and outputs. You never want to have an unscaled FP8 tensor.
        * Second approach: mathematically equivalent to generic approach, but only works with a few ops, notably Dot and Convolve
    * **Question from Maciek Urbanski**: can you upscale to something other, higher-than-fp8 precision types can be used or fp16 is a requirement ? My question is in the context of quantized_dot_generic.
        * **Answer from Reed**: No you can upscale to whatever you want. The pattern matching code needs to be aware of what types it can upscale to. Fusion pass is generic so we don’t have to hard code any particular precision type.  
    * **Question**: Is there any work ongoing in supporting FP8 data types in the frameworks like TensorFlow and JAX
        * **Answer**: There will be support in TensorFlow and JAX, hopefully by the end of the year. The user will still have to do some work by hand, but it will be possible to use.
    * **Question**: You are making scaling and unscaling explicit in the IR. Doesn’t that increase the size of the internal IR. Could you have maybe chosen an implicit encoding of that?
        * **Answer**: We didn’t want to have to add the scale concept to a ton of ops so it does increase size of IR. StableHLO has special quantized types and ops. StableHLO has special quantized types represents both a tensor and scale associated with it.
    * **Question**: In the future you may consider that? 
        * **Answer**: We might in the end choose to only fully support using the quantized ops if we go that direction. We can’t force the user to not pass.
    * **Question**: Question about example. In this example, the dot product of a vector with that same vector.
    *  provides update on TensorFlow/XLA Refactor
        * Gives a recap of the three repository solution: (1) TensorFlow (2) XLA (3) TSL
            * Describes content of each repository
        * Gives update on current status
            * 99% of TSL is complete and you can already clone the repository
        * Walks through the PR review and submit flow in different phases (December, December-January, January-February)
    *  provides list of StableHLO RFCs and reminder that the next OpenXLA Community meeting has been rescheduled to December 13th at 8AM PST

Chat questions:

**Vinod Grover**: You still mention MHLO.. isn't that going away, to be rplaced by StableHLO?



* **Eugene Burmako**: StableHLO is replacing MHLO in its role of compiler input. MHLO the compiler IR will still be around.
* **Mehdi Amini**: MHLO is what every pass inside the compiler will operate on. It won't be stable. StableHLO was bootstrapped from MHLO, but it won't replace it. It gives the options to evolve the compiler IR and have operations "internal" to the compiler (not part of the input).

**Vinod Grover**: What about HLO?



* **Mehdi Amini**: HLO is the non-MLIR encoding, we want to keep it at parity with MHLO. That said we'd also like to have an end-to-end pipeline using MLIR and avoid back-and-forth 
* **Mehdi Amini**: Unify the tooling as well: right now some of the tooling will work on one or another.

**Harry Saini**: Any other hardware than Hopper architecture which is close to support fp8 types?



* **Penporn Koanantakool**: Re: Harry: Habana Gaudi 2 can support FP8 in the Matrix Multiplication Engine (MME) [https://download.intel.com/newsroom/2022/corporate/vision/Habana-Gaudi2-Launch-Fact-Sheet.pdf](https://us02st1.zoom.us/web_client/9zdhk1t/html/externalLinkPage.html?ref=https://download.intel.com/newsroom/2022/corporate/vision/Habana-Gaudi2-Launch-Fact-Sheet.pdf)

**Kulin Seth**: For intermediate tensors which need to be forwarded from Backward pass for instance in Batch norm, how will that be handled ? I am assuming there will be additional function to handle them



* **Mehdi Amini**: Kulin: I suspect this has to be handled by the framework.
* **Reed Wanderman-Milne**: For the batchnorm question: As Mehdi mentioned, the framework can handle this in autograd
