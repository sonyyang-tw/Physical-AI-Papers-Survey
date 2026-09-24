---
layout: default
title: "VLA Papers"
permalink: /vla/
---

# VLA (Vision-Language-Action) Papers

This page is maintained by an automated Paper Survey Harness. Each day, following the topic taxonomy below, it selects one paper published that day (on arXiv) or recently at a top conference, writes a complete survey, and creates a sub-page for it.

Every paper title is a link — click through to the complete survey sub-page (Abstract / Method / Result / Limitation / Related work / Conclusion).

---

## Topic Taxonomy

### 1. Architecture Paradigms (Autoregressive / Diffusion / Flow-matching / Hybrid)

Scope: the core action-generation mechanism design of VLA models — how tokens/actions are decoded (discrete autoregressive, continuous diffusion, flow matching, or unified/hybrid schemes).

Representative papers:

- [Discrete Diffusion VLA: Bringing Discrete Diffusion to Action Decoding in Vision-Language-Action Policies]({{ site.baseurl }}/vla/discrete-diffusion-vla-bringing-discrete-diffusion-to-action-decoding-in-vision--1945364352/) — arXiv:2508.20072 — unifies vision/language/action decoding with discrete diffusion, outperforming an AR baseline on the same backbone
- [DFM-VLA: Iterative Action Refinement for Robot Manipulation via Discrete Flow Matching]({{ site.baseurl }}/vla/dfm-vla-iterative-action-refinement-for-robot-manipulation-via-discrete-flow-mat-1945538880/) — arXiv:2603.26320 — discrete flow matching that can iteratively refine already-generated action tokens
- [SnapFlow: One-Step Action Generation for Flow-Matching VLAs via Progressive Self-Distillation]({{ site.baseurl }}/vla/snapflow-one-step-action-generation-for-flow-matching-vlas-via-progressive-self--1945767352/) — arXiv:2604.05656 — progressive self-distillation compresses flow-matching denoising to a single step
- [AsyncVLA: Asynchronous Flow Matching for Vision-Language-Action Models]({{ site.baseurl }}/vla/asyncvla-asynchronous-flow-matching-for-vision-language-action-models-1945767374/) — arXiv:2511.14148 — a non-uniform/asynchronous flow-matching schedule with confidence-based self-correction over long horizons
- [Let It Be Simple: One-Step Action Generation for Vision-Language-Action Models]({{ site.baseurl }}/vla/let-it-be-simple-one-step-action-generation-for-vision-language-action-models-1945767397/) — arXiv:2606.05737 — challenges the assumption that one-step generation is inherently hard

### 2. Hierarchy: High-Level Planning/Reasoning vs Low-Level Control

Scope: hierarchical systems where a VLM/reasoner handles task decomposition and a low-level policy handles execution; includes chain-of-thought / latent reasoning in VLA.

Representative papers:

- [What Matters in Orchestrating Robot Policies: A Systematic Study of Hierarchical VLA Agents]({{ site.baseurl }}/vla/what-matters-in-orchestrating-robot-policies-a-systematic-study-of-hierarchical--1945392011/) — arXiv:2606.10267 — a systematic study unifying Hi-VLA agents under an options framework
- [DualCoT-VLA: Visual-Linguistic Chain of Thought via Parallel Reasoning for Vision-Language-Action Models]({{ site.baseurl }}/vla/dualcot-vla-visual-linguistic-chain-of-thought-via-parallel-reasoning-for-vision-1945767494/) — arXiv:2603.22280 — parallel visual + linguistic chain-of-thought
- [DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models]({{ site.baseurl }}/vla/deepthinkvla-enhancing-reasoning-capability-of-vision-language-action-models-1945473584/) — arXiv:2511.15669 — latent CoT variables, examining whether reasoning truly drives action decisions
- [LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks]({{ site.baseurl }}/vla/lohovla-a-unified-vision-language-action-model-for-long-horizon-embodied-tasks-1945538792/) — arXiv:2506.00411 — a unified backbone that performs both high-level planning and low-level control
- [Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models]({{ site.baseurl }}/vla/latent-reasoning-vla-latent-thinking-and-prediction-for-vision-language-action-m-1945391568/) — arXiv:2602.01166 — internalizes multimodal CoT into a continuous latent space
- [ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models]({{ site.baseurl }}/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/) — arXiv:2601.11404 (CVPR 2026, AgiBot) — reasoning happens directly in action space via an Explicit/Implicit Action Reasoner pair, a third CoT-space route distinct from language/visual CoT

