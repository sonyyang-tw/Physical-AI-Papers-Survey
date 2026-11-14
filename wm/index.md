---
layout: default
title: "World Model Papers"
permalink: /wm/
---

# World Model Papers

This page is maintained by an automated Paper Survey Harness. Each day, following the topic taxonomy below, it selects one paper published that day (on arXiv) or recently at a top conference, writes a complete survey, and creates a sub-page for it.

Every paper title is a link — click through to the complete survey sub-page (Abstract / Method / Result / Limitation / Related work / Conclusion).

This page is a sister topic to [VLA Papers]({{ site.baseurl }}/vla/): here the focus is "prediction/simulation first" world-model research (video/latent dynamics prediction), while the VLA page focuses on "action-generation first" research; the two overlap at the World Action Model boundary and cross-reference each other.

---

## Foundational / Reference Models (Milestones Every Survey Should Know, Regardless of Topic)

1. [GAIA-1: A Generative World Model for Autonomous Driving]({{ site.baseurl }}/wm/gaia-1-a-generative-world-model-for-autonomous-driving-1945473423/) — arXiv:2309.17080 (Wayve)
2. [Mastering Diverse Domains through World Models (DreamerV3)]({{ site.baseurl }}/wm/mastering-diverse-domains-through-world-models-dreamerv3-1945767304/) — arXiv:2301.04104 / Nature 2025
3. [Genie 3: A New Frontier for World Models]({{ site.baseurl }}/wm/genie-3-a-new-frontier-for-world-models-1945364950/) — DeepMind official blog
4. [How Cosmos 3 Helps Physical AI Think Before It Acts]({{ site.baseurl }}/wm/how-cosmos-3-helps-physical-ai-think-before-it-acts-1945539515/) — NVIDIA official technical report
5. [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning]({{ site.baseurl }}/wm/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planni-1945474552/) — arXiv:2506.09985 (Meta)
6. [GAIA-2: A Controllable Multi-View Generative World Model for Autonomous Driving]({{ site.baseurl }}/wm/gaia-2-a-controllable-multi-view-generative-world-model-for-autonomous-driving-1945539764/) — arXiv:2503.20523 (Wayve)

---

## Topic Taxonomy

### 1. Video-Generation World Models (General-Purpose / Foundational, Not Robot-Specific)

Scope: large-scale text/action-conditioned video generators positioned as general-purpose "world simulators" (game-like, open-domain), not robot-specific.

Representative papers: see the foundational models Genie 3 and Cosmos 3 above.

### 2. Robot-Specific Action-Conditioned World Models (Manipulation Tasks)

Scope: world models directly coupled to a robot's action space, used for planning, policy imagination, or policy-in-the-loop rollout.

Representative papers:

- [Ctrl-World: A Controllable Generative World Model for Robot Manipulation]({{ site.baseurl }}/wm/ctrl-world-a-controllable-generative-world-model-for-robot-manipulation-1945391989/) — arXiv:2510.10125 (ICLR 2026) — a controllable, multi-view generative world model that improves policy success rate via imagined rollout
- [τ0-WM: A Unified Video-Action World Model for Robotic Manipulation]({{ site.baseurl }}/wm/τ0-wm-a-unified-video-action-world-model-for-robotic-manipulation-1945767449/) — arXiv:2606.01027 (AGIBOT) — a unified video-action world model
- [WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation]({{ site.baseurl }}/wm/weaver-better-faster-longer-an-effective-world-model-for-robotic-manipulation-1945767558/) — arXiv:2606.13672 — a multi-view world model (flow-matching)
- [VLAW: Iterative Co-Improvement of Vision-Language-Action Policy and World Model]({{ site.baseurl }}/wm/vlaw-iterative-co-improvement-of-vision-language-action-policy-and-world-model-1945474219/) — arXiv:2602.12063 — iterative co-improvement of a VLA policy and a world model
- [Pelican-Sim 1.0: A General World Model Simulator for Embodied Intelligence]({{ site.baseurl }}/wm/pelican-sim-1-0-a-general-world-model-simulator-for-embodied-intelligence-1968596049/) — arXiv:2609.12036 (AgiBot) — a unified 28-dim action-value space plus action-visual injection and sparse MoE for cross-embodiment world modeling
- [GE-Act 2.0: Pretraining and Scaling a World-Action Model for Robotic Manipulation]({{ site.baseurl }}/wm/ge-act-2-0-pretraining-and-scaling-a-world-action-model-for-robotic-manipulation-1972876063/) — arXiv:2609.05588 (AgiBot) — trains a WAM entirely from scratch (not inheriting a pretrained video generator), validating a data-scaling law from 300 to 30,000 hours

