---
layout: default
title: "World Model Papers"
permalink: /en/wm/
---

# World Model Papers

This page is maintained by an automated Paper Survey Harness. Each day, following the topic taxonomy below, it selects one paper published that day (on arXiv) or recently at a top conference, writes a complete survey, and creates a sub-page for it.

Every paper title is a link — click through to the complete survey sub-page (Abstract / Method / Result / Limitation / Related work / Conclusion).

This page is a sister topic to [VLA Papers]({{ site.baseurl }}/en/vla/): here the focus is "prediction/simulation first" world-model research (video/latent dynamics prediction), while the VLA page focuses on "action-generation first" research; the two overlap at the World Action Model boundary and cross-reference each other.

---

## Foundational / Reference Models (Milestones Every Survey Should Know, Regardless of Topic)

1. [GAIA-1: A Generative World Model for Autonomous Driving]({{ site.baseurl }}/en/wm/gaia-1-a-generative-world-model-for-autonomous-driving-1945473423/) — arXiv:2309.17080 (Wayve)
2. [Mastering Diverse Domains through World Models (DreamerV3)]({{ site.baseurl }}/en/wm/mastering-diverse-domains-through-world-models-dreamerv3-1945767304/) — arXiv:2301.04104 / Nature 2025
3. [Genie 3: A New Frontier for World Models]({{ site.baseurl }}/en/wm/genie-3-a-new-frontier-for-world-models-1945364950/) — DeepMind official blog
4. [How Cosmos 3 Helps Physical AI Think Before It Acts]({{ site.baseurl }}/en/wm/how-cosmos-3-helps-physical-ai-think-before-it-acts-1945539515/) — NVIDIA official technical report
5. [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning]({{ site.baseurl }}/en/wm/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planni-1945474552/) — arXiv:2506.09985 (Meta)
6. [GAIA-2: A Controllable Multi-View Generative World Model for Autonomous Driving]({{ site.baseurl }}/en/wm/gaia-2-a-controllable-multi-view-generative-world-model-for-autonomous-driving-1945539764/) — arXiv:2503.20523 (Wayve)

---

## Topic Taxonomy

### 1. Video-Generation World Models (General-Purpose / Foundational, Not Robot-Specific)

Scope: large-scale text/action-conditioned video generators positioned as general-purpose "world simulators" (game-like, open-domain), not robot-specific.

Representative papers: see the foundational models Genie 3 and Cosmos 3 above.

### 2. Robot-Specific Action-Conditioned World Models (Manipulation Tasks)

Scope: world models directly coupled to a robot's action space, used for planning, policy imagination, or policy-in-the-loop rollout.

Representative papers:

- [Ctrl-World: A Controllable Generative World Model for Robot Manipulation]({{ site.baseurl }}/en/wm/ctrl-world-a-controllable-generative-world-model-for-robot-manipulation-1945391989/) — arXiv:2510.10125 (ICLR 2026) — a controllable, multi-view generative world model that improves policy success rate via imagined rollout
- [τ0-WM: A Unified Video-Action World Model for Robotic Manipulation]({{ site.baseurl }}/en/wm/τ0-wm-a-unified-video-action-world-model-for-robotic-manipulation-1945767449/) — arXiv:2606.01027 (AGIBOT) — a unified video-action world model
- [WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation]({{ site.baseurl }}/en/wm/weaver-better-faster-longer-an-effective-world-model-for-robotic-manipulation-1945767558/) — arXiv:2606.13672 — a multi-view world model (flow-matching)
- [VLAW: Iterative Co-Improvement of Vision-Language-Action Policy and World Model]({{ site.baseurl }}/en/wm/vlaw-iterative-co-improvement-of-vision-language-action-policy-and-world-model-1945474219/) — arXiv:2602.12063 — iterative co-improvement of a VLA policy and a world model

### 3. World Models for Autonomous Driving

Scope: video/latent world models for driving-scenario generation, simulation, closed-loop evaluation, and planning.

Representative papers:

