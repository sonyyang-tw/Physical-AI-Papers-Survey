---
layout: paper
title: "IMLE-VLA: Fast Single-Step Action Generation for Vision-Language-Action Policies"
section: vla
page_id: "1960020599"
permalink: /en/vla/imle-vla-fast-single-step-action-generation-for-vision-language-action-policies-1960020599/
---

### Abstract

IMLE-VLA proposes a single-step action generation head trained with conditional Implicit Maximum Likelihood Estimation (cIMLE), designed to replace the diffusion / flow-matching action heads commonly used in VLA models. Current mainstream designs (such as π0.5) rely on multi-step iterative sampling (e.g., 10 Euler steps), causing inference latency, "stop-and-go" discontinuous robot motion, and reduced task completion speed. The cIMLE objective preserves multimodal coverage of actions (avoiding the mode collapse common to simple regression heads) while completely eliminating multi-step sampling. Applying IMLE-VLA to π0.5 boosts inference frequency by 3.67x (55Hz vs. 15Hz), with action throughput improved by up to 11x. On the 40-task LIBERO benchmark, IMLE-VLA achieves the highest average success rate among all baselines (98.0%), while maintaining the highest inference frequency; under test-time perturbations in LIBERO-plus, IMLE-VLA maintains π0.5's original robustness, while other fast baselines degrade noticeably. Real-world experiments on a Franka Emika Panda arm across four tasks show smoother motion (jerk reduced by 2.2-3.0x), faster task completion, and IMLE-VLA outperforms π0.5 on every task, with average per-episode VLA inference time reduced by 3.9-6.6x. The paper has been accepted at IEEE/RSJ IROS 2026.

### Method

**Problem addressed:** A common VLA policy design pairs a pretrained VLM backbone with a separate continuous action head trained via diffusion or flow matching. Such action heads rely on multi-step iterative denoising sampling (π0.5 uses 10 Euler steps), causing a pronounced inference bottleneck: robots exhibit stop-and-go motion patterns, task completion speed decreases, and high-frequency closed-loop control becomes difficult to achieve.

**Main method:** The authors propose training a single-step conditional generator with conditional Implicit Maximum Likelihood Estimation (cIMLE), directly replacing the original iterative action head. The core idea of cIMLE is: for each condition (observation + language instruction), sample m candidate actions from latent noise, and only apply gradient updates to the sample "closest" to the true demonstrated action (a nearest-neighbor style loss). This preserves single-step generation (no iterative denoising required) while still capturing the multimodality of the action distribution, avoiding the mode collapse commonly seen with simple L2 regression heads.

**Differences from prior approaches:** Unlike diffusion/flow-matching action heads (which require multi-step iterative solving of an ODE/SDE), the cIMLE action head generates a complete action with just a single forward pass at inference time. Architecturally, it is a "plug-and-play" replacement for π0.5's original flow-matching action head, while the rest of the VLM backbone and training data remain unchanged; thus the modification is concentrated on the action generation mechanism itself, rather than a full system redesign.

**Key method illustrations:** Fig. 1 (embedded below) shows the overall architecture of IMLE-VLA as a "plug-and-play" single-step action head replacing the original iterative module; Fig. 5 (embedded below) shows qualitative comparisons across three real-world experiment categories (single-step manipulation, multi-step sequential reasoning, dynamic reactive tasks), showing that IMLE-VLA produces faster, smoother motion with higher success rates.

![Figure]({{ site.baseurl }}/assets/images/1960020599_imle_overview.png) 

_Fig. 1: Overall IMLE-VLA architecture — replacing the iterative diffusion/flow-matching action head with a single-step cIMLE action head_

![Figure]({{ site.baseurl }}/assets/images/1960020599_imle_experiments.png) 

_Fig. 5: Qualitative comparison across three real-world task categories (single-step manipulation, multi-step sequential reasoning, dynamic reactivity)_

### Result

**Main improvements:** (1) Inference frequency increases from π0.5's 15Hz to 55Hz (3.67x); under an execution horizon of H=10, action throughput improves by up to 11x. (2) On the 40-task LIBERO benchmark, average success rate is 98.0%, the highest among all baselines, while still maintaining the fastest inference frequency. (3) Under distribution-shift testing on LIBERO-plus, other fast baselines' success rates degrade severely as perturbation increases, while IMLE-VLA maintains robustness close to that of the original π0.5. (4) Across four real-world Franka Panda tasks, IMLE-VLA outperforms π0.5 on every task, reducing action jerk by 2.2-3.0x and per-episode VLA inference time by 3.9-6.6x.

**Fairness of results:** The paper's comparison baselines (π0.5, other single-/few-step baselines) are all recent, strong public baselines, and both simulation and real-robot experiments are reported, along with ablations over different execution horizons and the cIMLE sampling factor m (Fig. 3, Fig. 4), showing that the authors have thoroughly accounted for result robustness. The real-world experiment sample size is 20 episodes per task, a moderate but reasonable scale; no obvious contradictions were found with numbers reported by other papers (e.g., the original π0.5 paper), and the 98.0% LIBERO success rate is roughly consistent with the success rate range (95-99%) reported for high-performing VLA models in recent literature.

### Limitation

**Known limitations:** cIMLE relies on the sampling factor m (the number of candidate actions drawn per condition during training) for multimodal coverage; when m=1, it degenerates into standard regression (losing multimodal capability), showing the method is fairly sensitive to hyperparameter choice. The paper does not discuss whether this method retains its advantage on more complex, long-horizon tasks requiring explicit multi-stage reasoning (such as the hierarchy/reasoning-category papers elsewhere on this page).

**Weaknesses inferred from the results:** Real-world experiments cover only four tasks, a single robotic arm (Franka Panda), and a single GPU (A6000); transferability across embodiments (e.g., humanoid, dual-arm) remains unverified. In addition, the optimal execution horizon H=10 was selected specifically for LIBERO, and whether it is optimal for all downstream tasks still requires further validation.

### Related work

This page already includes several closely related papers focused on "efficiency/single-step generation," such as SnapFlow (which compresses flow-matching to a single step via progressive self-distillation) and Let It Be Simple (which challenges the assumption that "single-step generation is hard"). IMLE-VLA stands in direct comparison to both within this same sub-topic, and can be read together to compare the strengths, weaknesses, and applicable scenarios of different single-step generation strategies (self-distillation vs. cIMLE). It is worth tracking whether more follow-up work applying cIMLE / implicit maximum likelihood estimation to robot action generation appears on arXiv.

### Conclusion

IMLE-VLA is a methodologically concise and solidly validated paper: it clearly identifies the core tradeoff between "single-step generation" and "multimodal coverage," and offers a relatively elegant solution via cIMLE, accompanied by complete validation in both simulation and real robots. Having been accepted at IROS 2026, it is well worth referencing. It forms a triangular comparison with SnapFlow and Let It Be Simple under this page's "Architecture Paradigms" sub-topic, together depicting the trend of VLA action heads evolving toward "single-step, high-frequency inference"; with π0.5 (the base model), it forms a direct "efficiency-enhancing plugin" relationship. For ROCm/AMD, the gap this type of paper highlights is that current mainstream VLA inference performance evaluation and optimization (such as this paper's L40S GPU benchmark) is almost entirely based on the NVIDIA ecosystem. AMD still lacks public VLA inference latency/throughput benchmarks and corresponding ROCm optimization case studies, which is worth pursuing as a future improvement direction.
