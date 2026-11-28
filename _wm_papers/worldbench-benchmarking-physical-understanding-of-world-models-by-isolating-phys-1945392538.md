---
layout: paper
title: "WorldBench: Benchmarking Physical Understanding of World Models by Isolating Physics Concepts"
section: wm
page_id: "1945392538"
permalink: /wm/worldbench-benchmarking-physical-understanding-of-world-models-by-isolating-phys-1945392538/
---

**Paper** : [WorldBench: Benchmarking Physical Understanding of World Models by Isolating Physics Concepts](https://arxiv.org/abs/2601.21282)  
**Source** : arXiv (cs.CV), project page: <https://world-bench.github.io/>  
**arXiv ID** : 2601.21282

### Abstract

WorldBench is a video-based benchmark specifically designed to evaluate the physical understanding of generative world models, whose core design philosophy is "disentanglement"—each test isolates and evaluates a single physical concept or law, rather than entangling multiple physical laws in a single score. The authors point out that existing physics-oriented video benchmarks commonly suffer from an "entanglement" problem: a single test simultaneously evaluates multiple physical laws and concepts, which fundamentally limits diagnostic ability. WorldBench designs two levels of evaluation: (1) an intuitive physics understanding level, covering higher-level concepts such as object permanence and scale/perspective relationships; (2) a low-level physical constants and material properties evaluation, such as friction coefficients and fluid viscosity, thereby precisely measuring the degree of deviation between generated video and the real world. The authors evaluate several SOTA video-based world models and find that these models exhibit clear and consistent failure modes on specific physical concepts, and that all tested models lack the physical consistency needed to produce reliable real-world interactions.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392538_worldbench_fig1.png) 

_Figure 1: Overview of the WorldBench generation and evaluation pipeline (Kubric/PyBullet/Blender generate scenes, and world models are evaluated with multi-level physics tasks)._

![Figure]({{ site.baseurl }}/assets/images/1945392538_worldbench_fig2.png) 

_Figure 2: Overview of the physical parameter estimation pipeline — estimating physical constants from input video via checkerboard detection and SAM2-extracted 3D positions._

  * Problem being addressed: existing physics-oriented video benchmarks often have test items that involve multiple physical laws/concepts simultaneously (entanglement), making it impossible to precisely pinpoint which specific physical concept a model fails on, limiting diagnostic ability.
  * Main method: WorldBench proposes a "concept-specific, disentangled" evaluation framework, designing two levels of benchmarks:
    * High-level intuitive physics understanding: tests such as object permanence (whether an object still "exists" after being occluded) and scale/perspective relationships—human-intuitive-level physical concepts.
    * Low-level physical constants and material properties: tests such as friction coefficients and fluid viscosity—concrete, quantifiable physical quantities, used to measure the quantitative gap between generated video and real physical phenomena.
  * Difference from prior approaches: in previous benchmarks, a single test item often involved multiple physical laws simultaneously (e.g., a scene of "a ball rolling down a slope" simultaneously involves gravity, friction, and elastic collision), so failures could not be attributed to a specific law; WorldBench deliberately designs each test to isolate and test only a single concept/law, making diagnosis more precise and scalable.
  * Description of key method design: one can imagine the entire benchmark as divided into two testing tracks—the intuitive physics track designs specific scenarios (e.g., an object temporarily occluded, or camera scale changes) to examine whether the model maintains object continuity, size/distance relationships, and other "common-sense-level" physical understanding; the low-level physical constants track uses controlled physical scenarios (e.g., an object of a specific material sliding on a specific surface, or the flow behavior of a liquid of a specific viscosity) to quantify the deviation between the model's generated results and known ground-truth physical constants/material properties. Both tracks are video-based evaluations, meaning that an input prompt is used by the world model to generate a video, which is then scored against designed physics criteria.



### Result

  * Main finding: multiple SOTA video-based world models were evaluated, and it was found that "all tested models exhibit failure modes on specific physical concepts" and generally lack the physical consistency needed to produce reliable real-world interactions; through disentangled evaluation, the benchmark can precisely pinpoint which specific physical concepts (such as friction, viscosity, object permanence, etc.) a model performs poorly on.
  * What was primarily enhanced: mainly the "diagnostic granularity" of physical understanding evaluation (compared to a single overall score, allows concept-by-concept analysis) and "scalability" (new physical concepts can be added to the benchmark in a modular fashion).
  * Fairness: the abstract does not provide specific model rankings or score table details (only describing the qualitative conclusion that "all models have failure modes"), making it difficult to directly compare the relative strengths of different models; it is necessary to verify whether other papers (especially the contemporaneous PhyGround, arXiv:2605.10806) reach similar or different evaluation conclusions on the same or overlapping set of models, to confirm the consistency of the results.



### Limitation

  * Self-reported limitations: based only on information from the arXiv abstract page, the abstract itself does not explicitly list a Limitation section; this needs to be verified against the full paper to confirm the authors' self-reported limitations.
  * Weaknesses inferred from the results:
    * The paper's core finding is that "all models have physical understanding deficiencies," which, while a meaningful diagnostic result, also means there is currently no model that can serve as a positive control with "good physical understanding," which may reduce the comparability of the benchmark (i.e., which model is relatively better).
    * The evaluation of low-level physical constants (e.g., friction coefficient, viscosity) relies on human or automated judges assessing whether the generated video visually conforms to specific physical quantities; this kind of visual-level quantitative judgment may itself carry error or subjectivity, and the abstract does not describe how the reliability of the judging method was validated.
    * The paper has undergone revisions from v1 (January 2026) to v2 (August 2026), spanning nearly half a year, which may reflect adjustments to the evaluation method or model set; the differences between versions need to be verified.



### Related work

  * This paper overlaps significantly in topic and methodology with the contemporaneous PhyGround (arXiv:2605.10806, another paper handled in the same batch). Both adopt a "disentangled" evaluation philosophy but present it differently (WorldBench divides into "intuitive physics" and "physical constants" levels; PhyGround uses a 13-category law taxonomy plus a judge model, PhyJudge-9B). It is recommended to cross-compare the evaluation methods and findings of the two papers on the same physical concepts (such as friction and fluid behavior) to see whether they are consistent.
  * Assessment of how worth surveying the related work is: high. Physical consistency evaluation is a popular sub-direction in world model research in the first half of 2026, worth organizing into a small survey systematically comparing WorldBench, PhyGround, and other similar benchmarks.



### Conclusion

  * Overall assessment: WorldBench's proposed "disentangled" evaluation philosophy is clear and persuasive, effectively addressing the problem of ambiguous diagnosis in traditional physics-oriented benchmarks caused by entangling multiple physical concepts in a single test item. It is worth referencing for researchers who want to systematically understand the physical weaknesses of world models; however, since the full text has not been read, specific model ranking data and validation of judging method reliability remain to be verified.
  * Relationship to other important papers: it forms two different solution routes to the same problem and time period alongside PhyGround, and is recommended for joint reading and comparison; the shared conclusion of both papers (that existing world models generally lack physical consistency) also echoes the general skepticism in the embodied AI field about "whether world models can truly support robot planning and simulation."
  * Areas for ROCm/AMD to strengthen: the paper does not mention the hardware or framework used for training/evaluation, so no clear connection to ROCm/AMD is apparent, and it should not be speculated. If an AMD team wants to use WorldBench to evaluate the physical consistency of their own world models trained with ROCm, they could directly adopt its public evaluation framework, but this falls under user extension rather than the content of the paper itself.
