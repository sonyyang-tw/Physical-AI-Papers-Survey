---
layout: paper
title: "VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks"
section: vla
page_id: "1945474246"
permalink: /vla/vlabench-a-large-scale-benchmark-for-language-conditioned-robotics-manipulation--1945474246/
---

**Paper** : [VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks](https://arxiv.org/abs/2412.18194)  
**Source** : arXiv (cs.RO); ICCV 2025 (accepted, poster)  
**arXiv ID** : 2412.18194

### Abstract

General-purpose embodied agents are designed to understand a user's natural language instructions or intentions and to precisely execute actions to complete general-purpose tasks. Recently, foundation-model-based approaches, especially Vision-Language-Action (VLA) models, have shown remarkable potential for solving Language-Conditioned Manipulation (LCM) tasks. However, existing benchmarks do not adequately meet the needs of VLA and related algorithms. To better define such general-purpose tasks in the context of large language models and to advance VLA research, the authors propose VLABench, an open-source benchmark for evaluating general LCM task learning. VLABench provides 100 carefully designed task categories, each with a high degree of randomization, spanning more than 2,000 objects in total. VLABench differs from existing benchmarks in four key respects: (1) tasks that require world knowledge and common-sense transfer; (2) natural language instructions that carry implicit human intent, rather than templated instructions; (3) long-horizon tasks that require multi-step reasoning; and (4) simultaneous evaluation of both action policies and language model capabilities. The benchmark evaluates a range of abilities, including understanding of mesh and texture, spatial relationships, semantic instructions, physical laws, knowledge transfer, and reasoning. To support downstream fine-tuning, the authors also provide high-quality training data collected via an automated framework (combining heuristic skills and prior information). Experimental results show that current state-of-the-art pretrained VLA models, as well as VLM-based workflow methods, both face challenges on the tasks in this benchmark.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474246_vlabench_fig1.png) 

_Figure 1: VLABench overview._

![Figure]({{ site.baseurl }}/assets/images/1945474246_vlabench_fig6.png) 

_Figure 6: VLABench evaluation workflow._

  * Problem addressed: Existing robot manipulation benchmarks do not adequately meet the evaluation needs of VLA and related algorithms — for example, they lack tests of world knowledge and common-sense transfer, their instructions are mostly fixed templates rather than natural language carrying implicit intent, most tasks are single-step rather than long-horizon multi-step reasoning tasks, and they typically evaluate only action policy performance without evaluating language understanding capability.
  * Main method: VLABench constructs a large-scale simulated benchmark spanning 100 task categories and over 2,000 objects, with a high degree of randomization within each task category to prevent models from exploiting memorized templates rather than genuine understanding. Task design deliberately covers four aspects that were less emphasized by previous benchmarks: world knowledge/common-sense transfer, natural language instructions with implicit intent, long-horizon tasks requiring multi-step reasoning, and a dual-track evaluation of both action policy and language model capability. Additionally, the authors provide an automated data-collection framework (combining heuristic skills and prior information) for generating high-quality training data for downstream fine-tuning.
  * Difference from prior approaches: Unlike previous benchmarks (whose tasks are mostly short-horizon, whose instructions are templated, and which evaluate only action success rate), VLABench deliberately designs tasks that are closer to the ambiguity and complexity of the real world — instructions carry implicit human intent rather than explicit templates, tasks require multi-step long-horizon reasoning, and the evaluation scope extends to language/visual understanding capability.
  * Key design description: The overall benchmark can be envisioned as a two-tier task structure — Primitive Tasks (60 basic tasks requiring only one or two dimensions of ability and a small combination of skills, such as a single grasp or place action) and Composite Tasks (40 combination tasks requiring multi-step reasoning and long-horizon planning, involving a larger combination of skills and abilities). The evaluation framework is further divided into three main categories: evaluation of pretrained or fine-tuned VLA models, evaluation of heuristic workflows integrating foundation models with various algorithms, and evaluation of vision-language models (VLMs) across multiple dimensions of capability (e.g., mesh/texture understanding, spatial relationships, physical-law reasoning).



### Result

  * Experimental results show that current state-of-the-art pretrained VLA models and VLM-based workflow methods both face significant challenges on VLABench's tasks (the abstract does not provide specific success-rate numbers; the experimental tables in the full text need to be checked).
  * Main improvement/revelation: What this benchmark mainly enhances is not the performance of any specific model, but rather the completeness of the evaluation dimensions — it reveals the widespread inadequacy of existing VLA models in long-horizon reasoning, implicit-intent understanding, and world-knowledge transfer.
  * Fairness: As a paper formally accepted at ICCV 2025, it has undergone peer review; however, since this is a newly proposed benchmark, whether its task design has any implicit bias toward specific model architectures needs to be verified against the full text and third-party evaluation results, and it is currently not possible to confirm whether there are any discrepancies with other papers' results.



### Limitation

  * The abstract does not have an explicitly stated limitations section; the full text needs to be checked.
  * Potential weaknesses inferred from the experimental results: Since current SOTA VLA models and VLM workflows all encounter difficulty on this benchmark, the task difficulty may be relatively high, meaning that in the short term its value lies more in serving as a reference for the ceiling of model capability rather than as a tool for day-to-day iterative validation. In addition, as a simulation benchmark, whether it can fully represent the diversity of real-world manipulation scenarios still requires sim-to-real validation.



### Related work

  * Highly related to vla-eval (arXiv:2603.13966) from the same batch — VLABench is likely one of the benchmarks supported by vla-eval; it also directly echoes the structural gap in long-horizon reasoning evaluation mentioned in the VLA survey (arXiv:2604.23001).
  * The paper was submitted in December 2024 and formally published at ICCV in October 2025; it is currently not possible to confirm whether there is a direct follow-up improved version, and it is recommended to check for subsequent publications by the author team (Fudan University OpenMOSS).
  * Degree to which the related work is worth surveying: high — an important reference point for understanding the sub-field of long-horizon reasoning evaluation for VLA.



### Conclusion

  * Overall assessment: VLABench is a peer-reviewed (ICCV 2025), well-designed benchmark paper that systematically addresses clear gaps in existing benchmarks, offering high reference value for evaluating the reasoning and generalization capability of VLA models.
  * Relationship to other important papers: Forms a close citation/echoing relationship with vla-eval and the VLA survey (2604.23001) from the same batch.
  * Relevance to ROCm/AMD: No clear direct connection to ROCm/AMD can be identified; the paper focuses on the design of robotic manipulation task benchmarks and simulation environment construction, without mentioning specific training/inference hardware platform choices. This benchmark involves large-scale simulation rendering, so if AMD wants to validate GPU/ROCm performance on large-scale robot simulation, it could serve as a test case, but this is a speculative direction.
