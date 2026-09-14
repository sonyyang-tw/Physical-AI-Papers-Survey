---
layout: paper
title: "OpenVLA: An Open-Source Vision-Language-Action Model"
section: vla
page_id: "1945393020"
permalink: /en/vla/openvla-an-open-source-vision-language-action-model-1945393020/
---

**Paper** : [OpenVLA: An Open-Source Vision-Language-Action Model](https://arxiv.org/abs/2406.09246)  
**Source** : arXiv  
**arXiv ID** : 2406.09246

### Abstract

Large policies pretrained on internet-scale vision-language data and diverse robot demonstration data have the potential to change how robots learn new skills: rather than training new behaviors from scratch, such vision-language-action (VLA) models can be fine-tuned to obtain robust, generalizable visuomotor control policies. However, broad adoption of VLA faces two major challenges: 1) existing VLAs are mostly closed and difficult for the public to access; 2) prior work has not sufficiently explored how to efficiently fine-tune VLA for new tasks (a critical part of adoption). To address this, the authors propose OpenVLA, a 7B-parameter open-source VLA trained on a diverse collection of 970k real-world robot demonstrations. OpenVLA is built on top of the Llama 2 language model, combined with a vision encoder that fuses pretrained features from DINOv2 and SigLIP. Thanks to more diverse data and new model components, OpenVLA performs excellently on general manipulation tasks, achieving an absolute task success rate 16.5% higher than the closed model RT-2-X (55B) across 29 tasks and multiple robot embodiments, using 7x fewer parameters. The authors further demonstrate that OpenVLA can be effectively fine-tuned for new scenarios, showing particularly strong generalization results and language grounding capability in multi-object, multi-task environments, outperforming expressive imitation learning methods trained from scratch, such as Diffusion Policy, by a margin of 20.4%. The authors also explore computational efficiency, showing that OpenVLA can be fine-tuned on consumer-grade GPUs via modern low-rank adaptation (LoRA) methods, and can be served efficiently through quantization without loss of downstream success rate. Finally, the authors release model checkpoints, fine-tuning notebooks, and a PyTorch codebase with built-in support for large-scale VLA training on the Open X-Embodiment dataset.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945393020_openvla_fig1.png) 

_Figure 1: OpenVLA overview_

![Figure]({{ site.baseurl }}/assets/images/1945393020_openvla_fig2.png) 

_Figure 2: OpenVLA model architecture_

  * Problem addressed: existing VLAs are mostly closed and lack publicly available efficient fine-tuning methods, hindering community adoption of and research into VLA technology.
  * Main method: build a fully open-source 7B-parameter VLA model, combining an open-source language model backbone (Llama 2) with a fused vision encoder (DINOv2 + SigLIP), trained on a large-scale, diverse set of real robot demonstration data (970k episodes, sourced from Open X-Embodiment).
  * Difference from prior approaches: compared to closed models such as RT-2, OpenVLA is fully open-source (model weights, fine-tuning code, and data processing pipeline are all public); compared to a single vision encoder, OpenVLA fuses two pretrained visual features — DINOv2 (emphasizing spatial/geometric features) and SigLIP (emphasizing semantically aligned features) — improving the quality of visual representations. In addition, the authors systematically explore LoRA fine-tuning and quantized deployment methods, filling a gap left by prior work in "efficient fine-tuning/deployment."
  * Key method design: architecturally, visual input is passed separately through the DINOv2 and SigLIP vision encoders, and the fused features from both are fed into the Llama 2 language model backbone; action output continues the RT-2-style approach of discretizing actions into text tokens; the training data comes from 970k multi-embodiment demonstrations collected via Open X-Embodiment; fine-tuning can be performed with low-rank adaptation methods like LoRA on consumer-grade GPUs (rather than datacenter-grade hardware), and deployment can reduce inference cost through quantization without loss of success rate.

### Result

  * Key enhancements: across 29 tasks and multiple robot embodiments, OpenVLA (7B) exceeds RT-2-X (55B) in absolute success rate by 16.5% while using far fewer parameters; when fine-tuned to new scenarios, it shows particularly strong generalization and language grounding capability in multi-object, multi-task environments, outperforming Diffusion Policy trained from scratch by a margin of 20.4%; it also demonstrates that LoRA fine-tuning and quantized deployment do not sacrifice downstream performance, balancing performance and computational efficiency.
  * Fairness assessment: as an open-source model, OpenVLA's comparative results (especially outperforming RT-2-X) have already been cited by several subsequent papers (including multiple VLA interpretability papers in this task) as an analysis subject or benchmark, showing that its results enjoy considerable community recognition and reproducibility, and thus relatively high fairness.

### Limitation

  * Limitations stated by the authors or inferable: (1) actions are still represented via text-token discretization (continuing RT-2's design), which may have limited expressiveness on tasks requiring high-frequency, high-precision continuous control — this is also one reason later models such as π0 and GR00T switched to flow matching/diffusion; (2) although LoRA fine-tuning and quantized deployment are supported, the 7B parameter scale may still pose a challenge for real-time control scenarios requiring extremely low latency; (3) although the 970k training demonstrations are diverse, they are still predominantly drawn from a specific set of robot embodiments (those covered by Open X-Embodiment); its zero-shot transfer capability to entirely new hardware embodiments needs to be verified against the full paper.

### Related work

  * Several VLA interpretability papers covered in this task (such as Not All Features Are Created Equal, 2603.19233) list OpenVLA as one of their analysis subjects, showing that OpenVLA has become an important benchmark model for VLA mechanistic interpretability research.
  * Subsequent models such as π0 (2410.24164) and GR00T N1 (2503.14734) represent the direction of technical evolution beyond OpenVLA in terms of action output mechanism (flow matching/diffusion vs. text tokens).
  * Extremely high survey value: OpenVLA is one of the most important open-source benchmark models in the current VLA field; nearly all subsequent open-source VLA research references or compares against OpenVLA.

### Conclusion

  * Overall assessment: through being fully open-source and offering efficient fine-tuning and deployment solutions, OpenVLA has significantly lowered the barrier to VLA research and application, marking a pivotal turning point in the VLA field's shift from "closed large-vendor models" to an "open community ecosystem." Its impact on the field is enormous, and it is strongly recommended for reference.
  * Relationship to other important work: OpenVLA directly challenges and outperforms RT-2-X, while also serving as an important research subject for several mechanistic interpretability papers in this task (SAE, activation injection, etc.), showing that its open-source nature makes it one of the preferred platforms for academic research into internal VLA mechanisms. As for ROCm/AMD, OpenVLA — being fully open-source and supporting LoRA fine-tuning and quantized deployment — is one of the best current candidate models for validating VLA training/inference support on the ROCm ecosystem; since its weights and code are public, it can in principle be directly tested for training and inference compatibility and performance on AMD GPUs. This is one of the few models in this task list that is highly actionable (directly deployable and testable), and is worth prioritizing for evaluation by AMD teams as a starting point for validating the ROCm VLA ecosystem — though the paper itself does not mention any ROCm or AMD hardware test results; this is a reasonable extension based on its open-source nature.
