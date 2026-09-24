---
layout: paper
title: "Pelican-Sim 1.0: A General World Model Simulator for Embodied Intelligence"
section: wm
page_id: "1968596049"
permalink: /wm/pelican-sim-1-0-a-general-world-model-simulator-for-embodied-intelligence-1968596049/
---

### Abstract

Pelican-Sim 1.0 (arXiv:2609.12036, submitted 2026-09-10, AgiBot's Beijing Innovation Center of Humanoid Robotics) is a general-purpose world-model simulator that predicts a robot's future observations given a visual context and an action, to support downstream learning and decision-making. The model has four key design elements: (1) a unified 28-dimensional action-value space covering mainstream heterogeneous embodiments, allowing a single model to be used across devices; (2) Action-visual injection: bridging actions and pixels via URDF- and camera-rendered "action videos," substantially improving controllability across embodiments/scenes/tasks (PSNR +0.904 over other fusion baselines); (3) Sparse mixture-of-experts (MoE): sparse MoE layers provide extra capacity for heterogeneous dynamics and absorb action modalities, reducing cross-modal conflict (FVD −6.530 vs. a dense backbone); (4) Efficient rollout generation: causal adaptation plus few-step distillation produce a 4-step autoregressive simulator, 5.67x faster than the 35-step teacher model. Trained on roughly 1 million real and simulated trajectories, it improves PSNR by 4.636, 2.080, and 10.343 on the AgiBotWorld Beta, RoboMIND, and RoboTwin benchmarks respectively; in downstream applications, adding 500 generated trajectories per task on RoboTwin (with only 50 original demonstrations) raises policy success rate from 70% to 93%, and policy evaluation achieves a Pearson correlation of 0.994.

### Method

**Problem addressed**: Existing world models are mostly trained for a single embodiment or task domain, making it difficult to generalize across heterogeneous robot platforms (different degrees of freedom, different action spaces); the coupling (controllability) between action conditioning and pixel prediction is often insufficient, leading to simulation results that are not sensitive or accurate enough to action changes.

**Main method**: (1) representing actions across mainstream embodiments via a unified 28-dimensional action-value space; (2) an Action-visual injection mechanism that renders URDF structure and camera calibration information into an "action video," injected as an extra signal into the Video DiT backbone (action-video residuals injected via a Context Block at even layers, action-value embeddings performing scale-and-shift modulation at odd layers); (3) adding sparse MoE layers to the Video DiT so different experts absorb different embodiment/dynamics patterns, reducing modal conflict; (4) via causal adaptation and few-step distillation, compressing the original 35-step diffusion rollout into 4-step autoregressive generation, achieving a 5.67x speedup.

**Difference from prior approaches**: Unlike existing robot world models (e.g., τ0-WM, WEAVER, Ctrl-World already covered on this page), which are mostly validated on only one or a few embodiments, Pelican-Sim 1.0 explicitly bridges actions and pixels via a unified action-value space plus URDF/camera-rendered action videos — the first systematic architectural solution to both "cross-embodiment generality" and "action controllability" simultaneously, complemented by sparse MoE to handle the resulting heterogeneous dynamics conflict; this is an architectural combinatorial innovation rather than an extension of a single trick.

**Key method figures**: Figure 1 (teaser) shows the overall overview of Pelican-Sim 1.0 — taking an initial RGB image, a 28-dimensional unified action value, and a camera-aligned action video as input, and outputting future observation predictions; Figure 3 shows the model architecture — how the 28-layer Video DiT simultaneously receives action-value embeddings (modulation) and action-video residuals (Context Block injection), and how the sparse MoE layer combines shared-expert and routed-expert outputs.

![Figure]({{ site.baseurl }}/assets/images/2609.12036_pelican_teaser.png)

_Figure 1: Overall overview of Pelican-Sim 1.0_

![Figure]({{ site.baseurl }}/assets/images/2609.12036_pelican_archi.png)

_Figure 3: Model architecture — Video DiT + sparse MoE_

### Result

**How the results turned out**: Across three benchmarks (AgiBotWorld Beta, RoboMIND, RoboTwin), PSNR improves over the strongest baseline by 4.636, 2.080, and 10.343 respectively, with EWMBench DYN score improving by 0.426 on RoboTwin; all four downstream applications were successfully validated: (a) data augmentation — 500 generated trajectories plus 50 demonstrations raise policy success rate from 70% to 93%; (b) policy evaluation — Pearson correlation of 0.994 across five checkpoints; (c) action selection improves 47.7% relatively; (d) policy improvement improves 20.3% relatively.

**Are the results fair**: The paper consistently demonstrates advantages across three independent benchmarks, and the downstream applications span four different uses (data generation, policy evaluation, action selection, policy improvement), cross-validating the model's practical utility rather than overfitting to a single metric; however, as a technical report rather than a peer-reviewed conference paper, the choice of baselines and experimental design have not passed third-party peer review, and independent replication or conference acceptance is still needed for further confirmation.

### Limitation

**Known limitations**: The paper itself is a technical report and has not yet indicated a specific conference acceptance status; while cross-embodiment generalization is qualitatively demonstrated (trajectory, scene, object, embodiment, viewpoint shifts), quantitative validation of the four downstream applications is conducted only on the single RoboTwin benchmark, not yet verified on AgiBotWorld Beta or RoboMIND.

**Weaknesses inferred from results**: While the 4-step autoregressive simulator achieves a 5.67x speedup over the 35-step teacher model, the paper does not fully discuss whether the distilled model's error accumulates over long-horizon rollouts; the impact of sparse MoE on training/inference memory overhead is also not analyzed in detail.

### Related work

Newer related work on arXiv: τ0-WM (AGIBOT, a unified video-action world model), Ctrl-World (ICLR 2026, a controllable multi-view generative world model), and DreamDojo (NVIDIA GEAR, large-scale human-video pretraining), all already covered on this page, belong to the same "robot-specific action-conditioned world model" sub-topic, and can be compared with Pelican-Sim 1.0 along the two dimensions of "unified cross-embodiment action representation" and "training-data scaling."

Worth surveying: Medium-high. Pelican-Sim 1.0's action-visual injection and sparse MoE design concretely address the core pain points of cross-embodiment world models; worth tracking whether future versions (e.g., Pelican-Sim 2.0) introduce larger-scale training data or extend to human-video pretraining.

### Conclusion

**Overall assessment**: Pelican-Sim 1.0 systematically addresses the controllability and heterogeneous-dynamics-conflict problems of cross-embodiment world models at the architectural level, and validates practical value via four downstream applications (data augmentation, policy evaluation, action selection, policy improvement); it comes from a research institution under AgiBot, meeting the "major tech company/well-known lab" criterion; although it is a technical report without a clear conference acceptance status, its degree of methodological innovation and validation completeness are sufficient to include it as a reference for this page's "Robot-Specific Action-Conditioned World Models" sub-topic.

**Relationship to other important papers**: Together with τ0-WM, DreamDojo, and Ctrl-World already covered on this page, it forms a "robot-specific world model" lineage, and may share infrastructure on data and embodiment engineering with the same team's (AGIBOT) τ0-VLA (already covered on the VLA Papers page), forming a cross-reference point between AgiBot's world-model and VLA product lines. ROCm/AMD gap: Pelican-Sim 1.0's sparse MoE layers and Video DiT hybrid architecture, plus the 4-step autoregressive inference pipeline after few-step distillation, currently have limited public optimization solutions for inference optimization of large-scale video-diffusion + MoE hybrid architectures on ROCm (especially non-standard cross-attention paths like action-video residual injection) — an opportunity for AMD to engage with inference acceleration for this class of cross-embodiment world models.
