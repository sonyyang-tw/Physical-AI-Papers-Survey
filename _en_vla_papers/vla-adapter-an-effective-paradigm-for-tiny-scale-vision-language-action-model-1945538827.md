---
layout: paper
title: "VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model"
section: vla
page_id: "1945538827"
permalink: /en/vla/vla-adapter-an-effective-paradigm-for-tiny-scale-vision-language-action-model-1945538827/
---

**Paper** : [VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model](https://arxiv.org/abs/2509.09372)  
**Source** : arXiv, Accepted by AAAI 2026 (Oral)  
**arXiv ID** : 2509.09372

### Abstract

Vision-Language-Action (VLA) models typically bridge the gap between perception space and action space by pretraining a large vision-language model (VLM) on robot data; while this substantially improves performance, it also incurs significant training cost. This paper investigates how to effectively bridge "vision-language (VL) representations" to "action (A)," and proposes VLA-Adapter, a new paradigm designed to reduce VLA models' dependence on large-scale VLMs and extensive pretraining. The authors first systematically analyze the effectiveness of various VL conditions to identify which ones are critical for bridging the perception and action spaces; based on these findings, they propose a lightweight Policy module paired with a Bridge Attention mechanism that automatically injects the best conditions into the action space. In this way, the method achieves strong performance using only a 0.5B-parameter backbone and without any robot-data pretraining. Extensive experiments on simulated and real-world robot benchmarks show that VLA-Adapter not only achieves state-of-the-art performance but also delivers the fastest reported inference speed to date, and can train a strong VLA model on a single consumer-grade GPU in just 8 hours.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945538827_vlaadapter_fig1.png) 

_Figure 2: Comparison of representative existing VL-to-A bridging paradigms, illustrating how prior methods connect vision-language model outputs to action generation._

![Figure]({{ site.baseurl }}/assets/images/1945538827_vlaadapter_fig2.png) 

_Figure 3: The overall framework proposed by VLA-Adapter, with key components including condition exploration and the Bridge Attention design._

  * **Problem addressed** : Existing VLA models rely on pretraining large VLMs on large-scale robot data to achieve good performance, but this incurs enormous training cost and hardware requirements. The core problem this paper addresses is how to achieve high performance without robot-data pretraining and with a tiny-scale backbone.
  * **Main method** : VLA-Adapter first systematically analyzes the effectiveness of various "VL conditions" (i.e., which intermediate representations extracted from the VLM, such as features from different layers) for bridging the perception and action spaces, identifying the key necessary conditions. Based on this, it designs a lightweight Policy module that automatically selects and injects the most suitable VL conditions into the action generation process via a "Bridge Attention" mechanism.
  * **Difference from prior approaches** : Most existing VLA models (such as OpenVLA) rely on large VLMs (with billions of parameters) and pretraining on large-scale robot data to effectively bridge perception and action. VLA-Adapter takes the opposite approach, using only a tiny 0.5B-parameter backbone (based on Qwen2.5-0.5B), completely skipping the robot-data pretraining stage, and instead compensating for the smaller model scale and lack of pretraining data with a carefully designed "condition bridging" mechanism.
  * **Architecture/pipeline description** : The model is built on the Prismatic-VLMs architecture, with Qwen2.5-0.5B as the LLM backbone. Prior to training, the contribution of each VLM layer/type of representation (VL condition) to action prediction is analyzed, and after filtering out the key conditions, Bridge Attention dynamically injects these conditions into a lightweight Policy module, which converts the bridged representations into robot action outputs. The overall pipeline emphasizes lightweight design and training efficiency (training can be completed on a single consumer-grade GPU in 8 hours).



### Result

  * According to a search-result summary (via WebSearch, not a direct reading of the arXiv full text), VLA-Adapter achieves roughly a 14x reduction in model scale, 38x faster fine-tuning, and 3x higher inference throughput compared to existing SOTA methods, while achieving SOTA-level performance and the fastest reported inference speed on simulation and real-robot benchmarks.
  * Since this data comes from a WebSearch summary rather than a direct reading of the paper's full text or original abstract, the full text needs to be verified to confirm the specific calculation basis and comparison baselines for these multipliers.
  * The original arXiv abstract itself only offers qualitative descriptions such as "state-of-the-art level performance" and "fastest inference speed reported to date," without specific numbers; the quantitative results need to be verified against the full text.



### Limitation

  * The paper itself (at the abstract level) does not explicitly state its limitations.
  * From the method design, using only a 0.5B-parameter backbone and skipping robot-data pretraining is highly efficient, but whether it can still match large pretrained VLAs (e.g., 7B-scale models) on highly out-of-distribution or extremely complex long-horizon tasks needs to be verified against broader benchmark comparisons in the full text (especially the gap versus large models on difficult tasks).
  * This paper shares a similar goal with VLA-AD (Offline Semantic Guidance, paper 7 in this list) — "reducing model scale while maintaining performance" — but takes a different methodological path (VLA-Adapter relies on condition-bridging attention, VLA-AD relies on semantic distillation). Their relative merits in real-world scenarios need further verification and comparison.



### Related work

  * This paper already has a complete open-source implementation and subsequent optimized version (Pro version) on GitHub (OpenHelix-Team/VLA-Adapter) and HuggingFace, indicating substantial community attention.
  * According to WebSearch results, related/concurrent work includes StableVLA (arXiv:2605.18287, on robust VLA models without extra data), which is worth reviewing and comparing.
  * Degree to which the related work is worth surveying: high. This paper received an AAAI 2026 Oral and holds a landmark position on the topic of efficient/lightweight VLA. Surveying it alongside VLA-AD, EcoVLA, VLA-Perf, and other papers concerned with efficiency helps establish a complete picture of the "VLA lightweighting/efficient deployment" technical thread.



### Conclusion

  * The "lightweight Policy + Bridge Attention" approach proposed here offers an effective solution to the practical pain point of VLA training cost and deployment barriers, and has been recognized with an AAAI 2026 Oral, giving it high reference value — especially for resource-constrained settings (e.g., small/medium teams, single consumer-grade GPU).
  * Relationship to other important papers: This paper, VLA-AD (the distillation route), and EcoVLA (the device-edge collaborative inference route) all belong to different technical routes under the broader direction of "making VLA lighter, faster, and more resource-efficient." The three can be compared together to understand "model-side lightweighting design" vs. "post-training distillation" vs. "system-level deployment optimization" as three complementary approaches.
  * Relevance to ROCm/AMD: This paper emphasizes "training completed on a single consumer-grade GPU in 8 hours." If the ROCm ecosystem can support training/inference of the Qwen2.5-0.5B backbone and Prismatic-VLMs architecture (theoretically feasible with the PyTorch ROCm version), this method's low hardware barrier would be attractive for reproducing/validating VLA training on AMD GPU platforms. However, neither the abstract nor the search results mention whether the authors have tested on ROCm/AMD hardware; the full text and the official code repository (GitHub) still need to be checked for hardware compatibility information.
