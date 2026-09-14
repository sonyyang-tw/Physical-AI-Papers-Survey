---
layout: paper
title: "Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination"
section: wm
page_id: "1945365146"
permalink: /en/wm/dream-mpc-gradient-based-model-predictive-control-with-latent-imagination-1945365146/
---

**Paper** : [Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination](https://arxiv.org/abs/2605.04568)  
**Source** : arXiv (cs.LG / cs.AI / cs.RO), accepted to ICML 2026  
**arXiv ID** : 2605.04568

### Abstract

Dream-MPC proposes a gradient-based model predictive control (MPC) method that combines a learned world model with a policy prior to perform "latent imagination"-style planning. The authors note that current state-of-the-art model-based RL methods either use gradient-free, population-based methods for planning (e.g., MPPI/CEM), use a learned policy network, or a mix of both; while hybrid approaches (MPC + learned model + policy prior) have shown good results, they typically still rely on gradient-free optimization, which is computationally expensive for high-dimensional control tasks. Although gradient-based methods are theoretically more efficient, prior research has shown their practical performance often falls short of gradient-free methods. Dream-MPC rolls out a small number of candidate trajectories from the policy and optimizes each one via gradient ascent using the learned world model, combined with uncertainty regularization and amortization of optimization iterations across time steps (reusing previously optimized actions). Experiments on 24 continuous control tasks show that Dream-MPC substantially improves the performance of the underlying policy and can outperform gradient-free MPC and other SOTA baselines.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945365146_dreammpc_fig2.png) 

_Figure 2: Overview of the proposed approach - Dream-MPC optimizes action sequences rolled out from the policy network in latent space z via gradient-based MPC, with N candidate trajectories sampled and optimized in parallel. (Note: Figure 1 in the paper is a results summary chart rather than a conceptual diagram, so only the method architecture diagram, Figure 2, is embedded here.)_

  * Problem addressed: Gradient-based MPC is theoretically more efficient than gradient-free methods (such as MPPI) in terms of fewer model evaluations, but has historically underperformed in practice; the authors aim to solve the problem of "how to make gradient-based MPC truly outperform gradient-free methods on high-dimensional continuous control tasks."
  * Main method: Dream-MPC draws a small number of candidate trajectories (in latent space z) from rollouts of a policy network π, and optimizes the action sequence of each candidate trajectory via gradient ascent, with the goal of maximizing a value objective J; it also adds uncertainty regularization to avoid overconfidently exploiting the world model's prediction errors, and uses "cross-time-step amortization" to reuse the action sequence already optimized at the previous time step, reducing the computation needed to re-optimize at every step.
  * Difference from prior approaches: Compared to gradient-free methods like MPPI, which require extensive sampling and model evaluations (e.g., N×I×H = 512×6×3 = 9216 model evaluations), Dream-MPC requires only a very small number of candidates and iterations (e.g., 5×1×3 = 15 model evaluations), substantially reducing computational cost. At the same time, using the policy prior to generate the starting point for candidate trajectories allows even a small number of candidates to be optimized effectively, overcoming the previous problem where "gradient-based methods perform poorly without a good initial proposal."
  * Key methodological design: The overall planning process can be described as follows — at each time step, the policy network π produces N candidate action sequences (rollouts), which are unrolled as imagined trajectories in the world model's latent space; each candidate trajectory then undergoes I gradient ascent iterations, exploiting the differentiability of the world model to directly compute gradients with respect to the action sequence to improve the objective value J; the uncertainty regularization term penalizes trajectory branches where the world model's prediction uncertainty is high, avoiding the planner exploiting dead zones of model error. After optimization, the first action of the candidate trajectory with the highest J value is applied to the environment, and the optimization result of this trajectory is retained and amortized to the next time step for continued fine-tuning (rather than optimizing from scratch), thereby spreading the overall optimization time cost across multiple time steps. The method can be integrated with different world model/policy frameworks such as Dreamer, TD-MPC2, DINO-WM, and BMPC (by replacing their planner).



