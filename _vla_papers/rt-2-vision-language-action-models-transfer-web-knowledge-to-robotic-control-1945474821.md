---
layout: paper
title: "RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control"
section: vla
page_id: "1945474821"
permalink: /vla/rt-2-vision-language-action-models-transfer-web-knowledge-to-robotic-control-1945474821/
---

**Paper** : [RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control](https://arxiv.org/abs/2307.15818)  
**Source** : arXiv / Google DeepMind  
**arXiv ID** : 2307.15818

### Abstract

This paper studies how to directly integrate a vision-language model (VLM) trained on internet-scale data into end-to-end robotic control, in order to improve generalization and elicit emergent semantic reasoning capabilities. The authors propose co-fine-tuning a VLM jointly on robot trajectory data and internet-scale vision-language tasks (such as visual question answering), representing robot actions as text tokens so they can be incorporated into the training data in the same way as natural-language tokens. Such models are referred to as vision-language-action (VLA) models. RT-2, proposed in this paper, is built on top of the prior RT-1 model, using two base VLMs (PaLI-X and PaLM-E). Through an extensive evaluation of six thousand trials, RT-2 demonstrates excellent robot policy performance and gains a series of emergent capabilities from internet-scale training, including markedly improved generalization to novel objects, the ability to understand instructions not present in the training data, and preliminary reasoning about user instructions (for example, determining which object to use as an improvised hammer, or which drink to give a tired person).

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474821_rt2_fig1.png) 

_Figure 1: RT-2 overview — robot actions represented as text tokens, co-trained with Internet-scale vision-language data_

![Figure]({{ site.baseurl }}/assets/images/1945474821_rt2_fig2.png) 

_Figure 2: RT-2 generalizes to real-world situations requiring reasoning, symbol understanding, and human recognition_

  * Problem addressed: how to enable a robot policy to have both "end-to-end learning of the mapping from observation to action" and "the benefit of generalization and reasoning from internet-scale language/vision-language pretraining," rather than having to choose between the two.
  * Main method: co-fine-tuning — fine-tuning a pretrained VLM (PaLI-X, PaLM-E) simultaneously on robot demonstration trajectory data and the original internet-scale vision-language tasks (such as VQA), rather than fine-tuning only on robot data (which would cause the model to forget its original web knowledge). Actions are discretized and represented as text tokens, output alongside natural-language tokens, allowing the model to "speak" actions in the same way it generates text.
  * Difference from prior approaches: previous robot learning methods (including the authors' own RT-1) mainly trained only on robot demonstration data and could not leverage internet-scale semantic knowledge; RT-2 is the first method to directly turn a VLM into an end-to-end robot control policy while preserving web knowledge through co-fine-tuning, and as a result gains "emergent capabilities" (such as reasoning about unseen objects) that prior methods lacked.
  * Key method design: architecturally, RT-2 uses PaLI-X (5B / 55B parameters) or PaLM-E (12B parameters) as the base VLM; actions (six-DoF end-effector displacement, rotation, gripper open/close, etc.) are discretized into a finite number of bins, each bin corresponding to a text token; the model takes images and language instructions as input, and part of the output text token sequence represents the action; the training data mixes robot demonstration data collected by RT-1 (13 robots, 17 months, office-kitchen environments) with the original internet-scale vision-language data; the model can also incorporate chain-of-thought reasoning, first producing intermediate reasoning steps before outputting the action.

### Result

  * Key enhancements: RT-2 retains performance on the original training tasks and significantly improves performance on "unseen scenarios," substantially rising from RT-1's 32% to 62%, demonstrating the clear benefit of large-scale pretraining. RT-2 also exhibits emergent capabilities such as chain-of-thought reasoning, generalization to novel objects, and understanding unseen instructions.
  * Fairness assessment: the evaluation scale reaches 6,000 trials, a fairly rigorous scale for robot evaluation; however, as a paper published in-house by Google DeepMind, its comparison baseline (RT-1) is also prior work from the same team, and whether there are independent third-party reproduction results needs to be checked against the comparative data in other papers. The OpenVLA paper (2406.09246) mentions RT-2-X (55B) as a comparison baseline, showing that subsequent research indeed adopts the RT-2 series as a recognized benchmark, which to some extent corroborates the reference value of its results.

### Limitation

  * Limitations stated by the authors or inferable: (1) using an extremely large VLM (PaLI-X with 55B parameters) as the base imposes considerable demands on inference latency and deployment cost, which is unfavorable for real-time control scenarios; (2) representing actions via text-token discretization may have limited expressiveness on tasks requiring high-precision continuous control; (3) the robot demonstrations in the training data are still confined to a specific environment (office kitchen), and its generalization to other more complex, finer-grained manipulation tasks needs to be checked against the full paper.

### Related work

  * The subsequent OpenVLA (arXiv:2406.09246, 2024) directly uses RT-2-X (55B) as a comparison baseline, claiming to surpass RT-2-X by an absolute success rate of 16.5% across 29 tasks while using 7B parameters (7x smaller), showing that the RT-2 series has become a widely recognized important baseline in the VLA field.
  * Subsequent VLA models such as π0 (2410.24164) and GR00T N1 (2503.14734) continue the core idea of "VLM + robot action output," but switch to flow matching / diffusion rather than text-token discretization to output actions, showing this is the direction of technical evolution after RT-2.
  * Extremely high survey value: RT-2 is one of the seminal papers in the VLA research direction; almost all subsequent VLA papers list it as background or a comparison object.

### Conclusion

  * Overall assessment: RT-2 is pioneering work in the VLA field, being the first to demonstrate that directly turning an internet-scale VLM into a robot control policy is feasible and yields significant generalization gains. Its impact on the entire field is profound, and it is essential reading as a foundational paper.
  * Relationship to other important work: RT-2 is regarded by subsequent important work such as OpenVLA, π0, and GR00T N1 as a key background and comparison baseline; subsequent research generally evolves toward "replacing text-token discretization with continuous action-generation methods (diffusion/flow matching)," showing that although RT-2's text-token action representation was pioneering, it has since been surpassed by more refined continuous control methods. As for ROCm/AMD, RT-2's use of an extremely large 55B-parameter VLM places considerable demands on inference hardware memory and compute; if AMD wishes to support inference or fine-tuning of such large VLA models (especially since co-fine-tuning requires simultaneously processing a mixture of robot data and internet-scale data), it is worth paying attention to the maturity of large-model distributed training/inference on ROCm — though the paper itself does not mention the specific training hardware used, this is an inference rather than an explicit statement in the paper.