- [Spatially Aware World Action Model via Geometric Latent Diffusion]({{ site.baseurl }}/wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/) — arXiv:2609.02531 (Google DeepMind contributor) — injects a depth modality into an existing RGB World Action Model diffusion backbone without modifying the frozen VAE tokenizer (originally classified as World Action Models / Video-Action Joint Modeling; filed here pending review)
- [World Action Models are Zero-shot Policies (DreamZero)]({{ site.baseurl }}/wm/world-action-models-are-zero-shot-policies-dreamzero-1951337490/) — arXiv:2602.15922 (NVIDIA; #1 on the RoboArena leaderboard) — jointly models future video frames and action sequences on a single video diffusion backbone, unifying action generation and video prediction
- [DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos]({{ site.baseurl }}/wm/dreamdojo-a-generalist-robot-world-model-from-large-scale-human-videos-1955665089/) — arXiv:2602.06949 (NVIDIA GEAR) — uses continuous latent actions as a proxy-action mechanism, pretraining a world model on 44,000 hours of egocentric human video
- [Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning]({{ site.baseurl }}/wm/cosmos-policy-fine-tuning-video-models-for-visuomotor-control-and-planning-1963892209/) — arXiv:2601.16163 (ICLR 2026, NVIDIA/Stanford) — a latent frame injection mechanism unifies action generation, future-state prediction, and value estimation within a single diffusion sequence

### 3. World Models for Autonomous Driving

Scope: video/latent world models for driving-scenario generation, simulation, closed-loop evaluation, and planning.

Representative papers:

- [DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment]({{ site.baseurl }}/wm/driverse-navigation-world-model-for-driving-simulation-via-multimodal-trajectory-1945539343/) — arXiv:2504.18576 (ACM MM 2025)
- [End-to-End Driving with Online Trajectory Evaluation via BEV World Model (WoTE)]({{ site.baseurl }}/wm/end-to-end-driving-with-online-trajectory-evaluation-via-bev-world-model-1945392255/) — arXiv:2504.01941 (ICCV 2025)
- [DreamerAD: Efficient Reinforcement Learning via Latent World Model for Autonomous Driving]({{ site.baseurl }}/wm/dreamerad-efficient-reinforcement-learning-via-latent-world-model-for-autonomous-1945365119/) — arXiv:2603.24587
- [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)]({{ site.baseurl }}/wm/other-vehicle-trajectories-are-also-needed-a-driving-world-model-unifies-ego-oth-1945392511/) — arXiv:2503.09215

### 4. Model-Based RL / Latent Dynamics for Control

Scope: classic model-based RL that uses a learned latent dynamics model for planning/imagination-based policy learning (not necessarily pixel-level, and not necessarily robot-related).

Representative papers:

- DreamerV3 (see foundational models above)
- [Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination]({{ site.baseurl }}/wm/dream-mpc-gradient-based-model-predictive-control-with-latent-imagination-1945365146/) — arXiv:2605.04568 (ICML 2026)

### 5. World Model Evaluation & Physical-Reasoning Benchmarks

Scope: benchmarks/diagnostic tools that evaluate a world model's physical consistency, controllability, and embodied usefulness.

Representative papers:

- [PhyGround: Benchmarking Physical Reasoning in Generative World Models]({{ site.baseurl }}/wm/phyground-benchmarking-physical-reasoning-in-generative-world-models-1945539592/) — arXiv:2605.10806
- [WorldBench: Benchmarking Physical Understanding of World Models by Isolating Physics Concepts]({{ site.baseurl }}/wm/worldbench-benchmarking-physical-understanding-of-world-models-by-isolating-phys-1945392538/) — arXiv:2601.21282
- [RoboWM-Bench: A Benchmark for Evaluating World Models in Robotic Manipulation]({{ site.baseurl }}/wm/robowm-bench-a-benchmark-for-evaluating-world-models-in-robotic-manipulation-1945365171/) — arXiv:2604.19092
- [WorldOlympiad: Can Your World Model Survive a Triathlon?]({{ site.baseurl }}/wm/worldolympiad-can-your-world-model-survive-a-triathlon-1945767203/) — arXiv:2606.11129
- [iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework]({{ site.baseurl }}/wm/iworld-bench-a-benchmark-for-interactive-world-models-with-a-unified-action-gene-1945539121/) — arXiv:2605.03941

