---
layout: paper
title: "PhyGround: Benchmarking Physical Reasoning in Generative World Models"
section: wm
page_id: "1945539592"
permalink: /en/wm/phyground-benchmarking-physical-reasoning-in-generative-world-models-1945539592/
---

**Paper** : [PhyGround: Benchmarking Physical Reasoning in Generative World Models](https://arxiv.org/abs/2605.10806)  
**Source** : arXiv (cs.CV / cs.AI / cs.LG), Preprint, Project page: <https://phyground.github.io/>  
**arXiv ID** : 2605.10806

### Abstract

PhyGround is a benchmark designed to evaluate whether generative world models (video generation models) truly understand physical laws. The authors point out that while existing physics-oriented video benchmarks have made progress, they still face three major challenges: evaluation frameworks that are too coarse-grained and mask failures at the level of specific physical laws, annotator response bias and fatigue that affect the validity of judgments, and automated evaluators that are insufficiently sensitive to physics or difficult to audit. PhyGround includes 250 curated prompts, each paired with an expected physical outcome, and covers a taxonomy of 13 categories of physical laws spanning solid mechanics, fluid dynamics, and optics, with each law broken down into observable sub-questions to support per-law diagnosis. The authors evaluate 8 modern video generation models through a large-scale, quality-controlled human study (drawing on social science experimental design), with 459 annotators providing 5,796 complete annotations and over 37,400 fine-grained labels; after quality control, the retained annotations show a high split-half model ranking correlation (Spearman's rho > 0.90). To support reproducible automated evaluation, the authors also release PhyJudge-9B, an open-source, physics-specialized vision-language model (VLM) judge, whose overall relative bias is significantly lower than that of Gemini-3.1-Pro (3.3% versus 16.6%).

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539592_phyground_fig1.png) 

_Figure 1: Overview of PhyGround - decomposing each video generation model's overall physical reasoning score into individual scores across 13 categories of physical laws, evaluated through large-scale, quality-controlled human evaluation by 459 annotators._

![Figure]({{ site.baseurl }}/assets/images/1945539592_phyground_fig5.png) 

_Figure 5: Annotation design workflow - architecture diagram of PhyGround's human annotation process design._

  * **Problem addressed**: How to rigorously and fine-grainedly evaluate whether video generation / world models obey real-world physical laws, rather than masking failures on specific physical laws with coarse overall scores; and at the same time addressing the instability of human annotation quality (bias, fatigue) and the insufficient physical knowledge and auditability of automated evaluators.
  * **Main method**: PhyGround establishes a "criteria-grounded" benchmark, with the core design including:
    * 250 curated prompts, each annotated with an expected physical outcome.
    * A taxonomy of 13 categories of physical laws spanning solid mechanics, fluid dynamics, and optics.
    * Each law is decomposed into observable sub-questions, enabling per-law diagnosis rather than a single overall score.
    * Drawing on social science experimental design methods to control the quality of large-scale human annotation (459 people, 5,796 annotations, 37.4K fine-grained labels), and using a split-half method to verify annotation reliability.
    * Releasing PhyJudge-9B, an open-source VLM judge trained with enhanced physical knowledge, to enable automated reproduction of the evaluation.
  * **Difference from prior approaches**: Previous physics-oriented video benchmarks often entangle multiple physical concepts/laws within a single test item, making it difficult to pinpoint the exact cause of failure. PhyGround achieves disentangled evaluation by decomposing laws into sub-questions, and uses social-science-grade experimental design to control the quality of human annotation, while also providing a specialized evaluation model with lower bias than general-purpose VLMs (such as Gemini-3.1-Pro).
  * **Key design details**: The entire evaluation process can be imagined as three layers — (1) Prompt layer: 250 prompts covering 13 categories of physical laws, each with an explicit "expected physical outcome" description; (2) Generation layer: 8 modern video generation models each generate videos according to the prompts; (3) Evaluation layer: for each generated video, annotators score a set of observable sub-questions under that law item by item (e.g., "does the object maintain constant volume," "does the fluid behave according to expected viscosity"), forming fine-grained labels; meanwhile, PhyJudge-9B serves as an automated substitute evaluator, and after being trained/calibrated on quality-controlled human labels, can reproduce the evaluation results without requiring large-scale human annotation.

### Result

  * **Main results**: A large-scale human evaluation of 8 modern video generation models was completed (5,796 annotations, 37.4K fine-grained labels), with annotation quality validated by split-half analysis achieving high correlation (Spearman's rho > 0.90), indicating stable and credible evaluation results. Meanwhile, PhyJudge-9B shows lower evaluation bias compared to Gemini-3.1-Pro (3.3% versus 16.6%).
  * **Contributions**: The main contributions are enhancing "fine-grained diagnostic ability for physical reasoning evaluation" (per-law analysis rather than an overall score) and "the physical accuracy/auditability of automated evaluation" (PhyJudge-9B outperforming general-purpose large VLMs).
  * **Fairness**: The comparison between PhyJudge-9B and Gemini-3.1-Pro bias (3.3% vs 16.6%) provided in the abstract is the authors' own evaluation result, and is a self-reported comparison. Since this is a newly released benchmark (May 2026), it currently needs to be verified whether other papers have used PhyGround to re-evaluate the same or different sets of models to verify ranking consistency.

### Limitation

  * **Limitations stated by the authors**: Based only on the arXiv abstract page, the abstract itself does not detail the limitations section (the full paper is 56 pages with 39 figures and 40 tables, and verification of the limitations/discussion section in the full text is needed).
  * **Weaknesses inferred from the results**:
    * Only 8 modern video generation models were evaluated, and this coverage may not represent all mainstream models (especially since new models are updated rapidly, and the benchmark may quickly become outdated).
    * Although the large-scale crowd annotation (459 people) underwent quality control, human subjective judgments of "physical correctness" may still vary across cultural/background differences; while the paper draws on social science experimental design to control for this, subjectivity cannot be completely eliminated.
    * As a 9B-scale specialized model, whether PhyJudge-9B's physical knowledge coverage can generalize to physical phenomena not covered by PhyGround (e.g., electromagnetism, thermodynamics, and other domains not included in the 13 categories of laws) is not addressed in the abstract.

### Related work

  * Other papers' comparison data need to be verified: PhyGround shares a highly similar theme with the contemporaneous (2601, i.e., January 2026) WorldBench (arXiv:2601.21282, another paper processed in this same batch), both focusing on disentangled evaluation of physical laws. It is worth cross-comparing the taxonomy design, evaluation scale, and identified model failure modes of the two.
  * **How worth surveying this related work is**: High. Physical reasoning evaluation is currently a popular sub-direction in the world model / video generation field (PhyGround, WorldBench, and other benchmarks appeared densely in the first half of 2026), and it is recommended to compile a small survey specifically comparing the taxonomies and findings of various benchmarks.

### Conclusion

  * **Overall assessment**: PhyGround is a methodologically rigorous (drawing on social science experimental design), large-scale (37.4K labels) benchmark for physical reasoning that also provides a reproducible automated evaluation tool (PhyJudge-9B). It is highly valuable for researchers who want to systematically evaluate or improve the physical consistency of world models; its "disentangled" evaluation design philosophy is also worth emulating for other benchmarks.
  * **Relationship to other important papers**: It has a direct methodological competitive/complementary relationship with WorldBench (also a physics-disentangled evaluation benchmark that appeared in 2026); both point out that existing video generation models are generally insufficient in physical consistency. It is recommended to study both papers together and compare their taxonomy differences.
  * **ROCm/AMD gaps**: The paper does not mention the hardware platform used for training/inference, so no clear connection to ROCm/AMD can be identified. If an AMD team wants to use PhyGround to evaluate their own (or ROCm-trained/inferred) world models, they can directly adopt its publicly released prompts, human annotations, and PhyJudge-9B evaluator, but the paper itself does not involve ROCm-related content, so it would not be appropriate to speculate further.
