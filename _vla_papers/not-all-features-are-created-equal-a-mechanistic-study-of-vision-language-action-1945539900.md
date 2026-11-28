---
layout: paper
title: "Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models"
section: vla
page_id: "1945539900"
permalink: /vla/not-all-features-are-created-equal-a-mechanistic-study-of-vision-language-action-1945539900/
---

**Paper** : [Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models](https://arxiv.org/abs/2603.19233)  
**Source** : arXiv / Accepted at the ICLR Multimodal Intelligence Workshop  
**arXiv ID** : 2603.19233

### Abstract

VLA models combine perception, language, and motor control within a single architecture, but how they transform multimodal inputs into actions remains unclear. This paper applies activation injection, sparse autoencoders (SAEs), and linear probes to six models ranging from 80M to 7B parameters, across four benchmarks totaling over 394,000 rollout episodes. Results show that the visual pathway dominates action generation across all architectures: injecting baseline activations into prompt-free episodes recovers nearly identical behavior, while cross-task injection biases the robot toward the position of the source task (99.8% of episodes in X-VLA align with the source trajectory), revealing action routines that are bound to scene coordinates rather than abstract task representations. Language sensitivity is determined by task structure rather than model design: when the visual context already uniquely determines the task, language is ignored; when multiple goals share the same scene, language becomes critical (in X-VLA's libero_goal task, success rate drops from 94% to 10% under an incorrect prompt, while the libero_object task remains unaffected by prompt correctness, staying at 60-100%). Across three multi-pathway architectures (π0.5, SmolVLA, GR00T), the expert pathway encodes action routines while the VLM pathway encodes goal semantics (behavioral shift caused by expert injection is twice that of VLM injection), and subspace injection experiments confirm that the two occupy separable activation subspaces. Per-token SAE processing is critical to action fidelity for most architectures, but mean-pooling instead improves fidelity on X-VLA. Contrastive identification uncovers 82+ manipulation concepts, and causal ablation experiments show zero-effect ratios ranging between 28%-92%, independent of representation width. The authors release the Action Atlas interactive platform for exploring the representations of the six models.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539900_notallfeatures_fig1.png) 

_Figure 1: Three core findings on pi0.5 — activation injection recovers baseline behavior, cross-task override, and feature attribution_

![Figure]({{ site.baseurl }}/assets/images/1945539900_notallfeatures_fig2.png) 

_Figure 2: Methodology overview — activation recording from VLA backbone/action expert and counterfactual replay_

  * Problem addressed: how the visual, language, and action signals within VLA models are internally divided in labor and encoded, and whether this division of labor generalizes across architectures.
  * Main method: combines three mechanistic interpretability tools — (1) activation injection (replacing the activations of one episode into another to observe behavioral changes and verify causality); (2) sparse autoencoders (SAEs), used to decompose and identify interpretable manipulation-concept features; (3) linear probes, used to test whether specific semantic/task information can be linearly read out from activations. The three approaches corroborate one another and are validated at large scale across six VLA models spanning 80M to 7B parameters, four benchmarks, and nearly 400,000 rollouts.
  * Difference from prior approaches: past studies of internal VLA mechanisms were typically confined to a single model or a single analysis tool, with sample sizes far smaller than this paper's (six models x four benchmarks x nearly 400,000 rollouts), giving this paper's conclusions stronger cross-architecture generality. In addition, the authors specifically distinguish between "visual pathway dominance" and "language pathway dependent on task structure" as two distinct mechanisms — this fine-grained conditional analysis has been rarely addressed in prior research.
  * Key method design: the core pipeline includes: (1) injecting baseline activations from other episodes into "null-prompt" episodes and observing whether behavior is dominated and recovered by visual signals; (2) cross-task injection experiments, injecting activations from a source task into target-task episodes and measuring whether the robot's trajectory is biased toward the source task's location (thereby validating the "spatially bound action routine" hypothesis); (3) for multi-pathway architectures (e.g., π0.5, SmolVLA, GR00T), injecting activations from the VLM pathway and the expert pathway separately, comparing the magnitude of behavioral shift each causes, and using subspace injection to confirm whether the two occupy distinct, separable activation subspaces; (4) comparing the effect of per-token versus mean-pooling SAE preprocessing on action fidelity; (5) using contrastive methods to identify manipulation concepts within SAE features, and testing each feature's importance (zero-effect ratio) via causal ablation.

### Result

  * Key findings/enhancements: the visual pathway dominates action generation across all architectures; language sensitivity is determined by task structure (whether the scene is ambiguous), not by model design; in the three multi-pathway architectures, the expert pathway and VLM pathway are functionally separated and occupy separable subspaces; per-token SAE processing generally outperforms mean-pooling (with X-VLA as the exception); 82+ manipulation concepts were identified, and causal ablation shows that sensitivity varies drastically across features (28%-92% zero-effect rate), independent of representation width.
  * Fairness assessment: this paper's sample size (six models, four benchmarks, nearly 400,000 rollouts) is larger than that of the two previously discussed VLA interpretability papers, theoretically giving its conclusions stronger generality; however, it is a workshop paper (ICLR Multimodal Intelligence Workshop) rather than a formal main-conference paper, so its review rigor may not match that of a formal ICML paper (such as Embodied Interpretability). In addition, this paper was submitted on the same day as SAE for VLA (2603.19183), and the two overlap partially in method and conclusions (both use SAEs to analyze VLA), but whether their specific data corroborate one another requires checking the comparative data in the other paper.

### Limitation

  * The abstract does not explicitly list a limitations section, but plausible weaknesses include: (1) X-VLA shows an exception different from other architectures (mean-pooling outperforms per-token), suggesting the conclusions may not be fully universal across architectures and would need re-validation for each new architecture; (2) the causal ablation zero-effect rate spans an extremely wide range (28%-92%), showing highly uneven feature importance, and how to systematically screen for "key features" remains unresolved; (3) the scale of 840,000 rollouts is enormous, and reproducing this experiment would require substantial computational resources, potentially limiting independent verification by other teams.

### Related work

  * Highly related to the concurrent paper "Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models" (2603.19183); both use SAEs to analyze VLA, and it is worth comparing whether the specific findings of the two papers are consistent.
  * No clearer subsequent follow-up research has been found so far.
  * High survey value: this paper offers the largest-scale cross-architecture mechanistic analysis of VLA to date, and is an important reference benchmark for understanding the "internal division of labor between vision/language/action in VLA."

### Conclusion

  * Overall assessment: this paper systematically analyzes VLA internal mechanisms at large scale and across architectures, providing substantial reference value for understanding practical questions such as "does VLA actually rely on vision or language" (e.g., evaluating a model's out-of-distribution robustness); it is well worth reading in depth.
  * Relationship to other important work: this paper extends and, together with SAE-for-VLA (2603.19183) and Embodied Interpretability (2605.00321), forms the core triangle of 2026 VLA mechanistic interpretability research, while also covering several mainstream VLA architectures such as π0.5, SmolVLA, GR00T, and X-VLA — informative for assessing "which VLA architecture is more mechanistically transparent and better suited for deployment and debugging on specific hardware." As for ROCm/AMD, the paper itself does not mention the training/inference framework or hardware used, so no direct connection is apparent; however, if AMD intends to support large-scale VLA interpretability research in the future (such as activation collection and injection experiments across six models and four benchmarks with nearly 400,000 rollouts), the throughput and batch activation-capture performance requirements of such workloads are worth noting, though the paper does not touch on this and it would need separate evaluation.
