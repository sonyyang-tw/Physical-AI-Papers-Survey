---
layout: paper
title: "Spatially Aware World Action Model via Geometric Latent Diffusion"
section: wm
page_id: "1946673367"
permalink: /en/wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/
---

### Abstract

World Action Models (WAMs) leverage large-scale pretrained video diffusion models to jointly predict future observations and actions, inheriting rich visual and physical priors from web-scale video, making them a promising paradigm for robot policy learning. However, existing methods almost exclusively operate on RGB observations, failing to leverage 3D information. This paper proposes the Spatially Aware World Action Model (SA-WAM), which adapts a pretrained video model to jointly predict actions, RGB, and depth, achieving 3D-aware world modeling and action prediction within a single diffusion backbone network. The authors design a nonlinear encoding that maps unbounded depth signals into the bounded input domain expected by a frozen VAE tokenizer, allowing the tokenizer to be reused without any 3D-specific fine-tuning, incorporating geometric information without sacrificing the pretrained priors. SA-WAM achieves state-of-the-art results on the RoboCasa and LIBERO-Plus benchmarks while also improving the quality of future state predictions; furthermore, in real-world UR5 robotic arm evaluations, it shows significant improvement over strong baselines under randomized environments. The authors also analyze the correlation between world model prediction quality and rollout success rate, providing insight into WAM performance and directions for improvement.

![Figure]({{ site.baseurl }}/assets/images/1946673367_diagram_sa-wam.png) ![Figure]({{ site.baseurl }}/assets/images/1946673367_robocasa_fig3.png) 

### Method

  * **Problem addressed**: Existing World Action Models (such as methods like Cosmos-Policy) all operate only in RGB observation space, lacking explicit 3D/depth information, which limits their ability to model object geometry and spatial relationships, in turn limiting the generalization and grasping precision of policies under randomized real-world scenarios.

  * **Main method**: SA-WAM adapts a pretrained video diffusion model (Diffusion Transformer, DiT) into a model that "jointly predicts action, RGB, and depth." Specifically, proprioception (q_t) and the action chunk (a_t) are inserted directly at dedicated positions within the latent sequence; the conditioning signals include the task description (task), one RGB frame per view (v_t^c) interleaved with its corresponding 3D modality (depth g_t^c), and the current proprioception information. The depth signal is mapped into the bounded input domain expected by a frozen VAE tokenizer via a nonlinear encoding scheme, so that the same RGB VAE tokenizer can be directly reused to process depth, without requiring an additional 3D-specific encoder or fine-tuning the tokenizer for 3D. The denoising process operates on the action chunk, future RGB (v_t'^c), and future depth (g_t'^c); the decoding stage is optional at inference time.

  * **Difference from prior approaches**: Previous WAMs (e.g., Cosmos-Policy) only leveraged RGB video priors to jointly predict actions and future frames, with no geometric/depth information whatsoever. SA-WAM is the first to seamlessly incorporate a depth modality into the same diffusion backbone without modifying the frozen VAE tokenizer, thereby preserving the visual priors from large-scale video pretraining while adding 3D spatial awareness — a design that achieves "geometric awareness with minimal modification."

  * The paper includes two important figures: Fig. 1 (comparison of SOTA results on the RoboCasa benchmark) and Fig. 2 (overall SA-WAM architecture diagram, showing the arrangement of RGB/depth/proprioception/action within the latent sequence).

