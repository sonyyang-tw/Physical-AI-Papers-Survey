---
layout: paper
title: "WholeBodyVLA: Towards Unified Latent VLA for Whole-Body Loco-Manipulation Control"
section: vla
page_id: "1945392363"
permalink: /en/vla/wholebodyvla-towards-unified-latent-vla-for-whole-body-loco-manipulation-control-1945392363/
---

**Paper** : [WorldBench: Benchmarking Physical Understanding of World Models by Isolating Physics Concepts](https://arxiv.org/abs/2601.21282)  
**Source** : arXiv (cs.CV), Project page: <https://world-bench.github.io/>  
**arXiv ID** : 2601.21282

### Abstract

WorldBench is a video-based benchmark specifically designed to evaluate generative world models' understanding of physics concepts, with a core design philosophy of "disentanglement" — each test isolates and evaluates a single physical concept or law, rather than entangling multiple physical laws in a single score. The authors point out that existing physics-oriented video benchmarks often suffer from an "entanglement" problem: a single test simultaneously evaluates multiple physical laws and concepts, which fundamentally limits diagnostic capability. WorldBench designs two levels of evaluation: (1) intuitive physics understanding, covering higher-level concepts such as object permanence and scale/perspective relationships; (2) low-level physical constants and material properties, such as coefficients of friction and fluid viscosity, precisely measuring the degree of deviation between generated video and the real world. The authors evaluated multiple SOTA video-based world models and found that these models exhibit clear and consistent failure modes on specific physical concepts, and that all tested models lack the physical consistency required to produce reliable real-world interactions.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392363_wholebodyvla_fig1.png) 

_Figure 1: WholeBodyVLA teaser._

![Figure]({{ site.baseurl }}/assets/images/1945392363_wholebodyvla_fig2.png) 

_Figure 2: WholeBodyVLA pipeline._

  * Problem addressed: Test items in existing physics-oriented video benchmarks often involve multiple physical laws/concepts simultaneously (entanglement), making it impossible to precisely pinpoint which specific physical concept a model fails on, thereby limiting diagnostic capability.
  * Main method: WorldBench proposes a "concept-specific, disentangled" evaluation framework, designing two levels of benchmarks:
    * High-level intuitive physics understanding: tests concepts such as object permanence (whether an object is still considered to "exist" after being occluded) and scale/perspective relationships — physical concepts at the level of human intuition.
    * Low-level physical constants and material properties: tests specific, quantifiable physical quantities such as coefficients of friction and fluid viscosity, thereby measuring the quantitative gap between generated video and real physical phenomena.
  * Difference from prior approaches: Test items in previous benchmarks often involved multiple physical laws at once (e.g., a scene of "a ball rolling down a slope" simultaneously involves gravity, friction, and elastic collision), so when a failure occurs, it cannot be attributed to a specific law; WorldBench deliberately designs each test to isolate a single concept/law, making diagnosis more precise and the benchmark more extensible.
  * Key design description: The whole benchmark can be imagined as split into two testing tracks — the intuitive physics track designs specific scenarios (e.g., an object temporarily occluded, changes in camera scale) to examine whether the model maintains "common-sense-level" physical understanding such as object continuity and size/distance relationships; the low-level physical constants track uses controlled physical scenarios (e.g., a specific material sliding on a specific surface, the flow behavior of a liquid with a specific viscosity) to quantify the deviation between the model's generated output and the true values of known physical constants/material properties. Both tracks are video-based evaluations — a world model generates video from an input prompt, and the generated result is then scored according to pre-designed physical criteria.



### Result

  * Main result: Multiple SOTA video-based world models were evaluated, and it was found that "all tested models exhibit failure modes on specific physical concepts" and generally lack the physical consistency required to produce reliable real-world interactions; through disentangled evaluation, the benchmark can precisely pinpoint which specific physical concepts (e.g., friction, viscosity, object permanence) a model performs poorly on.
  * Improvements: The main improvements are in the "diagnostic granularity of physical-understanding evaluation" (compared to a single overall score, per-concept analysis is now possible) and "extensibility" (new physical concepts can be added to the benchmark in a modular fashion).
  * Fairness: The abstract does not provide specific model rankings or detailed score tables (only the qualitative conclusion that "all models have failure modes"), making it difficult to directly compare the relative strengths of different models. It would be necessary to check whether other papers (especially the concurrent PhyGround, arXiv:2605.10806) reach similar or different evaluation conclusions on the same or overlapping set of models, in order to confirm the consistency of the results.



### Limitation

  * Limitations stated by the authors: Based solely on information from the arXiv abstract page, the abstract itself does not explicitly list a limitations section; the full text needs to be checked to confirm the authors' self-stated limitations.
  * Weaknesses inferred from the results:
    * The paper's core finding is that "all models have deficiencies in physical understanding," which, while a meaningful diagnostic result, also means there is currently no model that can serve as a positive control representing "good physical understanding," which may reduce the comparability of the benchmark (which model is relatively better).
    * The evaluation of low-level physical constants (e.g., friction coefficient, viscosity) relies on human or automated judges assessing whether the generated video's "visual appearance" matches a specific physical quantity; this kind of visual-level quantitative judgment may itself carry error or subjectivity, and the abstract does not describe how the reliability of the judging method was validated.
    * The paper went through revisions from v1 (January 2026) to v2 (August 2026), spanning nearly half a year, which may reflect adjustments to the evaluation method or model set; the differences between versions need to be checked.



### Related work

  * Highly overlapping in topic and methodology with the concurrent PhyGround (arXiv:2605.10806, another paper handled in this same batch); both adopt a "disentangled" evaluation philosophy but present it differently (WorldBench splits into "intuitive physics" and "physical constants" tiers; PhyGround uses a 13-category law taxonomy plus the PhyJudge-9B judge model). It is recommended to cross-compare the evaluation methods and findings of the two for the same physical concepts (e.g., friction, fluid behavior) to see whether they are consistent.
  * Degree to which the related work is worth surveying: high. Physical-consistency evaluation is a popular sub-direction of world model research in the first half of 2026, worth compiling into a small survey systematically comparing WorldBench, PhyGround, and other similar benchmarks.



### Conclusion

  * Overall assessment: WorldBench's "disentangled" evaluation philosophy is clear and persuasive, effectively solving the problem of diagnostic ambiguity caused by traditional physics-oriented benchmarks entangling multiple physical concepts in a single test item. It is worth referencing for researchers who want to systematically understand the physical weaknesses of world models; however, since the full text has not been read, specific model ranking data and validation of the reliability of the judging method remain to be verified.
  * Relationship to other important papers: Forms two different solution paths addressing the same problem consciousness at the same period alongside PhyGround; it is recommended to study and compare both together. Their shared conclusion (that existing world models generally lack physical consistency) also echoes the broader skepticism in the embodied AI field about whether world models can truly support robot planning and simulation.
  * Areas needing further ROCm/AMD investigation: The paper does not mention the hardware or framework used for training/evaluation, so no clear connection to ROCm/AMD can be identified; this should not be speculated upon. If an AMD team wants to use WorldBench to evaluate the physical consistency of their own ROCm-trained world models, they could directly adopt its published evaluation framework, but that would be a user-driven extension application rather than content of the paper itself.