### 3. Efficiency (Compression / Fast Inference / Data-Efficient Training)

Scope: making VLA practically deployable — distillation, quantization, edge/on-device inference, latency profiling, small models.

Representative papers:

- [VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model]({{ site.baseurl }}/vla/vla-adapter-an-effective-paradigm-for-tiny-scale-vision-language-action-model-1945538827/) — arXiv:2509.09372 (AAAI 2026) — an extremely small-scale VLA paradigm emphasizing parameter efficiency
- [EcoVLA: Energy-Efficient Device-Edge Co-Inference for VLA Models under Real-Time Constraints]({{ site.baseurl }}/vla/ecovla-energy-efficient-device-edge-co-inference-for-vision-language-action-mode-1945364578/) — arXiv:2608.15502 — energy-optimized device-edge collaborative inference
- [How Fast Can I Run My VLA? Demystifying VLA Inference Performance with VLA-Perf]({{ site.baseurl }}/vla/how-fast-can-i-run-my-vla-demystifying-vla-inference-performance-with-vla-perf-1945391760/) — arXiv:2602.18397 — an analytical performance/latency model across VLA + inference-system combinations
- [Offline Semantic Guidance for Efficient Vision-Language-Action Policy Distillation (VLA-AD)]({{ site.baseurl }}/vla/offline-semantic-guidance-for-efficient-vision-language-action-policy-distillati-1945473850/) — arXiv:2605.16241 — distills an OpenVLA-7B teacher down to a 158M student
- [A Survey on Efficient Vision-Language-Action Models]({{ site.baseurl }}/vla/a-survey-on-efficient-vision-language-action-models-1945363892/) — arXiv:2510.24795 — a unified efficiency taxonomy: model design / training / data

### 4. Memory, History-Awareness & Long-Horizon Control

Scope: memory mechanisms for handling non-Markovian, long-horizon manipulation tasks (explicit language memory, latent memory banks, keyframe/event memory, world-model imagination).

Representative papers:

- [MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation]({{ site.baseurl }}/vla/memoryvla-perceptual-cognitive-memory-in-vision-language-action-models-for-robot-1945363954/) — arXiv:2508.19236 — a Cognition-Memory-Action framework
- [MemoryVLA++: Temporal Modeling via Memory and Imagination in Vision-Language-Action Models]({{ site.baseurl }}/vla/memoryvla-temporal-modeling-via-memory-and-imagination-in-vision-language-action-1945473250/) — arXiv:2606.09827 — adds world-model imagination in the denoising latent space
- [Explicit Language Memory for Long-Horizon Planning in Vision-Language-Action Models]({{ site.baseurl }}/vla/explicit-language-memory-for-long-horizon-planning-in-vision-language-action-mod-1945364103/) — arXiv:2608.04765 — natural-language memory updated at every decision step
- [EventVLA: Event-Driven Visual Evidence Memory for Long-Horizon Vision-Language-Action Policies]({{ site.baseurl }}/vla/eventvla-event-driven-visual-evidence-memory-for-long-horizon-vision-language-ac-1945538699/) — arXiv:2606.20092 — dynamic keyframe evidence memory
- [Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation (LaMem-VLA)]({{ site.baseurl }}/vla/dual-latent-memory-in-vision-language-action-models-for-robotic-manipulation-1945391543/) — arXiv:2607.07608 — dual latent short/long-term memory

### 5. Data, Benchmarks & Simulation

Scope: training corpora, simulation environments, and evaluation suites/robustness stress tests for VLA policies.

Representative papers:

