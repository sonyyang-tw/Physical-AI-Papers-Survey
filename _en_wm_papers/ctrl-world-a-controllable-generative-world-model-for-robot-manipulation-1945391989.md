---
layout: paper
title: "Ctrl-World: A Controllable Generative World Model for Robot Manipulation"
section: wm
page_id: "1945391989"
permalink: /en/wm/ctrl-world-a-controllable-generative-world-model-for-robot-manipulation-1945391989/
---

**Paper** : [Ctrl-World: A Controllable Generative World Model for Robot Manipulation](https://arxiv.org/abs/2510.10125)  
**Source** : arXiv / ICLR 2026 (accepted)  
**arXiv ID** : 2510.10125

### Abstract

Generalist robot policies can already execute a large number of manipulation skills, but evaluating and improving their performance on "unseen objects and instructions" remains difficult: rigorous evaluation requires numerous real-world rollouts, and systematic improvement requires additional, expert-annotated corrective data — both slow, costly, and hard to scale. World models offer a scalable alternative, allowing policies to be rolled out in an "imagination space." This paper proposes Ctrl-World, a controllable, multi-view world model that can be used to evaluate and improve the instruction-following ability of generalist robot policies. The model maintains long-horizon temporal consistency through a pose-conditioned memory retrieval mechanism, and achieves precise action control through frame-level action conditioning. Trained on the DROID dataset (95k trajectories, 564 scenes), the model can generate temporally and spatially consistent trajectories of 20+ seconds in novel scenes and with novel camera viewpoints. The authors demonstrate that this method can accurately rank policy performance without requiring real robot rollouts, and by synthesizing successful trajectories in imagination and using them for supervised fine-tuning, improve policy success rate by 44.7%.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391989_ctrlworld_fig1.png) 

_Figure 1: Ctrl-World overview — policy-in-the-loop rollouts with generalist robot policies for evaluation and improvement._

![Figure]({{ site.baseurl }}/assets/images/1945391989_ctrlworld_fig2.png) 

_Figure 2: Ctrl-World architecture — multi-view joint prediction, pose-conditioned memory retrieval, and frame-level action conditioning._

  * Problem addressed: The cost of evaluating and improving existing generalist robot policies is high (requiring extensive real-world rollouts and expert-annotated corrective data), while existing world models cannot simultaneously support multi-view prediction, fine-grained action control, and long-horizon consistent multi-step interaction — making them insufficient for simulating the deployment scenarios of modern generalist policies.
  * Main method: Ctrl-World is a controllable multi-view world model fine-tuned from a pretrained Stable Video Diffusion (SVD) backbone, with core designs including: (1) a pose-conditioned memory retrieval mechanism to maintain long-horizon (20+ seconds) spatiotemporal consistency even when the camera viewpoint changes or the scene is entirely new; and (2) frame-level action conditioning, letting each generated image frame precisely correspond to a robot action, achieving fine-grained action control.
  * Difference from prior approaches: Compared to prior world models that could only do single-view prediction, had coarse action control, or drifted over long horizons (e.g., IRASim, the main baseline representing prior action-conditioned simulation methods supporting only a single view), Ctrl-World supports multi-view, fine-grained action control, and maintains long-horizon consistency, enabling it to be compatible with and interact with modern generalist policies (such as VLA policies).
  * Key methodological design: The overall pipeline can be understood as follows — the world model uses SVD's image diffusion backbone, with multi-view observations and per-frame action sequences as input; the memory retrieval module retrieves historically relevant visual memory segments based on the current camera pose, serving as a long-range reference when generating new frames, avoiding scene drift or object disappearance during long-horizon rollouts; action conditioning injects the corresponding robot action vector into the generation process for each frame, allowing the model to respond visually to subtle action changes (such as gripper opening/closing, small displacements).



### Result

  * After training on the DROID dataset, the model can generate temporally and spatially consistent trajectories exceeding 20 seconds in novel scenes and camera placements.
  * The world model can accurately rank the performance of different policies (policy evaluation) without requiring real robot rollouts.
  * By synthesizing successful trajectories in imagination space and using them for supervised fine-tuning of policies, success rate can be improved by 44.7%.
  * The abstract and available information do not provide direct quantitative comparisons with other papers (such as similar world models like WEAVER, τ0-WM); verification against those papers' comparison data is needed to confirm Ctrl-World's relative advantages on various metrics (e.g., policy ranking correlation, long-horizon consistency).



### Limitation

  * The paper's abstract and available information do not explicitly state a limitations section; the full text (Limitation/Discussion section) needs to be checked to confirm the authors' self-acknowledged limitations.
  * Potential weaknesses inferred from the results: The training data (DROID, 95k trajectories, 564 scenes) is still distributed according to a specific robot platform/scene distribution, and generalization to entirely different robot morphologies or entirely new task types is unclear; in addition, while the 20-second long-horizon consistency is better than previous methods, there may still be limitations for task planning at longer (minute-scale) time horizons.



### Related work

  * A follow-up work by the same author group (Yanjiang Guo, Chelsea Finn, et al.), VLAW (arXiv:2602.12063), directly cites and builds on Ctrl-World, focusing on using real-world rollout data to iteratively improve world model fidelity, which is then used to further improve the VLA policy — this can be seen as a natural extension of the Ctrl-World concept.
  * The contemporaneous/subsequent work WEAVER (arXiv:2606.13672) is also a world model for robotic manipulation, emphasizing simultaneously satisfying fidelity, consistency, and efficiency, and can be used as a comparison target.
  * Assessment of how worthwhile this is to survey: high. This is one of the important baselines frequently cited by subsequent papers in this subfield (robot manipulation world models).



### Conclusion

  * Overall assessment: worth referencing. Ctrl-World addresses the practical pain point of "generalist robot policy evaluation and improvement being too costly," offering a concrete, feasible solution already validated on real hardware (a 44.7% success rate improvement is quite significant), and it open-sources code and models (Hugging Face, GitHub), providing direct reference value for teams wanting to build evaluation/improvement pipelines.
  * Relationship to other important papers: It is the direct foundation for VLAW (a subsequent work by the same author group) and is also one of the comparison/challenge targets for contemporaneous robot manipulation world model papers such as WEAVER and τ0-WM. It can be seen as one of the representative works of this wave of research on "using world models to evaluate/improve VLA policies."
  * ROCm/AMD relevance: The paper focuses on the architectural design of the world model and robotic data, and does not mention the hardware platform used for training/inference or ROCm-related topics. No clear connection to ROCm/AMD can be identified from the abstract and available information; to evaluate the feasibility of deploying this kind of SVD-based large video diffusion model on AMD GPUs, additional verification of its computational resource requirements (model size, inference latency) would be needed, details which are not explicitly mentioned in the full text.