### Result

  * On the RoboCasa benchmark, using only 50 demonstrations per task, SA-WAM achieves a 76.6% success rate, 9.5 percentage points higher than the Cosmos-Policy baseline, and surpasses previous methods that required 6–20 times more demonstration data.
  * On the LIBERO-Plus benchmark, it also achieves state-of-the-art results (specific numbers are not listed in the abstract; verification against the full paper is needed for the precise scores).
  * In real-world UR5 robotic arm evaluations, SA-WAM shows clear improvement over strong baselines under randomized environment settings (the abstract and available text excerpts do not provide precise percentages; verification against the full tables in the paper is needed).
  * The paper also analyzes the correlation between world modeling quality and policy rollout success rate, providing a basis for understanding WAM performance and future directions for improvement; Fig. 3 shows a qualitative comparison of a "pick-and-place" task on RoboCasa, contrasting wrist-view rollouts and simulator rollouts between Cosmos-Policy and SA-WAM, with red boxes marking rollout inconsistencies and green boxes marking task completion.

  * **Fairness of the results**: Among the three authors is Google DeepMind researcher Cordelia Schmid. The experimental design includes both simulation (RoboCasa, LIBERO-Plus) and real robot (UR5) validation, with direct comparison against the contemporaneous strong baseline Cosmos-Policy, giving it relatively high credibility; however, currently only the paper's own reported numbers are available, with no third-party reproduction or cross-validation from other papers yet, so it is worth continuing to watch for subsequent work that reproduces or challenges these results.

### Limitation

  * The paper's abstract and readable text excerpts do not explicitly list the specific content of a limitations section; verification against the full text (especially the Discussion/Limitation section) is needed for complete information.
  * Potential limitations that can be inferred from the method design: (1) obtaining depth information still relies on simulators or depth sensors, and depth quality may be affected by sensor noise in real deployment; (2) although the nonlinear depth encoding reuses the existing VAE tokenizer, it may still risk distortion for depth values outside the training distribution range (e.g., extremely near or far distances); (3) the real-world robot platform validated so far is only a single UR5 arm, and transferability to more diverse embodiments (e.g., humanoid robots, dual-arm systems) has not yet been demonstrated.
  * Based on the results, the paper does not provide precise numbers for the LIBERO-Plus and real-world UR5 experiments (only abstract-level descriptions such as "state-of-the-art" and "strong gains"), which makes quantitative comparison with other methods less transparent — a weakness in the completeness of this paper's reporting.

### Related work

  * The direct comparison baseline is Cosmos-Policy (a policy fine-tuning work from NVIDIA's Cosmos series), one of the most important World Action Model-related works of the same period.
  * Recent arXiv papers (2609.xxxxx / 2608.xxxxx) include several other works in the World Action Model / Embodied World Model line, such as GeniWorld (2608.06332), XEWorld (2608.05799), and RoboPhys-3D (2608.28718), showing that "action-conditioned / 3D-aware world models" is a popular direction in robot learning in the second half of 2026, worth continued tracking.
  * **Assessment of how worth surveying this is**: High. This paper involves a Google DeepMind researcher, is methodologically the first to introduce a depth modality "without modifying the frozen tokenizer," has a clear architectural innovation, and provides both simulation and real robot validation, representing an important milestone stage in World Action Models moving from pure RGB toward 3D awareness.

### Conclusion

  * **Overall assessment**: This is a paper with solid methodological innovation and cross-simulation/real-world validation, from a team including a Google DeepMind researcher, achieving SOTA on both the RoboCasa and LIBERO-Plus mainstream robot manipulation benchmarks, and validating sim-to-real feasibility through real UR5 robotic arm experiments — worth serious reference as an important work on the 3D-ification route of World Action Models.
  * **Relationship to other important papers**: SA-WAM builds on Cosmos-Policy (an RGB-only WAM baseline), and is complementary to contemporaneous research directions such as GeniWorld and XEWorld on "action-conditioned world model generalization" — the latter focus on cross-embodiment generalization, while SA-WAM focuses on cross-modal (RGB+depth) geometric awareness; the two routes may eventually converge into a next generation of World Action Models that are both cross-embodiment and cross-modal.
  * **Areas where ROCm/AMD still needs strengthening in this field**: Currently, SA-WAM's training and inference pipeline is built on the NVIDIA ecosystem (comparison against Cosmos-Policy, and the CUDA-based video diffusion training frameworks commonly used in the industry). For AMD/ROCm to enter this type of "video diffusion + joint depth modeling" World Action Model training, it needs to validate the stability and throughput of large-scale video Diffusion Transformer (DiT) training on ROCm, and strengthen the corresponding depth modality data preprocessing and VAE tokenizer porting, in order to provide a competitive alternative for real robot world model training scenarios.