- [LIBERO-Para: A Diagnostic Benchmark and Metrics for Paraphrase Robustness in VLA Models]({{ site.baseurl }}/vla/libero-para-a-diagnostic-benchmark-and-metrics-for-paraphrase-robustness-in-vla--1945766990/) — arXiv:2603.28301 — exposes the fragility of the original LIBERO to instruction paraphrasing
- [vla-eval: A Unified Evaluation Harness for Vision-Language-Action Models]({{ site.baseurl }}/vla/vla-eval-a-unified-evaluation-harness-for-vision-language-action-models-1945539244/) — arXiv:2603.13966 — unified evaluation across 18 benchmarks and 13 model servers
- [VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks]({{ site.baseurl }}/vla/vlabench-a-large-scale-benchmark-for-language-conditioned-robotics-manipulation--1945474246/) — arXiv:2412.18194 (ICCV 2025) — a long-horizon, language-conditioned manipulation benchmark
- [VLA-REPLICA: A Low-Cost, Reproducible Benchmark for Real-World Evaluation of Vision-Language-Action Models]({{ site.baseurl }}/vla/vla-replica-a-low-cost-reproducible-benchmark-for-real-world-evaluation-of-visio-1945392290/) — arXiv:2605.20774 — a low-cost, reproducible real-world evaluation benchmark
- [Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines]({{ site.baseurl }}/vla/vision-language-action-in-robotics-a-survey-of-datasets-benchmarks-and-data-engi-1945392329/) — arXiv:2604.23001 (TMLR)

### 6. Embodiment Diversity (Humanoid / Bimanual / Quadruped / Driving)

Scope: cross-embodiment and embodiment-specific VLA adaptation — humanoid whole-body manipulation, quadruped manipulation, bimanual dexterous manipulation, autonomous-driving VLA.

Representative papers:

- [WholeBodyVLA: Towards Unified Latent VLA for Whole-Body Loco-Manipulation Control]({{ site.baseurl }}/vla/wholebodyvla-towards-unified-latent-vla-for-whole-body-loco-manipulation-control-1945392363/) — arXiv:2512.11047 (ICLR 2026) — a unified latent VLA for whole-body locomotion + manipulation
- [HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL]({{ site.baseurl }}/vla/haf-adapting-generalist-vlas-to-humanoid-whole-body-loco-manipulation-via-hierar-1945364999/) — arXiv:2608.16837
- [Human-as-Humanoid: Enabling Zero-Shot Humanoid Learning from Ego-Exo Human Videos with Human-Aligned Embodiments]({{ site.baseurl }}/vla/human-as-humanoid-enabling-zero-shot-humanoid-learning-from-ego-exo-human-videos-1945539450/) — arXiv:2606.32009
- [LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction]({{ site.baseurl }}/vla/leverb-humanoid-whole-body-control-with-latent-vision-language-instruction-1945539712/) — arXiv:2506.13751 — humanoid whole-body control via a latent action vocabulary + RL controller
- [ChainFlow-VLA: Causal Flow Planning with Vision-Language Models]({{ site.baseurl }}/vla/chainflow-vla-causal-flow-planning-with-vision-language-models-1945365318/) — arXiv:2605.23270 — driving-specific AR+diffusion trajectory generation

### 7. World Models Integration (World Action Models)

Scope: combining predictive world/video models with action generation to improve generalization, robustness, and simulation/planning capability. Overlaps with the [World Model Papers]({{ site.baseurl }}/wm/) page; this section focuses on integration research that is "action-generation first."

Representative papers:

- [World Action Models: The Next Frontier in Embodied AI]({{ site.baseurl }}/vla/world-action-models-the-next-frontier-in-embodied-ai-1945392639/) — arXiv:2605.12090 — defines a WAM taxonomy: Cascaded vs Joint WAM
- [Do World Action Models Generalize Better than VLAs? A Robustness Study]({{ site.baseurl }}/vla/do-world-action-models-generalize-better-than-vlas-a-robustness-study-1945392664/) — arXiv:2603.22078
- [In-Context World Modeling for Robotic Control]({{ site.baseurl }}/vla/in-context-world-modeling-for-robotic-control-1945474654/) — arXiv:2606.26025
- [World Model for Robot Learning: A Comprehensive Survey]({{ site.baseurl }}/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/) — arXiv:2605.00080
- [Robots Need More than VLA and World Models]({{ site.baseurl }}/vla/robots-need-more-than-vla-and-world-models-1945392804/) — arXiv:2606.06556 — a position paper identifying gaps in data/embodiment/world-model interfaces

### 8. Interpretability & Diagnostics (Additional Topic)

Scope: causal analysis, probing, and failure prediction for internal VLA mechanisms.

Representative papers:

