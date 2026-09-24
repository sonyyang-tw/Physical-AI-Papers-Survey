---
layout: paper
title: "GR00T N1: An Open Foundation Model for Generalist Humanoid Robots"
section: vla
page_id: "1945393079"
permalink: /vla/gr00t-n1-an-open-foundation-model-for-generalist-humanoid-robots-1945393079/
---

**Paper** : [GR00T N1: An Open Foundation Model for Generalist Humanoid Robots](https://arxiv.org/abs/2503.14734)  
**Source** : arXiv / NVIDIA  
**arXiv ID** : 2503.14734

### Abstract

General-purpose robots need a versatile body and an intelligent brain. Recent advances in humanoid robots have shown great promise as a hardware platform for building generalist autonomy in the human world. A robot foundation model trained on large-scale, diverse data sources is essential for enabling robots to reason about novel situations, robustly handle real-world variability, and rapidly learn new tasks. To this end, the authors introduce GR00T N1, an open foundation model for humanoid robots. GR00T N1 is a Vision-Language-Action (VLA) model with a dual-system architecture: the vision-language module (System 2) understands the environment through visual and language instructions, and the subsequent diffusion transformer module (System 1) generates fluid motor actions in real time. The two modules are tightly coupled and trained jointly end-to-end. The authors train GR00T N1 on a heterogeneous mixture of real robot trajectories, human videos, and synthetically generated datasets. They show that their generalist robot model, GR00T N1, outperforms state-of-the-art imitation learning baselines on standard simulation benchmarks across multiple robot embodiments. Furthermore, they deploy the model on a Fourier GR-1 humanoid robot to perform language-conditioned bimanual manipulation tasks, achieving strong performance with high data efficiency.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945393079_groot_fig2.png) 

_Figure 2: GR00T N1 Model Overview — dual-system VLA design converting image/language into action tokens_

![Figure]({{ site.baseurl }}/assets/images/1945393079_groot_fig3.png) 

_Figure 3: GR00T N1 Model Architecture — trained across embodiments from single-arm robots to bimanual humanoid hands_

  * Problem to be solved: How to build a generalist humanoid robot foundation model that can simultaneously handle "high-level semantic understanding (perceiving the scene, understanding instructions)" and "low-level real-time action generation (fluid, high-frequency motor control)," two requirements operating at very different time scales.
  * Main method: Adopts a dual-system architecture, drawing on the "System 1 / System 2" concept from cognitive science—System 2 (vision-language module) handles slower but semantically rich environment understanding and instruction parsing, while System 1 (diffusion transformer) handles real-time, high-frequency action generation. The two are tightly coupled and trained jointly end-to-end, rather than trained separately and stitched together.
  * Difference from prior approaches: Most prior VLA models used a single integrated architecture to handle both semantic understanding and action generation simultaneously (such as RT-2's single token sequence generation, or π0's VLM + action expert). GR00T N1 more explicitly splits "semantic understanding" and "action generation" into two systems operating at different time scales, and uses a diffusion transformer (rather than flow matching or autoregressive tokens) as the action generation module. Additionally, the training data for the first time systematically mixes three heterogeneous sources—real robot trajectories, human videos, and synthetic data (the so-called "data pyramid").
  * Key method design description: The vision-language backbone uses NVIDIA's Eagle-2 VLM to encode language and image inputs; the subsequent DiT (diffusion transformer)-based flow-matching policy module outputs high-frequency actions. The publicly released GR00T-N1-2B model has 2.2B total parameters (of which the VLM portion is 1.34B), and sampling a chunk of 16 actions on an L40 GPU in bf16 precision takes only 63.9ms. The training data follows a "data pyramid" structure—data volume decreases from the base to the top, while embodiment-specificity increases: the base consists of large amounts of general human video and synthetic data, while the top consists of a small amount of highly embodiment-specific (e.g., Fourier GR-1) real demonstrations.

### Result

  * Main enhancements: GR00T N1 outperforms state-of-the-art imitation learning baselines on standard simulation benchmarks across single-arm, bimanual, and humanoid robot embodiments; on the real Fourier GR-1 humanoid robot performing language-conditioned bimanual manipulation tasks, it shows strong performance with high data efficiency. In terms of inference speed, the 2B-parameter model samples a 16-step action chunk on an L40 GPU in just 63.9ms, indicating substantial real-time practicality for deployment.
  * Whether the results are fair: The paper is published by NVIDIA, and the comparison baseline is "state-of-the-art imitation learning baselines"; the specific baseline names and numbers require verification against the full paper to confirm fairness of comparison. Since the model and code are open-sourced (Isaac GR00T, continuously updated up to N1.7), it has high verifiability, which to some extent corroborates the credibility of its results.

### Limitation

  * The abstract does not explicitly list a limitations section, but inferred weaknesses include: (1) the "data pyramid" concept means the top tier (data most closely matched to a specific real embodiment) has the smallest quantity, so transfer performance to entirely new embodiments not covered at the top of the data pyramid requires verification against the full paper; (2) although the dual-system architecture has clear division of labor, the coordination latency between the two systems and how effectively System 2's semantic understanding results are passed to System 1's action generation, along with design details and potential bottlenecks, require verification against the full paper; (3) the currently public GR00T-N1-2B is a scaled-down model, and the full-size model's performance and resource requirements may differ.

### Related work

  * The Isaac GR00T project on GitHub has continued to evolve up to N1.7, adding new features such as whole-body humanoid control and large-scale human video pretraining, showing that this model series is still iterating rapidly.
  * GR00T (the N1 series) has been listed as an analysis subject by multiple 2026 VLA mechanistic interpretability papers (such as Not All Features Are Created Equal, 2603.19233), alongside π0.5 and SmolVLA as representative multi-pathway architectures, showing that its architectural design is considered representative.
  * Extremely worthwhile to survey: GR00T N1 is NVIDIA's flagship work in the humanoid robot foundation model space, and its dual-system architecture and data pyramid training strategy are of significant reference value for understanding the current technical trajectory of humanoid robot VLAs.

### Conclusion

  * Overall assessment: GR00T N1 proposes a systematic solution for the more complex embodiment of humanoid robots via a dual-system architecture and heterogeneous data mixture training, and releases the model and code openly, providing an important boost to the entire humanoid robot VLA ecosystem—well worth in-depth reference.
  * Relationship with other important papers: GR00T N1, along with π0.5 and SmolVLA, belongs to the "multi-pathway (separate VLM + expert/action module)" architectural camp, and is used as an analysis subject by papers such as Not All Features Are Created Equal (2603.19233), which confirm that its expert pathway and VLM pathway indeed encode different information (action programs vs. goal semantics). This is highly similar to Helix's (Figure AI) "System 1 / System 2" design philosophy, showing that dual-system architecture has become one of the mainstream design paradigms for humanoid robot VLAs. For ROCm/AMD, GR00T N1's published inference performance data (63.9ms/16-step chunk on an L40 GPU) provides a concrete performance reference point; if AMD wants to assess its own GPUs' competitiveness in humanoid robot VLA inference, this can serve as a benchmark comparison. However, the paper itself only mentions test data on NVIDIA's own GPU (L40), not performance on ROCm or AMD hardware—this is an extrapolated judgment rather than an explicit comparison in the paper.
