---
layout: paper
title: "HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL"
section: vla
page_id: "1945364999"
permalink: /en/vla/haf-adapting-generalist-vlas-to-humanoid-whole-body-loco-manipulation-via-hierar-1945364999/
---

**Paper** : [HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL](https://arxiv.org/abs/2608.16837)  
**Source** : arXiv (cs.RO, cs.AI)  
**arXiv ID** : 2608.16837

### Abstract

Humanoid robots are seen as promising general-purpose agents in human-centric environments, but generalist VLA foundation models cannot be directly applied to whole-body loco-manipulation for humanoid robots. The high dimensionality of humanoid actions and the interdependence among body parts make it difficult for traditional single-stage VLA architectures to effectively coordinate locomotion, torso posture, and bimanual manipulation. Furthermore, policies trained via offline behavior cloning may still perform poorly when deployed in the real world; while online reinforcement learning can refine policies through real-world interaction, directly fine-tuning a large VLA backbone requires extremely high computational cost and may introduce safety risks during real-robot exploration. To address these bottlenecks, the authors propose HAF (Humanoid Adaptation Framework), a framework composed of HAF-VLA and HAF-Steer, which transfers off-the-shelf generalist VLA foundation models to whole-body loco-manipulation for humanoid robots. HAF-VLA is a hierarchical action flow generator built on a pretrained flow-matching VLA, which splits the whole-body action denoising process into three sequential stages, using stage embeddings and cross-stage KV caching to preserve kinematic dependencies and avoid the whole-body action incoherence caused by one-shot generation. On top of the frozen HAF-VLA, HAF-Steer is an offline-to-online reinforcement learning pipeline in latent space, which exploits the invertibility of flow matching and DCT-based dimensionality reduction to restrict RL optimization to a compact noise subspace, training a regularized SAC policy. This design avoids updating the massive VLA backbone while still enabling efficient real-world policy refinement. In evaluations across seven real-world humanoid loco-manipulation tasks, HAF outperforms single-stage VLA baselines and improves whole-body coordination and task performance. Project website: <https://grange007.github.io/HAF>

### Method

![Figure]({{ site.baseurl }}/assets/images/1945364999_haf_fig1.png) 

_Figure 1: HAF overview._

![Figure]({{ site.baseurl }}/assets/images/1945364999_haf_fig2.png) 

_Figure 2: HAF VLA pipeline._

  * Problem to be solved: Although generalist VLA foundation models are powerful, they cannot be directly applied to whole-body loco-manipulation for humanoid robots, for two reasons: (1) humanoid actions have high dimensionality, and the various parts (locomotion, torso posture, bimanual manipulation) are highly interdependent, making coordination difficult for single-stage VLA architectures; (2) policies trained via offline behavior cloning may be suboptimal when deployed in the real world, while directly fine-tuning a large VLA backbone with online RL is too costly and carries safety risks.
  * Main method: The HAF framework contains two core components—(1) HAF-VLA: a "hierarchical action flow" generator built on a pretrained flow-matching VLA, which splits the whole-body action denoising process into three sequential stages (presumably corresponding to lower-body locomotion, torso posture, and bimanual manipulation, though the abstract does not explicitly specify what each of the three stages corresponds to—this requires verification against the full paper), using stage embeddings and cross-stage KV caching to preserve kinematic dependencies between stages; (2) HAF-Steer: layered on top of the frozen HAF-VLA, an offline-to-online RL pipeline in latent space that exploits the invertibility of flow matching along with discrete cosine transform (DCT)-based dimensionality reduction to restrict RL optimization to a compact "noise subspace," training a regularized SAC (Soft Actor-Critic) policy.
  * Difference from prior approaches: Unlike the traditional approach of a "single-stage VLA generating whole-body action in one shot," HAF-VLA adopts a staged, sequentially dependent action generation process, avoiding the whole-body action incoherence caused by one-shot generation. Unlike the traditional approach of "directly fine-tuning the VLA backbone with online RL," HAF-Steer freezes the large VLA backbone and performs RL optimization only within a compact, dimensionality-reduced latent noise subspace, substantially reducing the computational cost and exploration risk required for fine-tuning.
  * Key method design description: The entire system can be thought of as a "generation + fine-tuning" two-tier architecture: the underlying HAF-VLA is like a staged assembly line, where action generation flows sequentially through three processing stations, each marked with its own role via "stage embeddings," with cross-stage KV caching (similar to carrying key information from the previous station's processing results to the next) ensuring that downstream actions remain kinematically consistent with upstream decisions, avoiding odd, uncoordinated hand-foot motions. The upper HAF-Steer layer is like a "correction module" installed at the end of the assembly line—it does not modify the assembly line itself (freezing HAF-VLA), but first uses flow matching's invertibility to "invert" the generation process back into a noise space, then uses DCT to compress this noise space into a low-dimensional subspace, and finally trains an SAC policy within this small space for real-time correction. This allows online adjustment using real-world feedback without incurring the cost and risk of retraining the entire large model.

### Result

  * Evaluations across seven real-world humanoid loco-manipulation tasks show that HAF outperforms "vanilla single-stage VLA baselines," improving whole-body coordination and task performance. The abstract does not provide specific quantitative figures (such as success rate percentages or improvement margins); the full paper's experimental tables need to be checked to understand the specific degree of enhancement.
  * Whether the results are fair: Comparison data from other papers needs to be checked; the comparison target in the abstract is limited to "vanilla single-stage VLA baselines," with no direct comparison to WholeBodyVLA (also targeting humanoid whole-body loco-manipulation), a contemporaneous paper. The two papers were published around the same time (HAF slightly later) but do not cite each other, so whether there is a substantive performance difference requires verification against the full paper or subsequent literature.

### Limitation

  * The abstract does not contain an explicit limitations section; the full paper needs to be checked to understand under which task types or action complexity levels the framework's performance is limited, and whether the three-stage action flow split is applicable to all humanoid tasks.
  * Potential weaknesses inferred from the method design: while restricting RL optimization within HAF-Steer to a compact noise subspace reduces computational cost and safety risk, it may also limit the upper bound of the degrees of freedom the policy can explore and correct, potentially offering limited improvement for tasks that require large deviations from the pretrained distribution; furthermore, validation is limited to only seven real-world tasks, a relatively small number, so the breadth of its generalization ability requires further verification.

### Related work

  * Highly related to WholeBodyVLA (arXiv:2512.11047) from the same batch of papers; the two represent two different solutions to the same problem domain (adapting generalist VLAs to humanoid whole-body loco-manipulation) published around the same time, and are worth comparing: WholeBodyVLA focuses on "learning loco-manipulation knowledge from human video + a specialized RL controller," while HAF focuses on "freezing a pretrained flow-matching VLA + staged action flow + latent-space offline-to-online RL."
  * No direct follow-up work newer than HAF has been found so far (this paper was submitted in August 2026, one of the more recently published papers in this batch).
  * Highly worth surveying as related work: VLA adaptation for humanoid whole-body loco-manipulation is a rapidly developing hot subfield; it is recommended to read HAF and WholeBodyVLA together to grasp the two current mainstream technical approaches to this problem.

### Conclusion

  * Overall assessment: HAF proposes a technically clever two-stage solution (staged action flow generation + compact latent-space RL fine-tuning), providing a concrete solution to the practical pain point that "large VLA backbones are difficult to fine-tune online safely and efficiently." It is worth referencing, especially for teams that want to perform online policy refinement on real robots while avoiding retraining the entire large model.
  * Relationship with other important papers: Together with WholeBodyVLA (arXiv:2512.11047), it forms two contrasting solutions to the same problem domain; whether the flow-matching invertibility and DCT dimensionality reduction techniques used by HAF-Steer further challenge or extend other latent RL papers requires checking the full paper's related work section.
  * Regarding ROCm/AMD: No clear direct connection to ROCm/AMD is apparent; the paper focuses on robot action generation architecture and reinforcement learning algorithm design and does not mention specific training/inference hardware platform choices. However, HAF-Steer's design philosophy of "avoiding updates to the large VLA backbone, performing RL only within a compact subspace" could, in theory, reduce reliance on large-scale distributed training infrastructure if deployed on an AMD/ROCm platform—but this is speculative, and the abstract itself provides no specific details supporting this judgment.