- [Embodied Interpretability: Linking Causal Understanding to Generalization in Vision-Language-Action Models]({{ site.baseurl }}/vla/embodied-interpretability-linking-causal-understanding-to-generalization-in-visi-1945539823/) — arXiv:2605.00321 (ICML 2026)
- [Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models]({{ site.baseurl }}/vla/sparse-autoencoders-reveal-interpretable-and-steerable-features-in-vla-models-1945539857/) — arXiv:2603.19183
- [Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models]({{ site.baseurl }}/vla/not-all-features-are-created-equal-a-mechanistic-study-of-vision-language-action-1945539900/) — arXiv:2603.19233 — the visual pathway dominates the language pathway
- [Decoding Task Progress from VLA Representations]({{ site.baseurl }}/vla/decoding-task-progress-from-vla-representations-1945539940/) — arXiv:2608.13474
- [Tri-Info: Generalizable, Interpretable Failure Prediction for VLA Models via Information Theory]({{ site.baseurl }}/vla/tri-info-generalizable-interpretable-failure-prediction-for-vla-models-via-infor-1945392973/) — arXiv:2606.19998
- [Artificial Foveated Perception for Mitigating Shortcut Learning in Robotic Foundation Models]({{ site.baseurl }}/vla/artificial-foveated-perception-for-mitigating-shortcut-learning-in-robotic-found-1972778734/) — arXiv:2607.10655 (CoRL 2026, Yale/UConn/PKU/Imperial) — a policy-agnostic mask predictor that supervises policy attention during fine-tuning to mitigate shortcut learning, with zero inference-time overhead

---

## Foundational / Reference Models (Milestones Every Survey Should Know, Regardless of Topic)

1. [RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control]({{ site.baseurl }}/vla/rt-2-vision-language-action-models-transfer-web-knowledge-to-robotic-control-1945474821/) — arXiv:2307.15818 (Google DeepMind) — established the VLA paradigm
2. [OpenVLA: An Open-Source Vision-Language-Action Model]({{ site.baseurl }}/vla/openvla-an-open-source-vision-language-action-model-1945393020/) — arXiv:2406.09246 — an open-source 7B VLA
3. [π0: A Vision-Language-Action Flow Model for General Robot Control]({{ site.baseurl }}/vla/pi0-a-vision-language-action-flow-model-for-general-robot-control-1945365620/) — arXiv:2410.24164 (Physical Intelligence, RSS 2025) — a flow-matching, continuous-action, general-purpose policy
4. [GR00T N1: An Open Foundation Model for Generalist Humanoid Robots]({{ site.baseurl }}/vla/gr00t-n1-an-open-foundation-model-for-generalist-humanoid-robots-1945393079/) — arXiv:2503.14734 (NVIDIA) — a dual-system humanoid foundation model
5. [Helix: A Vision-Language-Action Model for Generalist Humanoid Control]({{ site.baseurl }}/vla/helix-a-vision-language-action-model-for-generalist-humanoid-control-1945393112/) — Figure AI official blog — the first VLA supporting high-frequency, whole-body humanoid upper-body control

---

## Daily Paper Push Log

> The entries below are added automatically by the scheduled task. Each new paper is tagged with the push date, its topic category, and its source (new arXiv release / top conference).

_(No entries yet — accumulation begins once the schedule starts.)_

### Push Date: 2026-09-08

[τ0-VLA: a Hierarchical Robot Foundation Model with World-Model-Guided Test-Time Computation]({{ site.baseurl }}/vla/τ0-vla-a-hierarchical-robot-foundation-model-with-world-model-guided-test-time-c-1946673513/) — crosses Hierarchy: High-Level Planning/Reasoning vs Low-Level Control (Category 2) and World Models Integration (Category 7) — arXiv:2608.16885, submitted 2026-08-17, not previously logged on this page

Why selected: from Agibot Finch (in collaboration with the Shanghai Innovation Institute and The Chinese University of Hong Kong) — meets the "major tech company/well-known lab" criterion. It introduces test-time compute scaling into high-level sub-task generation for hierarchical VLA, using a world model to predict and score the visual outcomes of candidate sub-tasks — a clear methodological departure from prior "world-model-assisted action generation" approaches rather than a minor recombination of existing techniques. Training data spans 40,115 hours of real-world data, representing an industrial-scale investment.

