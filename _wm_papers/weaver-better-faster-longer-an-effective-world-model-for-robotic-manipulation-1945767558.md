---
layout: paper
title: "WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation"
section: wm
page_id: "1945767558"
permalink: /wm/weaver-better-faster-longer-an-effective-world-model-for-robotic-manipulation-1945767558/
---

**Paper** : [WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation](https://arxiv.org/abs/2606.13672)  
**Source** : arXiv  
**arXiv ID** : 2606.13672

### Abstract

World models (WMs, i.e., learned simulators) have profound potential impact on robotics—policy evaluation, policy improvement, test-time planning—all achievable with limited real-world interaction. But unlocking these downstream capabilities requires the WM to simultaneously satisfy three requirements: (1) fidelity (producing simulated trajectories relevant to reality), (2) consistency (producing simulated trajectories that are coherent over long horizons), and (3) efficiency (generating simulated trajectories quickly). This paper proposes WEAVER (World Estimation Across Views for Embodied Reasoning), a WM architecture that satisfies all three requirements simultaneously, achieving state-of-the-art results on robotic manipulation tasks. WEAVER is a multi-view WM trained with a flow-matching loss to predict future latents and reward values. The authors distill the key design decisions across model architecture, memory mechanisms, and prediction objectives to unlock long-horizon dynamic manipulation tasks that previous world model approaches struggled to handle. The authors apply WEAVER on real robot hardware, demonstrating its effectiveness in policy evaluation (correlation ρ=0.870 with real-world success rate), policy improvement (38% real-world success rate improvement on the π0.5 robot foundation model), and test-time planning (14% real-world success rate improvement, while being 5-10x faster than prior world models). WEAVER also outperforms prior world models in out-of-distribution scenario evaluations.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767558_weaver_fig1.png) 

_Figure 1: WEAVER — a world model satisfying high fidelity, long-horizon consistency, and efficient generation, enabling policy evaluation, policy improvement, and test-time planning._

![Figure]({{ site.baseurl }}/assets/images/1945767558_weaver_fig2.png) 

_Figure 2: WEAVER architecture — world model encodes memory/history/action for latent rollouts, with a latent verifier (reward + critic heads) steering the policy distribution._

  * Problem being addressed: previous world models struggled to simultaneously satisfy fidelity, consistency, and efficiency—for example, high-fidelity methods tend to be slow (e.g., requiring multi-step diffusion denoising), while fast methods struggle to maintain long-horizon consistency, making it impossible to truly support the policy evaluation, improvement, and test-time planning needed for long-horizon, dynamic robotic manipulation tasks.
  * Main method: WEAVER is a multi-view world model trained with a flow-matching loss that simultaneously predicts future (visual) latents and reward values. The authors systematically distill the key design decisions spanning three dimensions—model architecture, memory mechanism, and prediction objective—to unlock long-horizon, dynamic manipulation tasks that previous world model approaches struggled with.
  * Difference from prior approaches: compared to previous work (including Ctrl-World) that tends to emphasize a single objective (e.g., only long-horizon consistency or only action controllability), WEAVER's core contribution is achieving all three requirements simultaneously, particularly a 5-10x speedup in efficiency while maintaining or even improving fidelity and consistency, and additionally predicting reward values to support test-time planning (rather than merely passively generating frames).
  * Description of key method design: the overall pipeline can be understood as follows—the model takes multi-view observations as input, and through flow-matching (a generative modeling technique that requires fewer steps and generates faster than traditional diffusion models) predicts future latent representations and corresponding reward/progress scores; the memory mechanism design allows the model to retain key scene and object information over long horizons, avoiding the high latency of pixel-level diffusion generation; the prediction objective jointly includes visual latents and reward signals, so the same model can both "imagine" future frames and directly output quantitative scores for use in policy evaluation or candidate action filtering at test time.



### Result

  * Policy evaluation: achieves a correlation of ρ=0.870 with real-world success rate, showing that the world model's scores fairly accurately reflect real-world performance.
  * Policy improvement: 38% real-world success rate improvement on top of the π0.5 robot foundation model.
  * Test-time planning: 14% real-world success rate improvement, while being 5-10x faster than prior world models.
  * In out-of-distribution scenarios, WEAVER also outperforms prior world models.
  * The abstract does not provide a direct numerical comparison with similar papers such as Ctrl-World and τ0-WM (e.g., success rate percentage differences under the same benchmark). This needs to be verified against comparison data from other papers to confirm relative strengths and weaknesses, especially since both WEAVER and Ctrl-World use the π-series or similar robot foundation models as the improvement target, making cross-comparison worthwhile.



### Limitation

  * The abstract does not contain an explicit self-reported Limitation section; this needs to be verified against the full paper (Limitation/Discussion section) to confirm the authors' self-reported limitations.
  * A potential weakness inferred from the results: although the 14% test-time planning improvement and 5-10x speedup appear significant, they are relatively modest compared to the 38% improvement from policy improvement, suggesting there may still be room to improve the efficiency/cost trade-off of test-time planning at this stage. Additionally, the paper focuses on manipulation tasks, and its generalization ability to navigation or more complex multi-object interaction scenarios is not mentioned in the abstract.



### Related work

  * This paper belongs to the same research direction as Ctrl-World (arXiv:2510.10125) and τ0-WM (arXiv:2606.01027)—"world models for robotic manipulation"—and all three focus on policy evaluation and improvement, making them important points of comparison for each other. Ctrl-World in particular also uses a similar π-series robot foundation model as its improvement target, making cross-comparison worthwhile.
  * No newer follow-up research building directly on WEAVER has been found so far (as of currently verifiable information).
  * Worth surveying: high. This paper explicitly proposes and systematically validates the fidelity/consistency/efficiency three-requirement framework, which is valuable for evaluating the methodology of similar world model papers.



### Conclusion

  * Overall assessment: worth referencing. The "fidelity, consistency, efficiency—all three are indispensable" framework proposed by WEAVER has clear value in defining the problem, and its validation data on real robot hardware (ρ=0.870 correlation, 38% success rate improvement, 5-10x speedup) is quite concrete, making it valuable for readers who want to understand what kind of world model design can truly support policy evaluation and improvement.
  * Relationship to other important papers: WEAVER, together with Ctrl-World and τ0-WM, forms an important triangle of 2026 robotic manipulation world model research, each representing different architectural trade-offs (WEAVER emphasizes efficiency and reward prediction, Ctrl-World emphasizes pose-conditioned long-horizon consistency, and τ0-WM emphasizes a unified single backbone for policy and simulation). Comparisons between the three (especially the magnitude of improvement on the same π-series foundation model) are worth further verification and tracking.
  * ROCm/AMD relevance: the paper focuses on world model architecture design and real robot validation, without mentioning the hardware platform used or any ROCm-related content. Based on available information there is no clear connection to ROCm/AMD. To assess the efficiency of flow-matching training and inference on AMD GPUs (especially whether the claimed 5-10x speedup is related to specific hardware optimizations), the full paper would need to be verified to confirm whether it discusses training/inference infrastructure details.