- [DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment]({{ site.baseurl }}/en/wm/driverse-navigation-world-model-for-driving-simulation-via-multimodal-trajectory-1945539343/) — arXiv:2504.18576 (ACM MM 2025)
- [End-to-End Driving with Online Trajectory Evaluation via BEV World Model (WoTE)]({{ site.baseurl }}/en/wm/end-to-end-driving-with-online-trajectory-evaluation-via-bev-world-model-1945392255/) — arXiv:2504.01941 (ICCV 2025)
- [DreamerAD: Efficient Reinforcement Learning via Latent World Model for Autonomous Driving]({{ site.baseurl }}/en/wm/dreamerad-efficient-reinforcement-learning-via-latent-world-model-for-autonomous-1945365119/) — arXiv:2603.24587
- [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)]({{ site.baseurl }}/en/wm/other-vehicle-trajectories-are-also-needed-a-driving-world-model-unifies-ego-oth-1945392511/) — arXiv:2503.09215

### 4. Model-Based RL / Latent Dynamics for Control

Scope: classic model-based RL that uses a learned latent dynamics model for planning/imagination-based policy learning (not necessarily pixel-level, and not necessarily robot-related).

Representative papers:

- DreamerV3 (see foundational models above)
- [Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination]({{ site.baseurl }}/en/wm/dream-mpc-gradient-based-model-predictive-control-with-latent-imagination-1945365146/) — arXiv:2605.04568 (ICML 2026)

### 5. World Model Evaluation & Physical-Reasoning Benchmarks

Scope: benchmarks/diagnostic tools that evaluate a world model's physical consistency, controllability, and embodied usefulness.

Representative papers:

- [PhyGround: Benchmarking Physical Reasoning in Generative World Models]({{ site.baseurl }}/en/wm/phyground-benchmarking-physical-reasoning-in-generative-world-models-1945539592/) — arXiv:2605.10806
- [WorldBench: Benchmarking Physical Understanding of World Models by Isolating Physics Concepts]({{ site.baseurl }}/en/wm/worldbench-benchmarking-physical-understanding-of-world-models-by-isolating-phys-1945392538/) — arXiv:2601.21282
- [RoboWM-Bench: A Benchmark for Evaluating World Models in Robotic Manipulation]({{ site.baseurl }}/en/wm/robowm-bench-a-benchmark-for-evaluating-world-models-in-robotic-manipulation-1945365171/) — arXiv:2604.19092
- [WorldOlympiad: Can Your World Model Survive a Triathlon?]({{ site.baseurl }}/en/wm/worldolympiad-can-your-world-model-survive-a-triathlon-1945767203/) — arXiv:2606.11129
- [iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework]({{ site.baseurl }}/en/wm/iworld-bench-a-benchmark-for-interactive-world-models-with-a-unified-action-gene-1945539121/) — arXiv:2605.03941

### 6. World Models as Data Engines / Simulators for Robot Learning

Scope: explicitly using world models to generate synthetic training data, augment simulation, and narrow the sim-to-real gap.

Representative papers:

- [WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL]({{ site.baseurl }}/en/wm/wovr-world-models-as-reliable-simulators-for-post-training-vla-policies-with-rl-1945473965/) — arXiv:2602.13977
- [Interactive World Simulator for Robot Policy Training and Evaluation]({{ site.baseurl }}/en/wm/interactive-world-simulator-for-robot-policy-training-and-evaluation-1945767226/) — arXiv:2603.08546
- [Targeting World Models to Compromise Robot Learning Pipelines]({{ site.baseurl }}/en/wm/targeting-world-models-to-compromise-robot-learning-pipelines-1945473989/) — arXiv:2606.09499 — an emerging adversarial/safety subtopic around data poisoning of world models
- [Cosmos Predict 2.5 & Transfer 2.5: Evolving the World Foundation Models for Physical AI]({{ site.baseurl }}/en/wm/cosmos-predict-25-and-transfer-25-evolving-the-world-foundation-models-for-physi-1945767248/) — NVIDIA official technical report
- [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations]({{ site.baseurl }}/en/wm/mimicgen-a-data-generation-system-for-scalable-robot-learning-using-human-demons-1945473767/) — arXiv:2310.17596 (CoRL 2023, baseline)
- [Dreamitate: Real-World Visuomotor Policy Learning via Video Generation]({{ site.baseurl }}/en/wm/dreamitate-real-world-visuomotor-policy-learning-via-video-generation-1945364542/) — arXiv:2406.16862 (CoRL 2024, baseline)