τ0-VLA addresses the problem that, in long-horizon robotic manipulation, high-level decision-making cannot dynamically allocate compute according to task difficulty. Its high-level policy combines a proposal model, a world model, a value model, and a reflective model: at uncertain decision points it uses world-model-guided beam search to predict and score the visual outcomes of candidate sub-tasks, and a reflective model produces the final sub-task, while the low-level policy executes cross-embodiment actions via flow matching. Across four real-robot long-horizon tasks, the hierarchical system achieves a 45% average success rate (versus 2.5% for GR00T N1.7 and 22.5% for π0.5), and test-time compute (TTC) improves both success rate and sub-task prediction accuracy over single-shot planning (Plan Once) across the board. Main limitation: the real-robot evaluation sample size is small (only 10 trials per task), and world-model prediction errors could mislead high-level decisions — the paper does not specifically analyze this general risk of world-model-guided methods.

### Push Date: 2026-09-09

[π0.7: a Steerable Generalist Robotic Foundation Model with Emergent Capabilities]({{ site.baseurl }}/vla/π07-a-steerable-generalist-robotic-foundation-model-with-emergent-capabilities-1951435101/) — Foundational/Reference Model (flagship of the π series, cross-cutting Architecture Paradigms and Hierarchical Planning) — arXiv:2604.15483, submitted 2026-04-16 (revised 2026-04-24), top-conference-caliber, not previously logged on this page

Why selected: from Physical Intelligence (the original π0 / RSS 2025 team), meeting the "major tech company/well-known lab" criterion. It proposes a "diverse context conditioning" training paradigm that uses episode metadata plus sub-goal images as extra conditioning signals, enabling the model to ingest heterogeneous, suboptimal, or even failed trajectories while achieving compositional generalization — a clear methodological innovation rather than a minor recombination of existing tricks. The air fryer case study (only two fragmentary demonstrations in training data, with success rate raised from 5% to 95% via 30 minutes of human coaching-style prompting) demonstrates a representative breakthrough in generalization and steerability.

π0.7 addresses the long-standing difficulty of achieving "compositional generalization" in VLA: a 5B-parameter model (4B VLM backbone + MEM video-history encoder + 860M action expert) where, at inference time, a high-level semantic policy of the same architecture generates instructions and a lightweight BAGEL-based world model produces sub-goal images. Key results: out-of-the-box performance on unseen multi-stage kitchen tasks, cross-embodiment laundry folding, and operating an espresso machine approaches that of specialized RL-fine-tuned models, with the air fryer case improving from 5% to 95% success. Limitation: the authors acknowledge that on large, diverse datasets it is difficult to rigorously determine whether tasks are truly "unseen," and the high success rates depend on real-time human coaching-style prompting, so pure zero-shot capability may be overstated; moreover, most evaluations were conducted by Physical Intelligence itself and await independent third-party replication.

### Push Date: 2026-09-10

