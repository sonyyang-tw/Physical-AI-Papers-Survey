---
layout: paper
title: "Decoding Task Progress from VLA Representations"
section: vla
page_id: "1945539940"
permalink: /en/vla/decoding-task-progress-from-vla-representations-1945539940/
---

**Paper** : [Decoding Task Progress from VLA Representations](https://arxiv.org/abs/2608.13474)  
**Source** : arXiv  
**arXiv ID** : 2608.13474

### Abstract

VLA models are rapidly moving toward deployment as general-purpose manipulation policies, but basic tools for understanding their internal representations or monitoring their state at runtime are still lacking. This paper draws on ideas from mechanistic interpretability to probe the residual stream of the π0.5 model, finding that "task progress" (i.e., the normalized fraction of time remaining in a trajectory) can be linearly read out from the activations. The authors find that this signal already exists before the PaliGemma backbone has been trained on any robot-specific data. A single linear probe generalizes to unseen tasks, and when trained on multi-prompt data it varies with language counterfactuals, but it cannot effectively steer policy behavior. These properties make the signal directly usable for monitoring already-deployed VLAs. The authors use this probe as a label-free out-of-distribution (OOD) detector capable of detecting stalled task progress, and find that its performance is comparable to state-of-the-art methods.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539940_taskprogress_fig1.png) 

_Figure 1: Task progress is linearly readable from pi0.5 internal activations via a linear probe on residual-stream activations_

![Figure]({{ site.baseurl }}/assets/images/1945539940_taskprogress_fig2.png) 

_Figure 2: Decodability of the progress feature across layers (SigLIP, PaliGemma Gemma backbone, action expert) and probe performance vs. capacity_

  * Problem addressed: Deployed VLAs lack tools for monitoring their internal state — for example, there is no way to know whether the model is "stuck" or whether the task is progressing normally — which is a major gap for safe deployment.
  * Main method: Borrowing the linear-probe method from mechanistic interpretability, the authors train a simple linear classifier/regressor on the residual-stream activations of the π0.5 model to predict "task progress" (the normalized fraction of time remaining in the trajectory).
  * Difference from prior approaches: Previous methods for runtime monitoring of VLAs have often relied on additional labeled data or specially trained anomaly-detection models; this paper instead demonstrates that the semantic quantity of "task progress" is already implicit in the model's existing activations (even present in the pre-trained PaliGemma backbone before it has seen any robot data), and can be read out with just a simple linear probe, without requiring additional labels or retraining the entire model.
  * Description of the key methodological design: The pipeline includes: (1) collecting residual-stream activations while the π0.5 model performs various manipulation tasks; (2) training a linear probe with "normalized time remaining" as the regression target; (3) verifying whether this signal already exists in the pre-trained PaliGemma backbone (without robot-data fine-tuning); (4) testing the probe's sensitivity to language counterfactuals on multi-prompt data; (5) attempting to use the probe direction to steer policy behavior, to test whether it has causal control power; (6) packaging the probe as a label-free OOD/stall detector and comparing it against existing state-of-the-art (SOTA) detection methods.

### Result

  * Main findings: the task-progress signal can be linearly read out and generalizes to unseen tasks; this signal already exists at the pre-trained backbone stage, showing that this kind of semantic quantity is not something that only emerges after robot-data fine-tuning; the probe is sensitive to language counterfactuals (indicating it does reflect task semantics), but **cannot** be used to effectively steer policy behavior (steering fails), showing that "a readable signal" is not equivalent to "a steerable signal" — the two properties are separate. As an OOD detector, this linear probe's performance is comparable to state-of-the-art methods.
  * Fairness: The paper compares its own simple linear-probe method against "state-of-the-art OOD detection methods" and claims competitiveness, but the abstract does not list specific numerical values or the names of the baseline methods compared; whether this is fair, and whether other papers reach different conclusions, would need to be verified against other papers' comparative data.

### Limitation

  * Self-stated limitations: although the probe can read out task progress and be used for detection, it **cannot be used to steer policy behavior** (steering is ineffective), indicating that while this signal is "readable" it is not a causal driver of policy decisions, limiting its application scope to monitoring/detection rather than active intervention.
  * Weaknesses inferred from the results: the method has only been validated on a single model architecture, π0.5; whether it generalizes to other VLA architectures (e.g., OpenVLA, GR00T, SmolVLA) is unknown, and the full text or follow-up research would need to be checked to confirm this. In addition, "task-progress stall detection" as an OOD-detection approach may fail to detect failure modes other than "stalling" (e.g., a task proceeding in the wrong direction while still advancing); the paper does not discuss the coverage of such failure modes.

### Related work

  * This paper is highly related to Tri-Info (arXiv:2606.19998, which likewise focuses on VLA failure detection); both attempt to detect runtime anomalies from internal model signals (rather than an additionally trained detector), making it worth comparing the two in terms of detection accuracy and generalization ability.
  * No newer direct follow-up research has been found so far.
  * Degree to which it merits surveying: high. This paper provides a lightweight, interpretable VLA monitoring method that requires no additional labels, and has direct practical reference value for engineering teams that wish to deploy VLAs in production (including teams considering deploying inference on AMD hardware).

### Conclusion

  * Overall assessment: This paper presents a simple but insightful finding — that a task-progress signal is already implicit in the pre-trained VLM backbone — and demonstrates its practical value for safety monitoring. It is a compact but practically meaningful piece of work, worth referencing, especially for engineers concerned with deployment reliability and runtime monitoring.
  * Relationship to other important papers: This paper belongs to the same sub-field as Tri-Info (2606.19998) — "runtime failure detection/monitoring of VLAs" — and the two are complementary (linear probe vs. information-theoretic signal); it is also directly related to π0/π0.5 (Physical Intelligence's flagship models), since π0.5 is the analysis target of this paper. Regarding ROCm/AMD, if an AMD team is exploring deploying VLA inference services on its own hardware, this type of "lightweight linear-probe monitoring" method, having extremely low computational cost (requiring only an additional linear-layer forward pass), is relatively easy to implement on any inference framework (including PyTorch/vLLM etc. on ROCm), and can be regarded as a low-cost, high-return direction for enhancing runtime observability; however, the paper itself does not discuss any hardware or framework-level issues, so this inference is an extrapolated judgment rather than an explicit conclusion of the paper.
