---
layout: paper
title: "Inference-time Physics Alignment of Video Generative Models with Latent World Models"
section: wm
page_id: "1959634541"
permalink: /en/wm/inference-time-physics-alignment-of-video-generative-models-with-latent-world-mo-1959634541/
---

### Abstract

Current state-of-the-art video generative models can produce visually persuasive content, but frequently violate basic physical laws, limiting their practical usefulness. This has often previously been attributed to insufficient physical understanding during pretraining, but the authors of this paper find that deficiencies in physical plausibility also stem from suboptimal inference strategies. The authors therefore propose WMReward, which reframes "improving the physical plausibility of video generation" as an inference-time alignment problem: it uses the strong physical priors of a latent world model (this paper uses Meta's V-JEPA 2) as a reward signal to search for and guide multiple candidate denoising trajectories during generation, trading increased test-time compute for improved generation performance. Experiments show that this method significantly improves physical plausibility across image-conditioned (I2V), multi-frame-conditioned (V2V), and text-conditioned generation scenarios, and this has been verified through human preference studies. Notably, in the ICCV 2025 Perception Test PhysicsIQ Challenge, this method won first place with a final score of 62.64%, exceeding the previous best result by 7.42 percentage points. This study demonstrates the feasibility of using latent world models to improve the physical plausibility of video generation, and this approach is not limited to any specific model implementation or parameterization.

### Method

**Problem addressed**: Existing video generation models (whether image-to-video or video-to-video) often produce results that violate physical intuition (such as objects passing through each other, or implausible collision responses). Previous research has mostly attributed this to insufficient physical understanding in the training data or the architecture itself, with relatively little exploration of whether the "inference strategy" itself is also one of the root causes of physical implausibility.

**Main method**: The authors propose WMReward — using V-JEPA 2 (Meta's self-supervised latent world model) as a reward function for physical plausibility, and during the inference stage of a video diffusion model, searching and steering multiple candidate denoising trajectories. This essentially applies test-time compute scaling to the physical alignment problem of video generation: without needing to retrain the generative model itself, additional computational resources are spent at inference time to filter/guide toward generation results that better match the world model's physical prior.

**Difference from previous approaches**: Unlike most existing research on improving the physical plausibility of video generation (which focuses on training data augmentation, architectural changes, or physics loss functions during training), WMReward operates entirely at inference time, combining "using a pretrained latent world model as a real-time reward signal" with "multi-candidate trajectory search." This is a new approach orthogonal to training-time fixes, and can be stacked on top of any pretrained generative model; it also demonstrates that a world model like V-JEPA 2, originally designed for representation learning/robotics tasks, can be directly repurposed as an evaluation and guidance tool for video generation quality, crossing the traditional boundary between "world model training" and "generative model inference."

**Key method illustration**: Figure 1 (embedded below, teaser) shows this method achieving new state-of-the-art results on the PhysicsIQ benchmark in both single-frame (I2V) and multi-frame (V2V) conditioned generation scenarios; Figure 3 (embedded below, method overview) presents in detail the overall process of using V-JEPA-2 via a sliding window to score and guide candidate denoising trajectories.

![Figure]({{ site.baseurl }}/assets/images/1959634541_wmreward_teaser.png) 

_Figure 1: On the PhysicsIQ benchmark, WMReward achieves new SOTA on both I2V and V2V conditioned generation_

![Figure]({{ site.baseurl }}/assets/images/1959634541_wmreward_method.png) 

_Figure 3: Method Overview — using the V-JEPA-2 latent world model as a reward, guiding candidate denoising trajectories via a sliding window_

### Result

**Main enhancements**: Won first place on the official leaderboard of the ICCV 2025 Perception Test PhysicsIQ Challenge with a final score of 62.64%, exceeding the previous generation SOTA by 7.42 percentage points; significant improvements in physical plausibility were observed across image-conditioned, multi-frame-conditioned, and text-conditioned (VideoPhy benchmark) generation scenarios, and the actual perceptual effectiveness of the results was verified through human preference studies (pairwise comparisons across the three criteria of Physics Plausibility / Visual Quality / Prompt Alignment), rather than being limited to improvements in automated metric numbers alone.

**Whether the results are fair**: The paper also reports visual quality (VBench metrics, Table 5) as a control, showing that improving physical plausibility does not come at the cost of overall visual quality; and it discloses the full computational cost (inference time, relative memory overhead multiplier) in Table 4, transparently presenting the core trade-off of "trading compute for physical plausibility," without appearing to deliberately avoid cost disclosure. The PhysicsIQ Challenge is an independent evaluation hosted by a third party (the ICCV 2025 Perception Test workshop), and the first-place result carries relatively high credibility, corroborating the authors' self-reported results.

### Limitation

**Known limitations**: The authors honestly disclose in Figure 10 (Failure Mode Analysis) that even with V-JEPA-2-based inference-time guidance, several persistent physical phenomena still fail — for example, modeling of rapid physical events such as fluid splashing remains inaccurate — showing that this method is powerless against "physical phenomena that the world model itself has not yet learned well," essentially limited by the upper bound of the underlying latent world model's (V-JEPA-2's) physical understanding.

**Weaknesses inferred from the results**: The computational cost multiplier shown in Table 4 means that this method belongs to the route of substantially increasing compute at inference time in exchange for quality; the actual latency and cost during deployment could be quite considerable, limiting its applicability to real-time applications (such as interactive simulation or robot policy-in-the-loop rollout). In addition, the method relies heavily on the quality of V-JEPA-2's own physical prior — if replaced with a weaker world model, the effect could be significantly diminished. Although the paper claims the method "is not limited to a specific implementation," the empirical validation only used V-JEPA-2 as the world model, so generalizability still awaits cross-validation with more world models.

### Related work

The "World Model Evaluation & Physical-Reasoning Benchmarks" sub-topic on this page already includes physical plausibility evaluation papers such as PhyGround and WorldBench, which can be cross-referenced with this paper's PhysicsIQ/VideoPhy evaluation results; the foundation model section on this page already includes V-JEPA 2 (arXiv:2506.09985), and this paper can be seen as an extension of downstream applications of it, demonstrating that V-JEPA 2 can, in addition to its original robot planning/representation learning purposes, also be directly used as an inference-time reward signal for generative models — worth reading the two papers side by side to understand the multiple application scenarios of the V-JEPA series of world models. It is recommended to further track whether there are subsequent papers applying this "world model as inference-time reward" approach to robot action generation (rather than just video generation).

### Conclusion

The "inference-time physics alignment" perspective proposed in this paper is a novel and inspiring angle, extending the role of world models from "training data generation/planning tool" to "real-time judge and guide of generation quality," and is backed by authoritative third-party evaluation (champion of the ICCV 2025 PhysicsIQ Challenge), with both methodological contribution and empirical strength being strong — worth reference. It forms a direct dependency relationship of "upstream world model — downstream inference-time application" with the foundation model V-JEPA 2 on this page; it forms a triangular relationship of "generator — evaluation benchmark — quality guidance method" with the Video-Generation World Models sub-topic (sub-topic 1, such as Genie 3, Cosmos 3) and the Evaluation & Benchmarks sub-topic (sub-topic 5). For ROCm/AMD, the gap highlighted by this kind of paper is that test-time compute scaling (multi-candidate trajectory search and guidance) has extremely high requirements for memory bandwidth and batch inference throughput, while the currently public V-JEPA 2 / video diffusion model inference performance evaluations and optimization cases in industry are almost all based on NVIDIA GPUs. AMD still lacks ROCm performance benchmarks and optimization practices targeting this kind of "world-model-guided test-time search" inference pattern, which is worth pursuing as a future area of improvement.
