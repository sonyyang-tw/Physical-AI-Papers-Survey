---
layout: paper
title: "ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models"
section: vla
page_id: "1968562502"
permalink: /vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/
---

### Abstract

ACoT-VLA (arXiv:2601.11404, accepted at CVPR 2026, AgiBot) proposes the "Action Chain-of-Thought" (ACoT) paradigm: letting VLA reasoning happen directly in action space, rather than relying on indirect intermediate representations such as language sub-task prediction or goal-image synthesis. The authors observe that existing explicit intermediate reasoning (language sub-tasks, visual goal images) has limited capacity to convey the fine-grained information required for precise action execution. The ACoT-VLA architecture consists of two complementary components: an Explicit Action Reasoner (EAR) that proposes a coarse reference trajectory as an explicit action-level reasoning step, and an Implicit Action Reasoner (IAR) that extracts implicit action priors from the internal representations of multimodal inputs. Together they form the ACoT that conditions the downstream action head, enabling grounded policy learning. Extensive real-world and simulation experiments show this method outperforms existing baselines; code is open-sourced on GitHub (AgibotTech/ACoT-VLA).

### Method

**Problem addressed**: Traditional VLA maps multimodal inputs directly to actions via VLM embeddings, without an explicit reasoning step; recent methods introduce language sub-task prediction or goal-image synthesis as intermediate reasoning, but such indirect representations inherently struggle to carry the complete, fine-grained information required for precise action execution.

**Main method**: The paper proposes the Action Chain-of-Thought (ACoT) paradigm, arguing that the most effective reasoning should happen directly in action space. The concrete architecture includes: (1) Explicit Action Reasoner (EAR): a Transformer module that proposes a coarse reference trajectory as an explicit action-level reasoning step; (2) Implicit Action Reasoner (IAR): extracts implicit action priors from internal features of a shared VLM backbone; the outputs of both jointly form the ACoT and condition the final action-generation head, giving action generation a traceable reasoning chain.

**Difference from prior approaches**: Unlike Language CoT (e.g., LoHoVLA, DualCoT-VLA, which use language sub-tasks as an intermediary) and Visual CoT (which uses synthesized goal images as an intermediary), ACoT-VLA's reasoning happens directly in action space (coarse trajectories), avoiding the information loss that language/image intermediate representations incur when conveying fine-grained action information — a third CoT-space approach not yet covered on this page.

**Key method figures**: Figure 1 compares three CoT paradigms (language space, visual space, action space); Figure 2 shows the full ACoT-VLA architecture, including how the EAR and IAR modules on a shared VLM backbone jointly condition the downstream action head.

![Figure]({{ site.baseurl }}/assets/images/2601.11404_acot_fig1.png)

_Figure 1: Comparison of three CoT paradigms (language space, visual space, action space)_

![Figure]({{ site.baseurl }}/assets/images/2601.11404_acot_fig2.png)

_Figure 2: Full ACoT-VLA architecture — how the EAR and IAR modules jointly condition the downstream action head_

### Result

**How the results turned out**: The paper conducts extensive experiments in both real-world and simulated environments, showing ACoT-VLA outperforms existing VLA baselines (including direct mapping and existing language/visual CoT methods); it has been accepted at CVPR 2026, indicating peer review has validated the completeness and contribution of its experiments.

**Are the results fair**: Since this is the CVPR-accepted version, the experimental design and baselines should have passed peer review; however, this harness only obtained the arXiv abstract and the public description in the HTML version, and did not individually verify whether the number of real-robot tasks and specific success-rate figures are directly comparable to other papers (e.g., LoHoVLA, DualCoT-VLA already on this page) under the same benchmark, so it cannot be asserted whether the results are fully consistent with other papers' results.

### Limitation

**Known limitations**: The abstract and method description do not explicitly disclose the risk of accumulated error from EAR's "coarse reference trajectory" in complex long-horizon tasks, nor do they discuss a fault-tolerance mechanism for when the EAR and IAR reasoning paths disagree.

**Weaknesses inferred from results**: As a CVPR 2026 paper, the abstract-level description is relatively concise; experimental details (e.g., the specific list of evaluation tasks, cross-embodiment generalization) require consulting the full text for further assessment; this entry can only reflect abstract-level information.

### Related work

Newer related work on arXiv: DualCoT-VLA (2603.22280), DeepThinkVLA (2511.15669), and Latent Reasoning VLA (2602.01166), already covered on this page, all belong to the language/latent CoT line, forming a contrast with ACoT-VLA's "action-space CoT" line — worth cross-comparing the trade-offs of the three CoT spaces.

Worth surveying: High. The "action-space reasoning" proposed by ACoT is a relatively novel sub-direction not yet fully covered on this page; if future papers extend this line (e.g., combining it with world models for look-ahead verification of action trajectories), it is worth continued tracking.

### Conclusion

**Overall assessment**: ACoT-VLA proposes a conceptually clear, methodologically distinct new CoT paradigm (action-space reasoning vs. existing language/visual-space reasoning), has passed CVPR 2026 peer review, and comes from a robotics research team of AgiBot's scale — worth including as a reference for the VLA hierarchical reasoning/CoT sub-topic.

**Relationship to other important papers**: Together with LoHoVLA (a unified backbone for high/low-level planning), DualCoT-VLA (parallel visual + language CoT), and Latent Reasoning VLA (latent CoT) under this page's "Hierarchy: High-Level Planning/Reasoning" topic, it forms a spectrum of different solutions within the same problem space; ACoT-VLA's "action-space CoT" can be seen as a methodological complement to existing language/visual CoT lines. ROCm/AMD gap: current open-source efforts on training/inference acceleration for VLA action heads mostly focus on diffusion/flow-matching action heads; public information on optimizing the inference pipeline of ACoT-VLA's three-stage "dual reasoner (EAR+IAR) + action head" architecture — especially how EAR's autoregressive coarse-trajectory generation and IAR's implicit feature extraction can run efficiently in parallel on ROCm — is currently limited, representing an opportunity for AMD to engage with this class of hierarchical VLA inference optimization.
