---
layout: paper
title: "DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models"
section: vla
page_id: "1945473584"
permalink: /en/vla/deepthinkvla-enhancing-reasoning-capability-of-vision-language-action-models-1945473584/
---

**Paper** : [DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models](https://arxiv.org/abs/2511.15669)  
**Source** : arXiv (conference paper, 26 pages)  
**arXiv ID** : 2511.15669

### Abstract

This paper investigates whether Chain-of-Thought (CoT) reasoning genuinely improves the performance of Vision-Language-Action (VLA) models, or merely adds extra overhead. Through systematic experiments, the authors find that for CoT to be effective for VLA, two conditions must be satisfied simultaneously: (1) Decoding Alignment — CoT and action must be generated using mechanisms suited to each modality's own characteristics; forcing a single autoregressive decoder to generate both simultaneously actually hurts performance; (2) Causal Alignment — CoT must be causally linked to the task outcome through optimization oriented toward task success; otherwise, purely supervised CoT performs almost as poorly as no reasoning at all under the dynamic shifts to which action execution is sensitive. Based on these two findings, the authors propose DeepThinkVLA, which achieves significant improvements on the LIBERO, LIBERO-Plus, and RoboTwin 2.0 simulation benchmarks, with preliminary real-robot experiments providing supporting evidence.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473584_deepthinkvla_fig2.png) 

_Figure 1: Comparison of VLA architectures. DeepThinkVLA proposes a hybrid design that combines autoregressive Chain-of-Thought reasoning with parallel action decoding, balancing reasoning capability with inference efficiency._

![Figure]({{ site.baseurl }}/assets/images/1945473584_deepthinkvla_fig1.png) 

_Figure 2: Two-stage pipeline for constructing the embodied CoT dataset. The first stage extracts key frames via gripper state changes and queries a cloud-based large vision-language model (LVLM); the second stage fine-tunes a local VLM to generate high-quality embodied reasoning-chain annotations._

  * **Problem addressed**: Existing CoT-VLA methods report limited and unstable gains, and no prior work has rigorously diagnosed when and why CoT helps robot action decision-making.
  * **Main method**: DeepThinkVLA adopts a "hybrid-attention decoder": the language (CoT) portion is generated token by token using causal attention, while the action portion is decoded in parallel using bidirectional attention, thereby simultaneously satisfying the generation needs of each modality (solving the Decoding Alignment problem). Training uses a two-stage process of supervised fine-tuning (SFT) followed by reinforcement learning (RL), using a sparse task-success reward to align the entire "reasoning chain to action" causal relationship (solving the Causal Alignment problem).
  * **Difference from prior approaches**: Previous CoT-VLA methods typically used a single autoregressive decoder to generate both textual reasoning and action tokens simultaneously, and trained CoT solely through supervised learning without necessarily linking it causally to task outcomes; DeepThinkVLA explicitly separates the decoding mechanisms and introduces outcome-oriented RL optimization.
  * **Description of the architecture/pipeline**: After receiving visual input and language instructions, the model first autoregressively generates a segment of textual reasoning (CoT) using causal attention, then generates a set of action tokens all at once (in parallel) using bidirectional attention. Training proceeds in two stages: first, SFT is performed using human/teacher-demonstrated CoT and actions; then, RL is used to fine-tune the entire reasoning-action chain with task success or failure as a sparse reward.

### Result

  * DeepThinkVLA achieves a 97.0% success rate on LIBERO, 79.0% on LIBERO-Plus (a robustness test for robots) compared to 61.6% for π0-FAST, and 59.3% success rate on RoboTwin 2.0, surpassing the strongest baseline by 21.7 percentage points.
  * Ablation experiments show that forcing CoT and action into the same autoregressive decoder degrades performance by 4.2 percentage points; without causal alignment (using purely supervised CoT), performance drops by 32.0 percentage points under dynamic-shift conditions, almost equivalent to the baseline with no reasoning at all (a drop of 31.6 percentage points).
  * The paper also conducts preliminary real-robot experiments, demonstrating the physical feasibility of its CoT data construction and hybrid architecture, but the quantitative results for the real robot are limited in scope.
  * Fairness: The baselines compared in the abstract (e.g., π0-FAST) are reproduced/cited by the authors themselves; whether this is fair, and whether there is any discrepancy with other papers' comparative data, needs to be verified.

### Limitation

  * Self-stated limitations: the real-robot experiments are only "preliminary evidence," and their scale and diversity may be limited.
  * Inferred from the results: this method relies heavily on task-success signals as the RL reward; the full text would need to be checked to confirm training stability and scalability in real-world scenarios where rewards are sparse and task success is difficult to determine automatically.
  * The abstract does not explicitly mention model scale, training data volume, or computational cost; deployment and hardware requirements (e.g., whether the RL stage can be trained efficiently on ROCm/AMD GPUs) would need to be verified in the full text.

### Related work

  * The paper mentions comparison baselines including π0-FAST and other existing CoT-VLA / VLA methods, but the abstract does not provide a more complete list of related work.
  * No clearly newer follow-up research has been found (as of the current search scope).
  * Degree to which the related work merits surveying: moderately high, because this paper offers a verifiable diagnostic framework for "when CoT is effective," and subsequent VLA reasoning papers (e.g., LaRA-VLA) are likely to cite or compare against its two alignment conditions.

### Conclusion

  * The two necessary conditions proposed in this paper (Decoding Alignment, Causal Alignment) have diagnostic/methodological value and are not merely a stacking of architectural tricks; they are very valuable for understanding "when CoT is effective in VLA," and worth reading closely.
  * Relationship to other important papers: This paper directly engages with and challenges existing CoT-VLA systems (e.g., π0-FAST mentioned in the abstract), and may complement or contrast with LaRA-VLA (paper 3 on this list, which also discusses CoT but uses latent reasoning to reduce latency) — DeepThinkVLA takes the "explicit CoT + RL alignment" route, while LaRA-VLA takes the "latent reasoning" route, giving different answers to whether reasoning should be made explicit.
  * ROCm/AMD relevance: the abstract does not mention specific training/inference hardware (likely an NVIDIA GPU ecosystem); the compatibility and efficiency of this paper's RL fine-tuning and hybrid-attention decoder on ROCm are unknown, and no clear connection is apparent; the full text's implementation details (whether it uses vLLM, FlashAttention, or other packages with varying degrees of ROCm support) would need to be checked.