### 7. World Models Surveys & Taxonomy Papers (Meta-Tracking Topic)

Scope: survey papers that periodically re-define this field.

Representative papers:

- [World Model for Robot Learning: A Comprehensive Survey]({{ site.baseurl }}/en/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/) — arXiv:2605.00080
- [World Models for Robotic Manipulation: A Survey]({{ site.baseurl }}/en/wm/world-models-for-robotic-manipulation-a-survey-1945391939/) — arXiv:2606.00113
- [A Step Toward World Models: A Survey on Robotic Manipulation]({{ site.baseurl }}/en/wm/a-step-toward-world-models-a-survey-on-robotic-manipulation-1945392081/) — arXiv:2511.02097
- [From World Models to World Action Models: A Concise Tutorial for Robotics]({{ site.baseurl }}/en/wm/from-world-models-to-world-action-models-a-concise-tutorial-for-robotics-1945539286/) — arXiv:2607.00836 — bridges the VLA/WAM sister topics
- [Aether: Geometric-Aware Unified World Modeling]({{ site.baseurl }}/en/wm/aether-geometric-aware-unified-world-modeling-1945539008/) — arXiv:2503.18945 (ICCV 2025 Outstanding Paper)

---

## Related NeurIPS 2026 Workshops (Potential Source of Future Push Candidates)

- "Robot Learning with World Models" — robowm-ws.github.io (Sydney, Dec 2026; camera-ready 11/30)
- "World Models in Physical AI" — worldmodels-physicalai.com (Sydney, Dec 2026; camera-ready 11/30)

## Boundary with the VLA Topic

Papers such as τ0-WM, VLAW, and WoVR sit at the "world action model" boundary and are classified under Category 2/6 of this page, while also overlapping with Category 7, "World Models Integration," on the [VLA Papers]({{ site.baseurl }}/en/vla/) page.

---

## Daily Paper Push Log

> The entries below are added automatically by the scheduled task. Each new paper is tagged with the push date, its topic category, and its source (new arXiv release / top conference).

_(No entries yet — accumulation begins once the schedule starts.)_

### Push Date: 2026-09-08

[Spatially Aware World Action Model via Geometric Latent Diffusion]({{ site.baseurl }}/en/wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/) — World Action Models (Video-Action Joint Modeling) — arXiv:2609.02531, new on 2026-09-02, not previously logged on this page

Why selected: the author group includes Google DeepMind researcher Cordelia Schmid, meeting the "major tech company/well-known lab" criterion. Methodologically, it is the first to inject a depth modality into an existing RGB World Action Model diffusion backbone without modifying the frozen VAE tokenizer — a genuine architectural innovation rather than a minor recombination of existing tricks — and it achieves state-of-the-art results on both the RoboCasa/LIBERO-Plus simulation benchmarks and a real UR5 arm, with high completeness of validation.

This paper proposes SA-WAM, addressing the problem that existing World Action Models operate only in RGB observation space and lack explicit 3D/depth information. The core method uses a nonlinear encoding to map unbounded depth signals into the bounded input domain of a frozen VAE tokenizer, allowing the same pretrained video diffusion backbone to jointly denoise and predict action, RGB, and depth. Key result: on RoboCasa, it achieves a 76.6% success rate with only 50 demonstrations, 9.5 percentage points above the Cosmos-Policy baseline, and it also wins on a real, randomized UR5 arm setup. Limitation and significance: the paper does not disclose exact numbers for the LIBERO-Plus and real-world experiments, leaving room for improved quantitative transparency, but its design philosophy of "geometry-awareness plus preserved pretrained priors" is a meaningful signal for World Action Models moving toward a 3D-aware generation.

### Push Date: 2026-09-09

