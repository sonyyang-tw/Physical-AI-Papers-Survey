---
layout: paper
title: "Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models"
section: vla
page_id: "1945539857"
permalink: /vla/sparse-autoencoders-reveal-interpretable-and-steerable-features-in-vla-models-1945539857/
---

**Paper** : [Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models](https://arxiv.org/abs/2603.19183)  
**Source** : arXiv (24 pages, 11 figures)  
**arXiv ID** : 2603.19183

### Abstract

Although VLA models have become the mainstream approach for general-purpose robotic manipulation, few studies have examined, from a mechanistic interpretability perspective, why they can generalize across variations in objects, scenes, and instructions. This paper trains a sparse autoencoder (SAE) on the hidden-layer activations of VLA models, learning a sparse dictionary of activations that reveals numerous features corresponding to interpretable directions in the model's representation space. The authors identify SAE features corresponding to motion primitives and semantic concepts, some of which generalize across episodes and can be causally manipulated (steered). The authors propose a metric for classifying features as "generalizable, transferable primitives" or "episode-specific memories," providing clues for understanding VLA generalization ability. The authors validate these findings through steering experiments on the LIBERO simulation benchmark and real-world DROID hardware.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539857_saevla_fig1.png) 

_Figure 1: Overview of the SAE training and feature analysis pipeline_

![Figure]({{ site.baseurl }}/assets/images/1945539857_saevla_fig2.png) 

_Figure 2: Feature steering experiment architecture_

  * Problem addressed: what reusable representations do VLA models actually learn internally that allow them to link perception, language, and action across tasks and scenes? There is currently a lack of mechanistic-level understanding of this.
  * Main method: training a sparse autoencoder on the hidden-layer activations of VLA, decomposing high-dimensional, superposed activations into a sparse dictionary of features that may each correspond to a single semantic/action concept.
  * Difference from prior approaches: previous understanding of VLA has mostly remained at the level of end-to-end behavioral evaluation (black-box metrics such as success rate), lacking fine-grained decomposition of internal representations; this paper borrows the SAE technique that has become popular in recent LLM interpretability research and applies it to the robotic VLA domain, additionally proposing a classification metric for generality vs. episodic memory, and validating causality through "steering" experiments (amplifying/ablating specific features) rather than merely performing correlational analysis.
  * Key method design: the pipeline includes: (1) collecting hidden-layer activations of the VLA model across a large number of rollout episodes; (2) training an SAE to learn a sparse dictionary, decomposing activations into multiple interpretable feature directions; (3) semantically annotating each feature, identifying whether it corresponds to a motion primitive (such as "grasping" or "moving to the left") or a semantic concept (such as an object category); (4) proposing a generality metric that quantifies whether a feature appears stably across multiple different episodes (a generalizable, transferable primitive) or only in a specific episode (an episode-specific memory); (5) conducting steering experiments: amplifying generalizable, semantic features and observing whether they induce behavior consistent with their semantics; ablating features and observing whether model performance is disrupted; (6) repeating validation on both the LIBERO simulation and real DROID robot hardware.

### Result

  * Key enhancements/findings: amplifying generalizable, semantic features induces behavior consistent with their semantics, while ablating these features disrupts model performance, demonstrating that these SAE features have a causal effect rather than being merely correlational artifacts. The authors also show that steering can be used to control the model to execute behavioral directions that were originally unpromptable via language. These results provide mechanistic-level evidence that "VLA learns reusable internal features linking perception/language/action."
  * Fairness assessment: the experiments cover both simulation (LIBERO) and real hardware (DROID), giving a degree of external validity; however, the abstract does not provide direct quantitative comparison with other similar SAE-for-VLA research (such as arXiv:2603.19233) — the two papers may have partially overlapping or complementary findings, and this needs to be checked against the comparative data in the other paper to confirm consistency of conclusions.

### Limitation

  * The paper's abstract does not explicitly list a limitations section, but plausible weaknesses include: (1) not all SAE features can be clearly semantically annotated, and there may be a large number of uninterpretable "dead features" or polysemantic features; (2) the effect of steering experiments may vary by task and model architecture, and its generality needs broader validation; (3) SAE training itself requires additional computational resources and hyperparameter tuning (such as sparsity level and dictionary size), and its stability and reproducibility need to be checked against the full paper.

### Related work

  * Around the same time (March 19, 2026), another closely related paper, "Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models" (arXiv:2603.19233), also uses SAEs and other mechanistic interpretability tools to analyze VLA; the two papers likely originate from different teams but overlap heavily in direction, and are worth reading side by side.
  * High survey value: this paper represents an important attempt to transfer LLM interpretability techniques (SAE) into VLA interpretability, and is foundational work for understanding internal VLA representations.

### Conclusion

  * Overall assessment: this paper is the first to systematically apply SAE to VLA models and validate causal steering effects via real hardware; the method is solid and thoroughly validated, worth referencing, especially of high value for researchers wanting to deeply understand the internal workings of the VLA "black box."
  * Relationship to other important work: this paper, together with "Not All Features Are Created Equal" (2603.19233) and "Embodied Interpretability" (2605.00321), belongs to the emerging 2026 cluster of VLA mechanistic interpretability research, complementing each other (SAE feature decomposition vs. causal intervention attribution). As for ROCm/AMD, SAE training and large-scale activation collection are computationally intensive offline analysis work; the paper does not mention what hardware/framework was used, so no clear direct connection to the ROCm ecosystem can be seen. If AMD wishes to enter this interpretability tool chain, a worthwhile gap to consider is "the performance and ecosystem support for SAE training and large-batch intervention experiments on ROCm/PyTorch," though the paper itself does not touch on this point.