### Result

  * Main results: Across 24 continuous control environments in DeepMind Control Suite, Meta-World, and HumanoidBench, integrating Dream-MPC into TD-MPC2 and BMPC substantially improves the performance of the underlying policy, outperforming the gradient-free MPPI planner and other SOTA baselines; it also demonstrates superior performance to MPPI on image-based observation tasks.
  * Enhancements: Mainly enhances "planning efficiency" (drastically reducing the number of model evaluations, e.g., 15 vs. 9216 as noted above) and "final policy performance"; it is also validated as transferable across multiple model-based RL frameworks (TD-MPC2, BMPC, Dreamer).
  * Fairness assessment: The authors honestly point out an important limitation — on TD-MPC2, although Dream-MPC improves policy performance, it cannot consistently outperform MPPI, showing that gradient-based MPC's dependence on "a high-quality initial policy prior" remains an issue. This shows that its advantage is not uniform across all settings, representing a relatively fair and self-critical presentation. Whether other papers (e.g., ELVIS: Ensemble-Calibrated Latent Imagination for Long-Horizon Visual MPC, a contemporaneous related work) present different comparative results needs further verification.



### Limitation

  * Self-acknowledged limitations in the paper: The authors explicitly mention that (1) fixed optimization parameters (such as the number of iterations, learning rate, etc.) may need to be dynamically adjusted per task to further improve performance; (2) gradient-based MPC requires a high-quality policy prior to plan effectively, but such a prior is not always available; (3) it cannot consistently match MPPI's performance on TD-MPC2.
  * Weaknesses inferred from the results: The method's efficiency advantage rests on the assumption of "few candidates + few iterations." If the policy prior is of poor quality, a small number of candidates may not cover sufficient exploration space, degrading planning quality; in addition, the method's sensitivity to hyperparameters (number of candidates N, number of iterations I) and its robustness across tasks still require broader validation.



### Related work

  * A contemporaneous work (May 2026) was found, ELVIS (Ensemble-Calibrated Latent Imagination for Long-Horizon Visual MPC, arXiv:2605.04709), whose topic is highly related to Dream-MPC (also focusing on latent-imagination-style MPC, but emphasizing long-horizon visual tasks and uncertainty estimation via ensemble calibration), worth comparing against.
  * Assessment of how worthwhile the related work is to survey: medium-high. The direction of combining gradient-based planning with world models remains active (ICML 2026 accepted this paper concurrently); it is recommended to make a cross-comparison of Dream-MPC and ELVIS, and their respective performance on TD-MPC2/Dreamer/BMPC.



### Conclusion

  * Overall assessment: This is a solid, engineering-focused paper centered on "using gradient information to improve MPC planning efficiency." Through the combination of candidate trajectories + gradient ascent + amortized iteration, it drives down the number of model evaluations drastically while maintaining or improving policy performance, offering direct reference value for engineers concerned with real-time control/low-latency inference (such as in robotics or embodied AI systems); its self-acknowledged limitation (dependence on the quality of the policy prior) also makes the assessment more credible.
  * Relationship to other important papers: It extends the Dreamer series (the origin of the latent imagination concept, "Dream to Control: Learning Behaviors by Latent Imagination") and model-based RL frameworks such as TD-MPC2/BMPC, and challenges the efficiency bottleneck of traditional gradient-free MPC (MPPI/CEM) on high-dimensional tasks; it forms a complementary research direction with the contemporaneous ELVIS paper.
  * ROCm/AMD gaps to be strengthened: The paper does not mention specific training hardware platforms, and the abstract contains no ROCm/AMD-related information, so no clear connection can be identified. To deploy this kind of "differentiable world model planning" pipeline on AMD hardware, one would need to independently verify the support level for differentiable simulation and world model backpropagation on the ROCm ecosystem, information which this paper does not provide.