[World Action Models are Zero-shot Policies (DreamZero)]({{ site.baseurl }}/en/wm/world-action-models-are-zero-shot-policies-dreamzero-1951337490/) — Robot-Specific Action-Conditioned World Models (Category 2) — arXiv:2602.15922, submitted 2026-02-17, top-conference-caliber (independently verified #1 on the third-party RoboArena leaderboard), not previously logged on this page

Why selected: the author group is a large NVIDIA-led team (including Linxi "Jim" Fan, Jan Kautz, Yuke Zhu, and other well-known researchers), meeting the "major tech company/well-known lab" criterion. By treating "video as a dense world representation," it unifies action generation and video prediction as a joint denoising task on a single diffusion backbone — a clear architectural departure from existing VLA action decoding and even existing cascaded WAM designs, rather than a minor recombination of existing tricks. It ranks #1 with an Elo of 1750 on the third-party-maintained RoboArena public leaderboard (April 2026), ahead of π0.5 (1622) and π-FAST (1592), a highly credible validation.

DreamZero addresses the problem that VLA models generalize well semantically but poorly physically in terms of motion: it uses the Wan2.1-I2V-14B-480P video diffusion model as its backbone, jointly modeling future video frames and action sequences, and optimizes across system/implementation/model layers so the 14B-parameter model achieves 7Hz real-time closed-loop control. Key results: more than 2x improvement in generalization to new tasks/environments over state-of-the-art VLA baselines; over 42% relative performance gain using only 10-20 minutes of cross-embodiment video demonstrations; and few-shot adaptation to an entirely new robot embodiment (YAM) using only 30 minutes of play data. Limitation: the authors acknowledge that on high-precision manipulation tasks requiring sub-millimeter precision (e.g., peg insertion, fine assembly), the model still inherits common behavior-cloning weaknesses, and even after optimization the 14B video diffusion model only reaches 7Hz, which remains a practical deployment bottleneck compared to lightweight VLAs.

### Push Date: 2026-09-10

[DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos]({{ site.baseurl }}/en/wm/dreamdojo-a-generalist-robot-world-model-from-large-scale-human-videos-1955665089/) — Robot-Specific Action-Conditioned World Models (Category 2, also touches data scaling) — arXiv:2602.06949, submitted 2026-02-06, top-conference-caliber (led by NVIDIA GEAR, with authors including Jitendra Malik, Pieter Abbeel, Yuke Zhu, and Linxi "Jim" Fan), not previously logged on this page

Why selected: the author group is a large NVIDIA GEAR team joined by well-known UC Berkeley scholars (Jitendra Malik, Pieter Abbeel), meeting the "major tech company/well-known lab" criterion. Using "continuous latent actions" as a unified proxy-action mechanism, it is the first to scale world-model pretraining data to 44,000 hours of egocentric human video (roughly 96x more diverse than the largest existing robot dataset), and it designs a distillation pipeline achieving 10.81 FPS real-time inference — an architectural innovation that combines data scaling with practical engineering, rather than a minor recombination of existing tricks. It shares data and infrastructure with EgoScale from the same team (arXiv:2602.16710, also pushed this round to the VLA Papers page), together forming the world-model side of NVIDIA GEAR's "human-data scaling" line of research.

DreamDojo addresses the problem that robot world models are heavily dependent on the robot's own data, which limits scale and diversity: it pretrains a foundational world model on 44K hours of egocentric human video, using continuous latent actions as a proxy-action representation to overcome the lack of action labels in human video, and then fine-tunes on a small amount of target-robot data to gain precise controllability. Key results: the distilled model reaches 10.81 FPS real-time speed with improved context consistency, and validation across multiple out-of-distribution benchmarks confirms its ability to simulate open-world, contact-rich tasks, supporting applications such as real-time teleoperation, policy evaluation, and model-based planning. Main limitation: robot-data fine-tuning is still required for precise controllability, indicating a persistent human-to-robot domain gap; at 10.81 FPS, latency remains higher than lightweight VLA policies, still a deployment bottleneck when used as a policy-in-the-loop.

### Push Date: 2026-09-11

[Inference-time Physics Alignment of Video Generative Models with Latent World Models]({{ site.baseurl }}/en/wm/inference-time-physics-alignment-of-video-generative-models-with-latent-world-mo-1959634541/) — World Model Evaluation & Physical-Reasoning Benchmarks (Category 5, also relevant to the foundational model V-JEPA 2 as a downstream application) — arXiv:2601.10553, submitted 2026-01-15 (v2 revised 2026-02-27), top-conference-caliber (winner of the ICCV 2025 Perception Test PhysicsIQ Challenge), not previously logged on this page

Why selected: the author group includes Meta FAIR senior researchers Nicolas Ballas and Michal Drozdzal (Ballas being a co-lead of the V-JEPA/JEPA series), meeting the "major tech company/well-known lab" criterion. It is directly validated by finishing #1 on the official ICCV 2025 Perception Test PhysicsIQ Challenge leaderboard (62.64%, 7.42 points above the prior SOTA) — a top-conference-caliber result backed by independent third-party evaluation. Methodologically, it is the first to reframe "improving the physical plausibility of video generation" as an inference-time alignment problem, using the latent world model V-JEPA 2 as a reward signal to guide multiple candidate denoising trajectories — a clear architectural departure from existing training-time correction approaches, rather than a minor recombination of existing tricks.

This paper proposes WMReward, addressing the problem that video generation models look visually realistic but often violate physical laws: it uses V-JEPA 2's physical priors as a reward function, searching over and guiding multiple candidate denoising trajectories at inference time, scaling test-time compute for physical-plausibility alignment without retraining the generative model itself. Key results: winner of the ICCV 2025 PhysicsIQ Challenge (62.64%, 7.42 points above the prior SOTA), with significant improvements in physical plausibility across image-conditioned, multi-frame, and text-conditioned generation settings, validated by human preference studies without sacrificing visual quality. Main limitation: it still fails on rapid physical events such as fluid splashing, reflecting the physical-understanding ceiling of the underlying world model (V-JEPA-2) itself, and it substantially increases inference-time compute cost, limiting its applicability to real-time use cases.

### Push Date: 2026-09-14

[Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning]({{ site.baseurl }}/en/wm/cosmos-policy-fine-tuning-video-models-for-visuomotor-control-and-planning-1963892209/) — Robot-Specific Action-Conditioned World Models (Category 2) — arXiv:2601.16163, submitted 2026-01-22, accepted at ICLR 2026 (top-conference-caliber), not previously logged on this page

Why selected: the author group includes NVIDIA researchers (Ming-Yu Liu, Jinwei Gu, and others) and well-known Stanford scholars (Chelsea Finn, Shuran Song, Percy Liang), meeting the "major tech company/well-known lab" criterion; it has been officially accepted at ICLR 2026, also meeting the "top-conference-caliber" criterion. Its core "latent frame injection" mechanism unifies action generation, future-state prediction, and value estimation as generation tasks within the same diffusion sequence, without modifying the pretrained video model's architecture — a clear architectural departure from the existing "video model + extra action head + multi-stage training" paradigm, rather than a minor recombination of existing tricks — and it achieves state-of-the-art results in both simulation and real-world dual-track evaluation, with high completeness of validation.

Cosmos Policy addresses the problem that adapting a pretrained video model's spatiotemporal priors into a robot policy typically requires extra architectural components and multi-stage training: its "latent frame injection" mechanism encodes robot actions, future states, and value estimates all as latent frames within a Cosmos-Predict2 video diffusion model sequence, requiring only a single stage of fine-tuning on robot demonstration data, while also supporting test-time planning. Key results: 98.5% average success rate on the LIBERO simulation benchmark and 67.1% on RoboCasa, both state-of-the-art; on real-world ALOHA bimanual tasks it outperforms a from-scratch-trained diffusion policy, existing video-model policies, and SOTA VLA models such as π0.5 and OpenVLA-OFT+; and it can continuously refine its own world model and value function using its own rollout experience. Main limitation: it depends heavily on the specific pretrained Cosmos-Predict2 backbone, and its effectiveness when transferred to other video models is unverified; real-world evaluation is limited to the ALOHA bimanual platform, and the paper discusses cross-embodiment transferability and inference latency in high-frequency control settings relatively briefly.
