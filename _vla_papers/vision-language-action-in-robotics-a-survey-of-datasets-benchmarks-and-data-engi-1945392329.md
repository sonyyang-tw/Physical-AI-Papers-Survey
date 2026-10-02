---
layout: paper
title: "Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines"
section: vla
page_id: "1945392329"
permalink: /vla/vision-language-action-in-robotics-a-survey-of-datasets-benchmarks-and-data-engi-1945392329/
---

**Paper** : [Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines](https://arxiv.org/abs/2604.23001)  
**Source** : arXiv (cs.RO, cs.AI); TMLR (peer-reviewed, OpenReview: https://openreview.net/forum?id=tAaWFpvnmm)  
**arXiv ID** : 2604.23001

### Abstract

Although Vision-Language-Action (VLA) models have made remarkable progress, one core bottleneck has long been insufficiently examined: the data infrastructure underpinning embodied learning. This survey argues that future progress in VLA will depend less on model architecture and more on the co-design of high-fidelity data engines and structured evaluation protocols. The authors propose a data-centric systematic analytical framework organized around three pillars: datasets, benchmarks, and data engines. On the dataset side, real-world and synthetic corpora are classified according to embodiment diversity, modality composition, and action-space form, revealing a persistent fidelity-cost trade-off that fundamentally limits large-scale data collection. On the benchmark side, both task complexity and environment structure are analyzed jointly, revealing structural gaps in existing evaluation protocols regarding compositional generalization and long-horizon reasoning assessment. On the data-engine side, three paradigms — simulation-based, video-reconstruction-based, and automatic task generation-based — are examined, pointing out their common limitations in physical grounding and sim-to-real transfer. Synthesizing this analysis, the authors identify four open challenges yet to be resolved: representation alignment, multimodal supervision, reasoning assessment, and scalable data generation.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392329_survey2_fig2.png) 

_Figure 2: Survey scope overview._

  * Problem addressed: the VLA field generally focuses on model architecture innovation, while the data infrastructure (datasets, benchmarks, data engines) — the real underlying bottleneck — has long been overlooked; this paper attempts to systematically organize this underappreciated problem area.
  * Main method: this is a survey, and its method is to propose a three-pillar classification framework (datasets / benchmarks / data engines), and to systematically summarize and comparatively analyze existing literature along multiple dimensions (embodiment diversity, modality composition, action-space form, task complexity, environment structure, data-generation paradigm), rather than proposing a new model or algorithm.
  * Difference from prior approaches: many previous VLA-related surveys have mainly centered on model architecture or training methods, whereas this paper deliberately shifts the perspective toward the data layer, incorporating benchmark design and data engines into the same analytical framework, emphasizing that the three need to be co-designed rather than discussed separately.
  * Key method design: the analytical logic of the paper can be envisioned as a three-layer structure — the bottom layer is the dataset layer, classified along the three axes of embodiment type x modality x action space, pointing out the trade-off relationship where real data has high fidelity but high collection cost, while synthetic data has low cost but limited fidelity; the middle layer is the benchmark layer, examining both the compositional complexity of tasks and environment structure, identifying systematic gaps in existing protocols regarding compositional generalization and long-horizon reasoning assessment; the top layer is the data-engine layer, comparing simulation engines, methods that reconstruct action labels from video, and automatic task generation methods as three data-generation routes, and pointing out that they commonly face insufficient physical grounding and the sim-to-real gap. The analysis across the three layers ultimately converges into a discussion of four open challenges.

### Result

  * Since this is a survey paper, there are no traditional experimental results; its contribution lies in systematically identifying four open challenges (representation alignment, multimodal supervision, reasoning assessment, scalable data generation), and revealing structural gaps in existing datasets/benchmarks/data engines regarding the fidelity-cost trade-off, compositional generalization evaluation, and sim-to-real transfer.
  * Fairness assessment: the fairness of survey-type papers depends on the comprehensiveness of their literature coverage and whether their classification has representative bias; this paper has passed TMLR peer review, giving it a degree of academic vetting, but the abstract itself does not state how many papers were covered or the time range covered, and this needs to be checked against the full paper's methodology section to assess its degree of systematicity.
  * Needs checking against comparative data in other papers: since this is a survey, whether its conclusions align with the judgments of other similar surveys requires further comparison; the abstract does not provide relevant comparative information.

### Limitation

  * The abstract does not contain an explicitly stated limitations section; this needs to be checked against the full paper (survey papers typically discuss the cutoff date of their literature coverage, the subjectivity of the classification framework, and emerging sub-fields not covered).
  * Inferred from the main content, potential limitations may include: although the three-pillar framework is systematic, it may not fully cover every aspect of VLA data infrastructure (such as data annotation quality control, privacy, and data licensing issues), and as a survey it inevitably has a literature cutoff date limitation, possibly not covering the newest datasets/benchmarks published after April 2026.

### Related work

  * This survey itself is a systematic organization of related work; the benchmark issues it covers (compositional generalization, long-horizon reasoning evaluation gaps) resonate strongly with VLABench (emphasizing long-horizon reasoning tasks), vla-eval (emphasizing engineered evaluation pipelines), and VLA-REPLICA (emphasizing real-world reproducibility) from the same batch of papers, and can be seen as explaining the problem context behind these specific benchmark/tool papers.
  * No newer VLA data-infrastructure survey of comparable systematicity has been found so far.
  * High survey value for related work: as a peer-reviewed systematic survey, it is very well suited as an introductory and map-like reference for researching VLA data/benchmark issues, especially for teams wanting to plan data collection or evaluation strategies.

### Conclusion

  * Overall assessment: this is a high-quality survey with a clear problem awareness and peer-review vetting, very much worth referencing for readers who want to systematically understand the current state and challenges of VLA data infrastructure (especially engineering teams planning data collection/evaluation strategies).
  * Relationship to other important work: this survey provides a higher-level problem context for concrete benchmark/tool papers from the same batch, such as VLABench, vla-eval, and VLA-REPLICA, explaining which of the structural gaps mentioned in the survey each tool addresses.
  * ROCm/AMD relevance: the survey focuses on data and evaluation infrastructure rather than underlying compute hardware/accelerator selection, so no clear direct connection to ROCm/AMD can be seen; however, the large-scale data generation and simulation it mentions have high compute resource demands, and if AMD wants to enter this field, a possible opportunity is providing ROCm-accelerated simulation/rendering pipelines for simulation-based data engines — but the abstract itself does not provide specific details supporting this judgment; this is a speculative direction that needs further verification.
