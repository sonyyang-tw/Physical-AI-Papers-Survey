---
layout: paper
title: "Explicit Language Memory for Long-Horizon Planning in Vision-Language-Action Models"
section: vla
page_id: "1945364103"
permalink: /vla/explicit-language-memory-for-long-horizon-planning-in-vision-language-action-mod-1945364103/
---

**Paper** : [Explicit Language Memory for Long-Horizon Planning in Vision-Language-Action Models](https://arxiv.org/abs/2608.04765)  
**Source** : arXiv (cs.RO / cs.AI / cs.CV)  
**arXiv ID** : 2608.04765

### Abstract

This paper addresses four major challenges facing VLA models on long-horizon tasks: (1) sparse expert demonstration data limits cross-task compositional generalization; (2) the non-Markovian nature of long-horizon tasks makes it difficult for policies relying only on the current observation to maintain temporal consistency; (3) limited closed-loop error correction ability leads to accumulating execution errors; and (4) end-to-end action fine-tuning can weaken the high-level semantic representations of the VLM backbone. To address these issues, the authors propose a hierarchical long-horizon VLA architecture with an "explicit language memory module." The core idea is to convert discrete temporal observations into a coherent, temporally-logical textual memory sequence. The system is split into a high-level VLM and a low-level VLA: the high-level VLM performs semantic reasoning via a visual question answering (VQA) training paradigm, while the low-level VLA executes precise continuous control based on sub-task instructions and visual observations. The high-level VLM uses prior memory as a contextual anchor, recursively updating the language memory and sub-task instructions, enabling continuous temporal tracking and dynamic correction throughout long-horizon execution. The authors validate the approach in multiple simulation environments and conduct sim-to-real experiments on a real robot platform.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945364103_explmem_fig1.png) 

_Figure: Illustration of the two-stage architecture built on pi-0.5, showing how the language memory module is embedded within the existing VLA reasoning pipeline to provide explicit language-level memory support for long-horizon planning tasks._

![Figure]({{ site.baseurl }}/assets/images/1945364103_explmem_fig2.png) 

_Figure: Details of the Explicit Language Memory architecture. Shows how the language memory module records, updates, and retrieves language-based summaries of past sub-task completion status for use in long-horizon planning decisions, avoiding sub-task misjudgments caused by visually similar states._

  * Problem to be solved: Long-horizon VLA tasks face four challenges—sparse data (limiting compositional generalization), non-Markovian dynamics (difficult to maintain temporal consistency), error accumulation (lacking closed-loop correction), and action fine-tuning weakening semantic representations.
  * Main method: Proposes a hierarchical architecture that splits the system into a "high-level VLM" and a "low-level VLA":
    * High-level VLM: performs semantic-level reasoning via a VQA (visual question answering) training paradigm. Its core innovation is converting discrete temporal observations into a "coherent, temporally-logical textual memory sequence" (explicit language memory), recursively using the previous round's memory as a contextual anchor to continuously update the language memory and sub-task instructions.
    * Low-level VLA: executes precise continuous control actions based on the sub-task instructions issued by the high level and the current visual observation.
  * Difference from prior approaches: Unlike methods such as MemoryVLA/MemoryVLA++/LaMem-VLA that store memory as "latent tokens," this paper uses "explicit language" as the memory carrier, which brings an interpretability advantage—the memory content itself is a human-readable natural language description. The recursive update mechanism also gives high-level planning closed-loop error correction ability, rather than open-loop, one-way execution.
  * Key method design description: The architecture can be thought of as a "two-tier decision pipeline"—the high-level VLM acts like a planner continuously keeping a log, updating, at each timestep, a coherent textual narrative (recording what has been completed, what is in progress, what remains, and execution status) via VQA-style question-answer reasoning based on the current observation and prior text memory, and issuing new sub-task instructions accordingly. The low-level VLA acts like an executor, performing continuous action control based only on the sub-task instruction and the current frame. The two tiers are linked via natural-language instructions and memory.

### Result

  * The paper validates the approach in multiple simulation environments and conducts sim-to-real experiments on a real robot platform; results show that explicit language memory improves success rate and robustness on complex long-horizon tasks, while also providing interpretable semantic explanations of the decision process.
  * The abstract does not provide specific quantitative figures (such as success rate percentages or improvement margins relative to specific baselines), so the exact magnitude of the effect cannot be judged here.
  * Whether the results are fair: Since the abstract does not include specific data, it is difficult to assess the persuasiveness of the results or whether reporting is selective; the full paper needs to be checked for detailed experimental numbers, and it should be confirmed whether other papers (such as contemporaneous work in the MemoryVLA series or LaMem-VLA) reach different conclusions on similar benchmarks or offer a comparison of "explicit language memory" versus "latent memory."

### Limitation

  * The abstract does not explicitly state limitations. Inferred from the method design, explicit language memory (in text form) may lose information relative to latent vector memory (natural language may not fully capture all visual details), and the high-level VLM's recursive generation of text memory may introduce additional inference latency—but this is speculative, as the paper itself does not discuss it in the abstract.
  * The absence of specific success-rate figures in the abstract is itself a limitation in results transparency at the abstract level; the full paper needs to be checked for complete experimental details and failure-case analysis.

### Related work

  * The abstract does not mention specific related-work comparison targets, but this paper can be judged to belong, along with MemoryVLA, MemoryVLA++, LaMem-VLA, and EventVLA, to the same research cluster examining "VLA memory mechanisms" around 2026, differing in memory representation form (text vs. latent vector) and architectural level (hierarchical dual-system vs. single integrated model).
  * No direct follow-up work by the same author group has been found so far, but the "explicit language memory + hierarchical dual-system" approach forms an interesting contrast with other memory methods, and is worth discussing in a survey alongside LaMem-VLA (which explicitly bills itself as "latent-memory-native," implicitly contrasting with this kind of explicit language memory approach).

### Conclusion

  * Overall assessment: The "explicit language memory" approach proposed in this paper has a unique advantage in interpretability (the memory content is human-readable text, facilitating debugging and trust-building), which is valuable for readers who prioritize system interpretability and human-robot collaboration scenarios; however, since the abstract lacks specific quantitative results, its performance relative to latent vector memory methods still needs to be confirmed against the full paper.
  * Relationship with other important papers: This paper, together with MemoryVLA/MemoryVLA++ (latent perception-cognition memory bank) and LaMem-VLA (latent-memory-native framework), represents two different tracks of VLA memory mechanisms—"explicit text memory" vs. "latent vector memory"—forming a methodological contrast and potential challenge relationship, though the abstract does not explicitly identify a directly compared baseline paper.
  * ROCm/AMD gaps: The abstract does not mention any hardware platform information. Since this architecture is a "high-level VLM + low-level VLA" dual-system design involving two separate model inference passes (with the high level needing to generate a relatively long text memory sequence), inference latency and throughput may be an important practical deployment consideration; deploying on ROCm may require evaluating the scheduling and memory management efficiency of a dual-model parallel/chained inference pipeline—but this is speculative based on the architecture, and the paper itself provides no relevant information, so no clear connection to ROCm/AMD can be identified.
