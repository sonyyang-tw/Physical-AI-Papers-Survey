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

- [IMLE-VLA: Fast Single-Step Action Generation for Vision-Language-Action Policies]({{ site.baseurl }}/vla/imle-vla-fast-single-step-action-generation-for-vision-language-action-policies-1960020599/) — arXiv:2609.10915 (IROS 2026) — trains a single-step action-generation head with conditional IMLE in place of an iterative diffusion/flow-matching head; applied to π0.5, inference frequency rises 3.67x
- [XR-1: Towards Versatile Vision-Language-Action Models via Learning Unified Vision-Motion Representations]({{ site.baseurl }}/vla/xr-1-towards-versatile-vision-language-action-models-via-learning-unified-1978567234/) — arXiv:2511.02776 (ICML 2026 Oral) — a dual-branch VQ-VAE with a shared codebook jointly encodes visual dynamics and robot motion, improving cross-embodiment transfer generalization

### 2. Hierarchy: High-Level Planning/Reasoning vs Low-Level Control

Scope: hierarchical systems where a VLM/reasoner handles task decomposition and a low-level policy handles execution; includes chain-of-thought / latent reasoning in VLA.

Representative papers:

- [What Matters in Orchestrating Robot Policies: A Systematic Study of Hierarchical VLA Agents]({{ site.baseurl }}/vla/what-matters-in-orchestrating-robot-policies-a-systematic-study-of-hierarchical--1945392011/) — arXiv:2606.10267 — a systematic study unifying Hi-VLA agents under an options framework
- [DualCoT-VLA: Visual-Linguistic Chain of Thought via Parallel Reasoning for Vision-Language-Action Models]({{ site.baseurl }}/vla/dualcot-vla-visual-linguistic-chain-of-thought-via-parallel-reasoning-for-vision-1945767494/) — arXiv:2603.22280 — parallel visual + linguistic chain-of-thought
- [DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models]({{ site.baseurl }}/vla/deepthinkvla-enhancing-reasoning-capability-of-vision-language-action-models-1945473584/) — arXiv:2511.15669 — latent CoT variables, examining whether reasoning truly drives action decisions
- [LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks]({{ site.baseurl }}/vla/lohovla-a-unified-vision-language-action-model-for-long-horizon-embodied-tasks-1945538792/) — arXiv:2506.00411 — a unified backbone that performs both high-level planning and low-level control
- [Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models]({{ site.baseurl }}/vla/latent-reasoning-vla-latent-thinking-and-prediction-for-vision-language-action-m-1945391568/) — arXiv:2602.01166 — internalizes multimodal CoT into a continuous latent space
- [ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models]({{ site.baseurl }}/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/) — arXiv:2601.11404 (CVPR 2026, AgiBot) — reasoning happens directly in action space via an Explicit/Implicit Action Reasoner pair, a third CoT-space route distinct from language/visual CoT

- [τ0-VLA: a Hierarchical Robot Foundation Model with World-Model-Guided Test-Time Computation]({{ site.baseurl }}/vla/τ0-vla-a-hierarchical-robot-foundation-model-with-world-model-guided-test-time-c-1946673513/) — arXiv:2608.16885 (AgiBot Finch) — uses world-model-guided beam search to score candidate sub-tasks, bringing test-time compute scaling into hierarchical VLA high-level decision-making

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

- [EgoScale: Scaling Dexterous Manipulation with Diverse Egocentric Human Data]({{ site.baseurl }}/vla/egoscale-scaling-dexterous-manipulation-with-diverse-egocentric-human-data-1955533518/) — arXiv:2602.16710 (NVIDIA GEAR) — validates a log-linear scaling law between egocentric human video data scale and validation loss, predictive of downstream real-robot performance
- [HuRo: Robotizing Human Videos for Scalable VLA Pretraining]({{ site.baseurl }}/vla/huro-robotizing-human-videos-for-scalable-vla-pretraining-1964050194/) — arXiv:2609.10706 (CoRL 2026) — a robotization pipeline converts heterogeneous human video into a robot-aligned format, supporting end-to-end VLA pretraining

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
6. [π0.7: a Steerable Generalist Robotic Foundation Model with Emergent Capabilities]({{ site.baseurl }}/vla/π07-a-steerable-generalist-robotic-foundation-model-with-emergent-capabilities-1951435101/) — arXiv:2604.15483 (Physical Intelligence) — a diverse-context-conditioning training paradigm using episode metadata and sub-goal images as conditioning signals, achieving compositional generalization

---

## Daily Paper Push Log

> The entries below are added automatically by the scheduled task. Each new paper is tagged with the push date, its topic category, and its source (new arXiv release / top conference).

_(No entries yet — accumulation begins once the schedule starts.)_