[EgoScale: Scaling Dexterous Manipulation with Diverse Egocentric Human Data]({{ site.baseurl }}/vla/egoscale-scaling-dexterous-manipulation-with-diverse-egocentric-human-data-1955533518/) — Data, Benchmarks & Simulation (Category 5, also touches Embodiment Diversity's dexterous-hand manipulation) — arXiv:2602.16710, submitted 2026-02-18, top-conference-caliber (led by NVIDIA GEAR), not previously logged on this page

Why selected: the author group is the NVIDIA GEAR team (including Linxi "Jim" Fan, Yuke Zhu, Danfei Xu) in collaboration with UC Berkeley (Trevor Darrell) and the University of Maryland (Furong Huang), meeting the "major tech company/well-known lab" criterion. It is the first to systematically verify a log-linear scaling law between the scale of large-scale egocentric human video data and validation loss, and shows this validation loss predicts downstream real-robot performance — an empirically meaningful methodological innovation on the data-scaling front rather than a minor recombination of existing tricks. Training data spans 20,854 hours of action-annotated egocentric human video, more than 20x larger than prior work, representing an industrial-scale investment.

EgoScale addresses the problem that robot teleoperation data is expensive to collect and hard to scale: it trains a VLA model via a two-stage pipeline (large-scale human-data pretraining plus lightweight human-robot alignment mid-training), extracting transferable interaction knowledge from unlabeled human video via continuous proxy action labels. Key results: on a 22-DoF dexterous hand, average success rate improves 54% over a no-pretraining baseline, and the gains transfer effectively to lower-DoF hands, showing that large-scale human motion provides reusable, cross-embodiment motion priors; the discovered scaling law also gives industry a quantitative basis for planning data-collection investment. Main limitation: there is no thorough sensitivity analysis of how noise in the pseudo action labels (derived from human pose estimation) affects downstream fine-motor policy precision, and all evaluation is based on a single institution's tasks and hardware platform, so cross-institution external validation is still needed.

### Push Date: 2026-09-11

[IMLE-VLA: Fast Single-Step Action Generation for Vision-Language-Action Policies]({{ site.baseurl }}/vla/imle-vla-fast-single-step-action-generation-for-vision-language-action-policies-1960020599/) — Architecture Paradigms (Category 1) — arXiv:2609.10915, new on 2026-09-10, a new same-day arXiv release (submitted the previous day)

Why selected: already accepted at IEEE/RSJ IROS 2026, meeting the "top-conference-caliber" criterion; while the author group (Simon Fraser University, University of Pennsylvania, Amii) is not a traditional tech giant, the method builds directly on and substantially outperforms Physical Intelligence's flagship model π0.5 (already covered on this page as a foundational model), making it highly relevant to this page's core research thread. It trains a single-step action-generation head with conditional Implicit Maximum Likelihood Estimation (cIMLE) in place of an iterative diffusion/flow-matching action head — a genuine methodological innovation (not a minor recombination of existing one-step-generation tricks) — validated comprehensively in both simulation and on a real robot.

IMLE-VLA addresses the problem that VLA action heads relying on multi-step iterative sampling (e.g., π0.5's 10-step Euler integration) incur inference latency and cause jerky, start-stop robot motion: it trains a single-step conditional generator with the cIMLE objective, sampling multiple candidate actions and applying gradient updates only to the sample closest to the demonstration, preserving action multimodality while eliminating iterative sampling. Applied to π0.5, inference frequency rises from 15Hz to 55Hz (3.67x), average success rate on the LIBERO 40-task benchmark reaches 98.0% (highest among all baselines), robustness under LIBERO-plus perturbation testing matches π0.5's original robustness, and it beats π0.5 across all four real Franka Panda arm tasks, with jerk reduced 2.2–3.0x. Main limitation: cIMLE is fairly sensitive to the choice of the sampling factor m (degenerating to standard regression at m=1), and real-world validation is limited to a single robotic arm and four tasks, so cross-embodiment transferability remains unverified.

### Push Date: 2026-09-14

[HuRo: Robotizing Human Videos for Scalable VLA Pretraining]({{ site.baseurl }}/vla/huro-robotizing-human-videos-for-scalable-vla-pretraining-1964050194/) — Data, Benchmarks & Simulation (Category 5, also touches large-scale human-data scaling) — arXiv:2609.10706, new on 2026-09-10, accepted at CoRL 2026 (top-conference-caliber), not previously logged on this page

Why selected: officially accepted at CoRL 2026, meeting the "top-conference-caliber" criterion; the author group is from Yonsei University in Korea (Seon Joo Kim's team) — while not from a traditional tech giant, the paper is highly relevant to and complements this page's already-covered NVIDIA GEAR "large-scale human-data scaling" line of work (EgoScale, DreamDojo). Methodologically, it is the first to systematically validate the effect of "joint end-to-end action + visual robotization" versus "visual-only transfer," and proposes a scalable robotization pipeline itself (rather than merely producing training data or verifying a scaling law) — a methodologically meaningful innovation on the data-engineering front rather than a minor recombination of existing tricks. The dataset spans 630,000 robotized episodes and 142 million frames, representing an industrial-scale investment.

HuRo addresses the problem that robot demonstration data is prohibitively expensive to collect and hard to scale: it builds a robotization pipeline that retargets and converts observation and action signals from heterogeneous human activity videos into a robot-aligned format, filling in missing intermediate signals across annotation levels, and then uses this to pretrain a VLA model end-to-end. Key results: across four real-world manipulation tasks, as robotization-pretraining scale increases, overall completion rate rises from 51.5% to 80.3%, and out-of-distribution (OOD) completion rate rises from 34.9% to 72.2%; ablations show visual robotization improves OOD robustness, and joint end-to-end action+visual conversion outperforms visual-only transfer. Main limitation: the robotization pipeline relies on multi-level annotation and signal inference, and there is no thorough sensitivity analysis of how its errors affect downstream action precision; evaluation is limited to four real tasks and five human-video sources, so cross-institution external validation is still needed.

### Push Date: 2026-09-15

[ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models]({{ site.baseurl }}/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/) — Hierarchy: High-Level Planning/Reasoning vs Low-Level Control (Category 2, CoT/reasoning sub-direction) — arXiv:2601.11404, submitted 2026-01-16 (revised v2 2026-03-30), accepted at CVPR 2026 (top-conference-caliber), not previously logged on this page

Why selected: accepted at CVPR 2026, meeting the "top-conference-caliber" criterion; the author group and code repository (github.com/AgibotTech/ACoT-VLA) confirm it is from AgiBot (the same team behind τ0-VLA, already covered on this page), meeting the "major tech company/well-known lab" criterion; it proposes "Action Chain-of-Thought" — reasoning happening directly in action space (rather than existing indirect intermediaries like language sub-tasks or synthesized goal images) — a clear departure from this page's existing CoT lines (DualCoT-VLA's parallel visual+language CoT, DeepThinkVLA's and Latent Reasoning VLA's latent CoT), constituting a third distinct CoT-space route and a genuine methodological innovation rather than a minor recombination of existing tricks.

ACoT-VLA addresses the problem that traditional VLA directly maps multimodal inputs to actions, or uses language sub-tasks/goal images as an intermediary, both of which struggle to carry the fine-grained information required for precise action execution: the core method is an Explicit Action Reasoner (EAR) that proposes a coarse reference trajectory as an explicit action-level reasoning step, paired with an Implicit Action Reasoner (IAR) that extracts implicit action priors from the VLM's internal representations, jointly forming the ACoT that conditions the downstream action head. Extensive real-world and simulation experiments show this method outperforms existing baselines, and it has passed CVPR 2026 peer review. Main limitation: the abstract-level description does not fully disclose the risk of accumulated error from EAR's coarse trajectory in long-horizon tasks, nor does it discuss a fault-tolerance mechanism for disagreement between the EAR/IAR reasoning paths; specific evaluation task lists and cross-embodiment generalization details require consulting the full text.

### Push Date: 2026-09-16

[Artificial Foveated Perception for Mitigating Shortcut Learning in Robotic Foundation Models]({{ site.baseurl }}/vla/artificial-foveated-perception-for-mitigating-shortcut-learning-in-robotic-found-1972778734/) — Interpretability & Diagnostics (Category 8, also touches cross-cutting "fine-tuning robustness") — arXiv:2607.10655, submitted 2026-07-12 (revised v2 2026-09-07), accepted at CoRL 2026 (top-conference-caliber), not previously logged on this page

Why selected: officially accepted at CoRL 2026, meeting the "top-conference-caliber" criterion; the author group is a joint academic team from Yale University, University of Connecticut, Peking University, and Imperial College London — while not a traditional tech giant, its real-robot experiments directly use Physical Intelligence's π0.5 (a foundational model already covered on this page) as a validation backbone, making it highly relevant to this page's core research thread; it reframes "aligning policy visual attention during fine-tuning" as a standalone auxiliary supervision problem, deliberately designed to have zero inference-time overhead and no modification to the policy architecture itself — a clear departure from existing fine-tuning paradigms that supervise only at the action level, constituting a genuine methodological innovation rather than a minor recombination of existing tricks; it is validated comprehensively across four foundation models (SmolVLA, OpenVLA, π0.5, Motus), eight simulated tasks, and five real-robot tasks, with code, an annotation tool, and a dataset all open-sourced.

This paper proposes Artificial Foveated Perception (AFP) to address the problem that robotic foundation models, after fine-tuning, tend to rely on shortcuts (background texture, lighting, object co-occurrence, and other visual correlations with no causal relationship to task success), causing failure under environmental perturbations: the core method is a policy-agnostic mask predictor that uses a MobileNetV3 feature path and deformable cross-attention query path to predict task-relevant region masks, serving as an auxiliary grounding loss to align policy attention during fine-tuning, with zero participation at inference time. Key results: π0.5's in-distribution Soft-IoU rises from 0.17 to 0.93, real-robot experiments across five tasks (including FurnitureBench) show improvements across the board in both distributions, and fine-tuning speed on long-horizon, multi-stage tasks is noticeably faster. Main limitation: it depends on human-annotated task-relevance masks, with annotation cost and potential bias remaining a scaling bottleneck, and real-world validation is limited to a single robotic-arm platform.
