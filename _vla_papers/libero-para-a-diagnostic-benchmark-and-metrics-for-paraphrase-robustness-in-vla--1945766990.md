---
layout: paper
title: "LIBERO-Para: A Diagnostic Benchmark and Metrics for Paraphrase Robustness in VLA Models"
section: vla
page_id: "1945766990"
permalink: /vla/libero-para-a-diagnostic-benchmark-and-metrics-for-paraphrase-robustness-in-vla--1945766990/
---

**Paper** : [LIBERO-Para: A Diagnostic Benchmark and Metrics for Paraphrase Robustness in VLA Models](https://arxiv.org/abs/2603.28301)  
**Source** : arXiv (cs.LG), EMNLP 2026 (Main Conference)  
**arXiv ID** : 2603.28301

### Abstract

This paper points out that while VLA models achieve strong performance on robot manipulation via pretrained vision-language backbones, they are typically fine-tuned with limited data in downstream robot scenarios, leading to overfitting to specific instruction phrasings, while robustness to "paraphrased" instructions has long been under-studied. To investigate this gap, the authors propose LIBERO-Para, a controlled benchmark that can independently vary "action expressions" and "object references," enabling fine-grained analysis of language generalization ability. The authors test seven VLA configurations (ranging from 0.6B to 7.5B parameters), observing that performance consistently drops by 22 to 52 percentage points (pp) under paraphrased conditions. This drop is primarily driven by "object-level lexical variation"—even simple synonym substitutions cause large performance drops, showing that models rely on surface-level word matching rather than genuine semantic grounding. Furthermore, 80% to 96% of failure cases stem from "planning-level trajectory divergence" rather than execution-level errors, showing that paraphrasing disrupts task identification itself rather than the precision of action execution. The authors also point out that binary success rate treats all paraphrases equally, obscuring whether a model performs consistently across different difficulty levels or merely relies on easier cases. To address this, the authors propose the PRIDE metric, which quantifies paraphrase difficulty using semantic and syntactic factors.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945766990_liberopara_fig1.png) 

_Figure 1: The paraphrase robustness gap under data-scarce fine-tuning — VLA models may overfit to specific instruction phrasing during fine-tuning, resulting in insufficient generalization to synonymous paraphrased instructions._

![Figure]({{ site.baseurl }}/assets/images/1945766990_liberopara_fig2.png) 

_Figure 2: Overview of LIBERO-Para — compared to the original LIBERO, LIBERO-Para evaluates paraphrase robustness under data-scarce fine-tuning through controlled two-axis paraphrasing (objects, actions)._

  * Problem addressed: VLA models under limited-data fine-tuning tend to overfit to specific instruction phrasings, resulting in insufficient robustness to "paraphrased" natural language instructions—a problem that previously lacked systematic, controllable diagnostic tools and evaluation metrics.
  * Main method:
    * Establish the LIBERO-Para benchmark: based on LIBERO, independently and controllably vary two dimensions—"action expressions" (different phrasings of the same action) and "object references" (different names/synonyms for the same object)—allowing researchers to analyze in fine-grained detail which dimension of linguistic variation causes model failure.
    * Propose the PRIDE metric: a metric based on semantic and syntactic factors that quantifies "paraphrase difficulty," replacing the traditional binary success rate (success/failure), so that evaluation can reflect whether a model performs consistently across different difficulty levels, rather than only presenting an overall average that obscures a model "cherry-picking" easier cases.
  * Differences from prior approaches: Existing VLA evaluations mostly focus on visual/physical-level generalization (e.g., new objects, new scenes), with less systematic, independent control of linguistic-level variation factors; this paper is the first to decompose "action expression" and "object reference" into two orthogonal (independently manipulable) variables, paired with the quantifiable PRIDE difficulty metric, rather than using only a single overall paraphrase set for coarse evaluation.
  * Key method design description: this method can be imagined as a "linguistic stress-testing framework"—researchers first take the original LIBERO task instructions, then systematically generate a large number of paraphrased versions (changing only the action wording, only the object naming, or both), feed these paraphrased instructions to seven VLA models of different scales (0.6B to 7.5B parameters) to execute, and record success rate changes and whether failures occur at the "planning stage" (task identification error) or the "execution stage" (insufficient action precision); the PRIDE metric additionally assigns a "difficulty score" to each paraphrased version based on its semantic/syntactic distance from the original instruction, allowing evaluation results to reflect a difficulty distribution rather than a single average.



