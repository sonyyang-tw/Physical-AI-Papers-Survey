---
layout: paper
title: "Aether: Geometric-Aware Unified World Modeling"
section: wm
page_id: "1945539008"
permalink: /en/wm/aether-geometric-aware-unified-world-modeling-1945539008/
---

**Paper** : [Aether: Geometric-Aware Unified World Modeling](https://arxiv.org/abs/2503.18945)  
**Source** : arXiv / ICCV 2025 & ICCV 2025 RIWM Outstanding Paper / Aether Team (Shanghai AI Laboratory, et al.)  
**arXiv ID** : 2503.18945

### Abstract

Integrating geometric reconstruction with generative modeling is a key challenge in developing AI systems with human-like spatial reasoning capabilities. Aether proposes a unified framework that, by jointly optimizing three core capabilities — (1) 4D dynamic reconstruction, (2) action-conditioned video prediction, and (3) goal-conditioned visual planning — equips world models with geometry-aware reasoning. Through task-interleaved feature learning, Aether achieves shared, mutually reinforcing knowledge across the reconstruction, prediction, and planning objectives. Built on top of a video generation model, this framework demonstrates zero-shot "synthetic-to-real" generalization even when it has never encountered real-world data, and achieves zero-shot generalization on both action-following and reconstruction tasks, with reconstruction performance comparable to or better than domain-specific models.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539008_aether_fig1.png) 

_Figure 1: An overview of Aether, trained entirely on synthetic data - highlighting 4D reconstruction, action-conditioned 4D prediction, and visual planning._

![Figure]({{ site.baseurl }}/assets/images/1945539008_aether_fig2.png) 

_Figure 4: The overall pipeline of Aether - with different condition combinations, Aether can serve different tasks._

  * **Problem addressed**: Geometric reconstruction (precise but lacking generative/predictive ability) and generative video models (able to generate but lacking precise geometric consistency) have long been regarded as two separate technical tracks. How to unify the two to support world models with spatial reasoning is the core problem.
  * **Main method**: Aether builds on a video generation model and simultaneously learns 4D dynamic reconstruction, action-conditioned video prediction, and goal-conditioned visual planning, using a task-interleaved feature-learning mechanism so that the three tasks share and mutually reinforce their representations. It also uses camera trajectories as a "geometry-informed action space," so that action-conditioned prediction and visual planning can be driven by geometrically consistent camera motion.
  * **Difference from prior approaches**: Unlike prior methods that only perform reconstruction (without generative/predictive ability) or only perform generation (lacking precise geometric consistency), Aether places all three capabilities within a single jointly optimized training framework, and is trained entirely on synthetic 4D data, using an automated data-annotation pipeline to obtain precise 4D geometric knowledge, yet still generalizes zero-shot to the real world.
  * **Key methodological design**: The overall architecture is built on an existing video generation backbone, interleaving training across three tasks within the same model — "given a video, predict its 4D geometric structure," "given a starting frame and a camera-trajectory action, predict the future video," and "given a start and goal image, perform visual path planning" — while sharing the underlying feature representation. The camera trajectory itself is treated as the action interface, so that when the model performs action-conditioned generation and planning, it naturally carries geometrically consistent constraints.



### Result

  * Even though it never saw real-world data during training (using only synthetic 4D data), Aether achieves zero-shot generalization on both action-following and reconstruction tasks, with reconstruction performance comparable to or better than domain models specifically designed for reconstruction.
  * The paper received the ICCV 2025 and ICCV 2025 RIWM (Robotics in the Wild Models) Outstanding Paper award, indicating a high degree of recognition within the peer-review community.
  * Fairness assessment: The paper provides a project page and code (InternRobotics/Aether), giving it a degree of reproducibility; since this write-up was prepared based only on the abstract and publicly known information, whether its quantitative comparison data are consistent with results reported by other 4D reconstruction/world model papers needs to be verified against those other papers' comparison data.



### Limitation

  * Based on available information, the authors' self-acknowledged limitations include: weaker performance in highly dynamic scenes (e.g., large-scale motion or dense crowds); camera pose estimation that is not sufficiently stable in some cases; and, for visual planning tasks, a recommendation that the spatial/visual distance between the starting observation and the goal image should not be too large, otherwise performance degrades.
  * Trained entirely on synthetic data — while this yields good zero-shot transfer capability, the performance ceiling for real-world complex physical phenomena not covered by synthetic data (e.g., deformable objects, fine-grained contact mechanics) still awaits further real-world validation. The abstract does not provide such details, and further verification of the full text is needed.



### Related work

  * Aether represents an important advance in the "geometry + generation unification" track within the world model field, and along with contemporaneous spatial intelligence models (e.g., related work from World Labs) and subsequent surveys (such as the multiple 2026 world model surveys in this collection), it will likely be listed as a representative method.
  * Assessment of how worthwhile the related work is to survey: high. This "4D reconstruction + action prediction + visual planning" three-in-one framework is an important paradigm repeatedly mentioned across multiple surveys in the world model for robotics field, and is worth following its derivative works.
  * No single newer work directly superseding Aether's position has been identified so far, but the multiple 2026 surveys in this collection (e.g., arXiv:2605.00080, 2606.00113) likely already include Aether in their classification discussions; it is recommended to cross-reference when reading these surveys.



### Conclusion

  * This paper is a representative work in the world model field that fuses geometric reconstruction with generative prediction/planning. Having received the ICCV 2025 Outstanding Paper award, it carries high reference value and is especially suitable as an introductory read for understanding the design philosophy of "4D geometry-aware world models."
  * Relationship to other important papers: This paper can be seen as an integration of and challenge to two tracks — "purely generative video world models (lacking geometric consistency)" and "purely geometric reconstruction models (lacking predictive/planning ability)" — filling the gap between them; it is also frequently cited by subsequent survey papers (such as the world model surveys in this collection) as a key technical milestone.
  * ROCm/AMD relevance: The paper is built on top of a video generation model (possibly based on a diffusion transformer architecture), and the training and inference scale may be quite large. Since the abstract does not mention specific training frameworks or hardware details, its compatibility with the ROCm ecosystem cannot be confirmed, and honestly, no clear connection can be identified. If an AMD team wants to reproduce this kind of unified world model on ROCm, further verification of the extent to which its open-source code supports non-CUDA environments (e.g., the PyTorch ROCm backend) is needed — this is also a common ecosystem maturity gap that ROCm currently faces in training large-scale video generation/4D reconstruction models.
