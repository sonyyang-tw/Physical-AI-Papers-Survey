---
layout: paper
title: "VLA-REPLICA: A Low-Cost, Reproducible Benchmark for Real-World Evaluation of Vision-Language-Action Models"
section: vla
page_id: "1945392290"
permalink: /vla/vla-replica-a-low-cost-reproducible-benchmark-for-real-world-evaluation-of-visio-1945392290/
---

**Paper** : [VLA-REPLICA: A Low-Cost, Reproducible Benchmark for Real-World Evaluation of Vision-Language-Action Models](https://arxiv.org/abs/2605.20774)  
**Source** : arXiv (cs.RO)  
**arXiv ID** : 2605.20774

### Abstract

VLA models have shown strong potential for general-purpose robotic manipulation, but their real-world evaluation has long been limited by the lack of an accessible, reproducible, and consistent benchmark. Simulation benchmarks cannot capture the complexity of the real world, while existing real-world benchmarks typically require expensive hardware, centralized evaluation pipelines, or offer limited task diversity. This paper proposes VLA-REPLICA, a low-cost, easily reproducible real-world VLA evaluation benchmark. The system is built from off-the-shelf components, can be assembled quickly, and can be replicated across different labs, providing a consistent environment for policy evaluation that can be reproduced anywhere in the world. VLA-REPLICA includes a diverse suite of manipulation tasks, along with a small-scale demonstration dataset for target-domain adaptation, and provides real-world evaluation protocols for both in-distribution and out-of-distribution settings. Experiments with imitation learning and state-of-the-art VLA models reveal the strengths and limitations of these models, and consistent results across independently built setups demonstrate the reproducibility of the benchmark.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392290_vlareplica_fig1.png) 

_Figure 1: VLA-REPLICA overview._

![Figure]({{ site.baseurl }}/assets/images/1945392290_vlareplica_fig2.png) 

_Figure 2: VLA-REPLICA method architecture._

  * Problem addressed: The accessibility and reproducibility of real-world VLA evaluation — simulated evaluation cannot reflect the complexity and noise of the real world, while existing real-world benchmarks typically require expensive, dedicated hardware or centralized evaluation (e.g., only runnable on robots at a specific lab), making it difficult for different teams to fairly compare each other's model performance.
  * Main method: A low-cost real-robot evaluation platform built from "off-the-shelf components" is proposed, which can be assembled independently at different labs while still producing consistent results. It includes a diverse set of manipulation tasks and a small-scale demonstration dataset supporting domain adaptation of models for target scenarios. The evaluation protocol covers both in-distribution scenarios (tasks/scenes similar to the training distribution) and out-of-distribution scenarios (tasks/scenes outside the training distribution, testing generalization ability).
  * Difference from prior approaches: Unlike existing benchmarks that require expensive robot arms, dedicated grippers, or must be sent to a centralized lab for evaluation, VLA-REPLICA emphasizes "low cost" and "reproducibility," allowing different institutions to independently build the same hardware configuration locally and obtain consistent evaluation results, lowering the barrier to real-world VLA evaluation.
  * Key design description: The overall system pipeline is roughly: (1) assemble a standardized robotic manipulation platform from off-the-shelf components; (2) collect a small-scale demonstration dataset for target-domain fine-tuning of each task; (3) carry out evaluation under in-distribution and out-of-distribution settings following a standardized protocol; (4) verify the consistency (reproducibility) of results by repeating experiments across multiple independently built setups, thereby confirming that the platform itself does not introduce excessive evaluation error due to assembly differences.



### Result

  * The results show that experiments with imitation learning and state-of-the-art VLA models reveal the strengths and weaknesses of each model (the abstract does not list specific numerical scores). Consistent results across independently built setups demonstrate the reproducibility of the benchmark, which is its core selling point.
  * The abstract does not provide specific success rates or quantitative cross-model comparison figures, so the specific magnitude of "which aspects were mainly improved" cannot be judged here; the experimental sections and tables in the full text need to be checked.
  * Fairness and consistency with other papers' results: Comparison data from other papers would need to be checked. Since this is a newly proposed real-world benchmark, its results currently cannot be directly compared with existing scores from other benchmarks (different hardware platforms, different task designs).



### Limitation

  * The abstract does not explicitly list limitations stated by the authors; the full text needs to be checked (such papers typically discuss task diversity, hardware coverage, and the gap relative to industrial-grade robot platforms).
  * Potential weaknesses inferred from the abstract: Using "off-the-shelf components" lowers cost and improves reproducibility, but may not fully represent the manipulation precision and challenges of industrial-grade or higher-degree-of-freedom robots; the small-scale demonstration dataset may also limit the depth of generalization evaluation after model fine-tuning.



### Related work

  * No newer related research was found (this paper was submitted in May 2026, making it one of the newer real-world benchmark papers in this list).
  * It forms a complementary relationship with vla-eval (a simulation evaluation tool), VLABench (a simulated long-horizon task benchmark), and the VLA survey (analyzing gaps in datasets/benchmarks) in the same batch, particularly echoing the "simulation cannot capture real-world complexity" issue mentioned in the survey.
  * Degree to which the related work is worth surveying: medium. For teams looking to build a low-cost real-world evaluation pipeline, this paper provides a concrete, actionable reference architecture, worth tracking for its open-source materials (if any).



### Conclusion

  * Overall assessment: This paper offers a solution to the practical pain point of "VLA real-world evaluation being difficult to democratize and reproduce," a pragmatic direction that directly benefits the community, especially valuable for teams without large robotics lab resources.
  * Relationship to other important papers: Complementary to vla-eval (a simulation evaluation tool) — vla-eval solves the engineering integration problem of simulated evaluation, while VLA-REPLICA solves the accessibility and reproducibility problem of real-world evaluation; together, they echo the structural issue of "lack of standardized benchmark protocols" pointed out in the VLA survey (2604.23001).
  * Relevance to ROCm/AMD: No clear connection to ROCm/AMD hardware can be identified; this paper focuses on the reproducibility of robot hardware platforms and evaluation protocols rather than the computing hardware or accelerators used for model training/inference, so no direct impact on the ROCm ecosystem can be determined.