### Result

  * Across seven VLA configurations (0.6B-7.5B parameters), paraphrased instructions consistently cause performance drops of 22 to 52 percentage points, showing that the paraphrase robustness problem is widespread across models of different scales, not just an issue for small models (large models like 7.5B are equally affected).
  * The performance drop is primarily driven by "object-level lexical variation"—even simple synonym substitutions cause large drops, confirming that models rely heavily on surface-level word matching rather than genuine semantic understanding.
  * 80%-96% of failure cases are "planning-level trajectory divergence" rather than execution errors, meaning the core issue is that the model "misunderstands what task to do," rather than "knowing what to do but executing imprecisely."
  * Fairness: this paper is a diagnostic benchmark paper, testing seven publicly available VLA configurations of different scales, giving it a certain breadth; the numbers (22-52pp drop, 80-96% of failures at the planning level) are specific and come from the authors' own controlled experiments, giving them reasonable credibility. However, since this is a newly proposed benchmark, it still needs verification as to whether other papers have reproduced similar conclusions on this benchmark, or whether there are alternative interpretations of the "synonym substitution" selection method.



### Limitation

  * As a diagnostic/evaluation paper, its inherent limitation is that it only identifies the problem (insufficient robustness) and quantifies it (the PRIDE metric), without proposing a solution (i.e., it is not a paper proposing a new VLA architecture or training method to solve the paraphrase robustness problem).
  * The abstract does not explicitly state other limitations, but it can be inferred that the LIBERO-Para benchmark itself is built on the LIBERO simulation environment, and whether its findings (such as sensitivity to object vocabulary) fully generalize to other simulation environments or real robot scenarios still requires verification from the full text and subsequent research.



### Related work

  * The abstract does not mention any direct connection to other VLA memory or efficiency-related papers (such as the MemoryVLA series, EventVLA, or LaMem-VLA); topically, this paper is about "language robustness/generalization evaluation" rather than "memory mechanisms," making it the only paper among these seven focused on "diagnosis and evaluation" rather than "proposing a new architecture."
  * No direct follow-up research to this paper has been found so far, but since it has been accepted at the EMNLP 2026 main conference, it can be expected to have some influence at the intersection of language models and robotics; it is worth tracking whether other teams propose targeted robustness improvement methods and validate them on this benchmark.



### Conclusion

  * Overall assessment: LIBERO-Para's diagnostic framework of "independently controlling action expression and object reference" is rigorously designed, and its findings that "object-level lexical sensitivity" and "failures mainly originate from planning rather than execution" have important diagnostic value. It is highly worth referencing for any reader working on VLA instruction understanding or language robustness research, and is a high-quality evaluation benchmark paper (already accepted at EMNLP 2026).
  * Relationship to other important papers: this paper differs in topic from the other six papers focused on "memory mechanisms" (the MemoryVLA series, EventVLA, LaMem-VLA, Explicit Language Memory), but can be seen as complementary—memory mechanism papers work to improve VLA robustness to "time/history," while LIBERO-Para reveals VLA's fragility to "variation in linguistic phrasing." Together they point to a common ailment across different dimensions of current VLA models: "surface-level pattern matching without genuine understanding," worth discussing side by side in an overall VLA survey to present the full picture of the field's robustness challenges.
  * ROCm/AMD gaps to address: the abstract does not involve any discussion of hardware platforms, inference efficiency, or training resources; this paper's contribution lies purely in evaluation methodology and dataset construction, with no obvious direct connection to ROCm/AMD hardware optimization.
  * Note: the paper list provided by the user includes multiple variant names such as "LIBERO-Para/Plus/Pro/X," but upon verification, the formal title of arXiv:2603.28301 is only "LIBERO-Para: A Diagnostic Benchmark and Metrics for Paraphrase Robustness in VLA Models," and the abstract does not mention other variant names such as Plus/Pro/X (only the MemoryVLA++ abstract mentions "Libero-Plus" as one of its evaluation benchmarks, which is a different paper). Therefore, this page is written solely based on the verified content of the LIBERO-Para paper, without speculating on the existence or content of other variants.
