---
layout: paper
title: "Cosmos Predict 2.5 and Transfer 2.5: Evolving the World Foundation Models for Physical AI"
section: wm
page_id: "1945767248"
permalink: /wm/cosmos-predict-25-and-transfer-25-evolving-the-world-foundation-models-for-physi-1945767248/
---

**Paper** : [Cosmos Predict 2.5 & Transfer 2.5: Evolving the World Foundation Models for Physical AI](https://huggingface.co/blog/nvidia/cosmos-predict-and-transfer2-5)  
**Source** : NVIDIA official technical blog / technical report (not a traditional peer-reviewed paper); related research pages: <https://research.nvidia.com/labs/cosmos-lab/cosmos-predict2.5/> , <https://research.nvidia.com/labs/cosmos-lab/cosmos-transfer2.5/> ; GitHub: nvidia-cosmos/cosmos-predict2.5, nvidia-cosmos/cosmos-transfer2.5  
**arXiv ID** : No formal arXiv paper link could be confirmed (related foundational research may correspond to arXiv:2511.00062, "World Simulation with Video Foundation Models for Physical AI," but information on the Predict 2.5 / Transfer 2.5 versions covered here comes mainly from the official blog and GitHub repo, not the arXiv paper itself verified in this pass; the exact correspondence between the two needs to be verified)

### Abstract

Cosmos Predict 2.5 and Cosmos Transfer 2.5 are next-generation versions of NVIDIA's Cosmos World Foundation Models (WFMs) family, designed for Physical AI applications (robotics, autonomous driving, etc.). Cosmos Predict 2.5 merges the three previously separate models (Text2World, Image2World, Video2World) into a single unified architecture capable of generating consistent, controllable video worlds from multiple input modalities. It is offered in 2B and 14B model sizes, is trained on 200 million high-quality pretraining video clips, and uses model merging along with new reinforcement learning algorithms to improve quality. It can generate sequences up to 30 seconds long, and when post-trained on proprietary/domain-specific data, achieves up to a 10x improvement in long-tail scenario generation accuracy. Cosmos Transfer 2.5 is built on top of Cosmos Predict 2.5 and is a conditional world generation model with adaptive multimodal control, able to generate high-quality world simulations based on various control inputs — such as edge maps, blurred video, segmentation maps, and depth maps (which may come from physics simulation engines like IsaacSim or from real-world video). Compared to its predecessor, Cosmos-Transfer1-7B, the Transfer2.5-2B model is 3.5x smaller in size, yet performs better in terms of quality degradation (hallucination/error accumulation) over long videos.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767248_cosmospredict25_fig1.svg) 

_Figure 1: Overview of the video data curation pipeline — converting raw multi-source real-world video into a high-quality, annotated, deduplicated training dataset._

![Figure]({{ site.baseurl }}/assets/images/1945767248_cosmospredict25_fig2.png) 

_Figure 2: The overall architecture of Cosmos-Predict2.5 — repeatedly stacking self-attention and cross-attention blocks in latent space, unifying the Text2World / Image2World / Video2World generation pipeline._

  * **Problem addressed**: Physical AI (robotics, autonomous driving) requires large amounts of high-quality simulation training data covering long-tail scenarios (rare weather, rare interaction events, etc.), while also needing world models that can generate consistent, controllable future world states based on various control signals (text, images, depth maps, segmentation maps, etc.). Previous versions of Cosmos were architecturally separate (Text2World/Image2World/Video2World), and the large model (Transfer1-7B) had a high inference cost.
  * **Main method**:
    * Cosmos Predict 2.5: Merges the three previously independent models — Text2World, Image2World, and Video2World — into a single unified architecture that accepts multimodal input to generate consistent future world video. It comes in 2B and 14B sizes, is pretrained on 200 million videos, introduces model merging and new reinforcement learning algorithms to improve generation quality, and can generate continuous sequences up to 30 seconds long. When post-trained on domain-specific data, it substantially improves long-tail scenario generation accuracy (up to 10x).
    * Cosmos Transfer 2.5: A conditional generation model built on top of Predict 2.5, supporting "adaptive multimodal control." It can be guided by various control inputs — edge maps, blurred video, segmentation maps, depth maps (sourced from physics simulation engines like IsaacSim, or from real-world video) — to guide world generation. The model is 3.5x smaller than its predecessor (Transfer1-7B), yet maintains better quality in long-video generation (reducing hallucination and error accumulation).
  * **Difference from prior approaches**: Compared to earlier Cosmos versions, Predict 2.5 replaces three separate models with a single unified architecture, simplifying the pipeline and potentially improving cross-modal consistency; Transfer 2.5 substantially shrinks model size (3.5x) while improving long-video quality stability, showing that efficiency and quality can improve simultaneously rather than following the traditional trade-off of "shrinking a model necessarily sacrifices quality." In addition, a distilled version for edge devices (Distilled Edge model) was added, supporting low-latency inference deployment.
  * **Key design description**: The Predict 2.5 architecture can be understood as a unified multimodal conditional generation backbone, where the input can be plain text, a single image, or a video clip, and the output is always a video of future world states; the training process includes large-scale pretraining (200 million videos) followed by two stages of quality enhancement via model merging and RL fine-tuning. Transfer 2.5 layers an "adaptive multimodal control" module on top of this backbone, capable of simultaneously or selectively ingesting multiple spatial control signals (such as depth, segmentation, edges), aligning these signals with control conditions from a simulation engine (IsaacSim) or from real video, and generating physically plausible world simulation videos usable for sim-to-real data augmentation.



### Result

  * Predict 2.5: After post-training on proprietary/domain-specific data, long-tail scenario generation accuracy improves up to 10x (compared to the non-post-trained version or a prior version; the specific comparison baseline needs to be verified against the original technical report).
  * Transfer 2.5: Model size is 3.5x smaller than Cosmos-Transfer1-7B, and the degree of quality score reduction across video chunks during long video generation is significantly less, meaning hallucination and error accumulation issues are reduced.
  * Timeline updates: On February 23, 2026, a distilled Transfer2.5 Edge model was released, supporting low-latency edge deployment, along with a corresponding Predict2.5 robot/policy version; a March 13 update noted that Cosmos Transfer 2.5 supports scalable, physically-based photorealistic simulation across diverse environments and lighting conditions, while Predict 2.5 can generate realistic future world states from multimodal input and improve long-tail scenario accuracy.
  * Fairness assessment: All of the above data come from NVIDIA's official blog and technical report and have not undergone independent third-party peer review. Claims such as "up to 10x" and "3.5x smaller with better quality" need to be verified against detailed benchmark tables in the official GitHub repo or research pages to understand the specific test scenarios and comparison baselines, bearing in mind that these are vendor self-reported performance claims.
  * It remains to be verified whether other papers/teams have conducted independent third-party benchmark comparisons of Cosmos Predict/Transfer 2.5.



### Limitation

  * The official materials do not contain an explicit "limitations" section (since this is a technical blog/product release document rather than an academic paper), so the Cosmos Cookbook or original technical report should be consulted to confirm whether any self-acknowledged limitations exist.
  * An important timeline-related limitation: as of June 1, 2026, NVIDIA has already released the next-generation Cosmos 3 (a unified language/image/video/audio/action omni-modal world foundation model), and the GitHub repos for Cosmos-Transfer2.5 and Cosmos-Predict2.5 have announced they are "no longer under active development, with only limited maintenance updates provided," with future new features to be concentrated on Cosmos 3. This means the Predict/Transfer 2.5 versions are now a "transitional generation" product with limited long-term support, a factor that should be taken into account when making adoption decisions.



### Related work

  * Updated related research: NVIDIA released Cosmos 3 in June 2026, the next-generation omni-modal world foundation model unifying language, image, video, audio, and action, replacing Predict/Transfer 2.5 as the current flagship product; the GitHub organization has also migrated to github.com/NVIDIA/Cosmos. There is also a related foundational research paper, arXiv:2511.00062, "World Simulation with Video Foundation Models for Physical AI," which may be the academic counterpart to the Cosmos series; its exact correspondence to Predict/Transfer 2.5 is worth verifying.
  * Assessment of how worthwhile this is to survey: high. The Cosmos series is a landmark commercial world foundation model product line in the industry (especially in physical AI/robotics sim-to-real), and its technical evolution (Predict/Transfer 2.5 → Cosmos 3) represents an industry trend direction worth continued tracking; however, since it has already been rapidly superseded by Cosmos 3, subsequent research focus should shift to the technical details of Cosmos 3.



### Conclusion

  * Overall assessment: Cosmos Predict 2.5 / Transfer 2.5 is an important commercial milestone from NVIDIA in the physical AI world model field, demonstrating a unified architecture, simultaneous model shrinkage and quality improvement, and multimodal control capability supporting sim-to-real data augmentation. It offers reference value for engineers wanting to understand large-scale industrial world model productization; however, since it has already been rapidly superseded by Cosmos 3, its technical lifecycle is short, and practical deployment decisions should prioritize evaluating the feasibility of migrating to Cosmos 3.
  * Relationship to other important papers: The Cosmos series represents a different technical track from the academic papers in this collection (such as Interactive World Simulator, WoVR) — the latter focus on lightweight, controllable world models for specific robotic tasks, whereas Cosmos pursues a large-scale, general-purpose, industrial-grade world foundation model route centered on integration with simulation engines like IsaacSim. The two can be viewed as complementary perspectives from academia and industry on world model research.
  * ROCm/AMD gaps to be strengthened: The Cosmos series' current training and inference ecosystem (GitHub repo, distillation/edge deployment, Diffusers support) is clearly centered on NVIDIA's own hardware and CUDA ecosystem (including dedicated support for the Blackwell architecture), with no mention whatsoever of ROCm or AMD hardware compatibility. This means that if AMD wants to compete in the emerging and rapidly growing physical AI/world model market, porting and performance validation of Cosmos Predict/Transfer 2.5 (and the soon-to-be-dominant Cosmos 3) on ROCm represents a clear and yet-to-be-filled gap, worth prioritizing as an investment area for the ROCm ecosystem.