- [Inference-time Physics Alignment of Video Generative Models with Latent World Models]({{ site.baseurl }}/wm/inference-time-physics-alignment-of-video-generative-models-with-latent-world-mo-1959634541/) — arXiv:2601.10553 (Meta FAIR; winner of the ICCV 2025 PhysicsIQ Challenge) — uses V-JEPA 2 as a reward signal to guide candidate denoising trajectories at inference time, improving physical plausibility

### 6. World Models as Data Engines / Simulators for Robot Learning

Scope: explicitly using world models to generate synthetic training data, augment simulation, and narrow the sim-to-real gap.

Representative papers:

- [WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL]({{ site.baseurl }}/wm/wovr-world-models-as-reliable-simulators-for-post-training-vla-policies-with-rl-1945473965/) — arXiv:2602.13977
- [Interactive World Simulator for Robot Policy Training and Evaluation]({{ site.baseurl }}/wm/interactive-world-simulator-for-robot-policy-training-and-evaluation-1945767226/) — arXiv:2603.08546
- [Targeting World Models to Compromise Robot Learning Pipelines]({{ site.baseurl }}/wm/targeting-world-models-to-compromise-robot-learning-pipelines-1945473989/) — arXiv:2606.09499 — an emerging adversarial/safety subtopic around data poisoning of world models
- [Cosmos Predict 2.5 & Transfer 2.5: Evolving the World Foundation Models for Physical AI]({{ site.baseurl }}/wm/cosmos-predict-25-and-transfer-25-evolving-the-world-foundation-models-for-physi-1945767248/) — NVIDIA official technical report
- [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations]({{ site.baseurl }}/wm/mimicgen-a-data-generation-system-for-scalable-robot-learning-using-human-demons-1945473767/) — arXiv:2310.17596 (CoRL 2023, baseline)
- [Dreamitate: Real-World Visuomotor Policy Learning via Video Generation]({{ site.baseurl }}/wm/dreamitate-real-world-visuomotor-policy-learning-via-video-generation-1945364542/) — arXiv:2406.16862 (CoRL 2024, baseline)

### 7. World Models Surveys & Taxonomy Papers (Meta-Tracking Topic)

Scope: survey papers that periodically re-define this field.

Representative papers:

- [World Model for Robot Learning: A Comprehensive Survey]({{ site.baseurl }}/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/) — arXiv:2605.00080
- [World Models for Robotic Manipulation: A Survey]({{ site.baseurl }}/wm/world-models-for-robotic-manipulation-a-survey-1945391939/) — arXiv:2606.00113
- [A Step Toward World Models: A Survey on Robotic Manipulation]({{ site.baseurl }}/wm/a-step-toward-world-models-a-survey-on-robotic-manipulation-1945392081/) — arXiv:2511.02097
- [From World Models to World Action Models: A Concise Tutorial for Robotics]({{ site.baseurl }}/wm/from-world-models-to-world-action-models-a-concise-tutorial-for-robotics-1945539286/) — arXiv:2607.00836 — bridges the VLA/WAM sister topics
- [Aether: Geometric-Aware Unified World Modeling]({{ site.baseurl }}/wm/aether-geometric-aware-unified-world-modeling-1945539008/) — arXiv:2503.18945 (ICCV 2025 Outstanding Paper)

---

## Related NeurIPS 2026 Workshops (Potential Source of Future Push Candidates)

- "Robot Learning with World Models" — robowm-ws.github.io (Sydney, Dec 2026; camera-ready 11/30)
- "World Models in Physical AI" — worldmodels-physicalai.com (Sydney, Dec 2026; camera-ready 11/30)

## Boundary with the VLA Topic

Papers such as τ0-WM, VLAW, and WoVR sit at the "world action model" boundary and are classified under Category 2/6 of this page, while also overlapping with Category 7, "World Models Integration," on the [VLA Papers]({{ site.baseurl }}/vla/) page.

---

## Daily Paper Push Log

> The entries below are added automatically by the scheduled task. Each new paper is tagged with the push date, its topic category, and its source (new arXiv release / top conference).

_(No entries yet — accumulation begins once the schedule starts.)_
