---
layout: paper
title: "iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework"
section: wm
page_id: "1945539121"
permalink: /en/wm/iworld-bench-a-benchmark-for-interactive-world-models-with-a-unified-action-gene-1945539121/
---

**Paper** : [iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework](https://arxiv.org/abs/2605.03941)  
**Source** : arXiv (cs.CV, cs.AI), Accepted at ICML 2026  
**arXiv ID** : 2605.03941

### Abstract

Achieving artificial general intelligence (AGI) requires agents capable of adaptive learning and interaction, and interactive world models provide a scalable environment for perception, reasoning, and action. However, current research still lacks large-scale datasets and unified benchmarks to evaluate their physical interaction capabilities. This paper proposes iWorld-Bench, a comprehensive benchmark for training and testing world models' performance on interaction-related capabilities such as "distance perception" and "memory." The authors construct a diverse dataset containing 330,000 video clips, and select 2,100 high-quality samples covering different viewpoints, weather conditions, and scenes. Since existing world models differ in their interaction modes (action modality), the authors propose an "Action Generation Framework" to unify the evaluation standard, designing six task types that together produce 4,900 test samples, jointly assessing model performance in visual generation, trajectory following, and memory. The authors evaluate 14 representative world models, identifying key limitations and providing insights for future research. The leaderboard is publicly available at iWorld-Bench.com.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539121_iworldbench_fig1.png) 

_Figure 1: iWorld-Bench overview, covering four viewpoints — UGV/UAV/human/robot — combined with a unified Action Generation Framework to evaluate interactive world models._

![Figure]({{ site.baseurl }}/assets/images/1945539121_iworldbench_fig2.png) 

_Figure 2: Data processing pipeline and overview, including the four steps of data collection, unification, VLM-assisted annotation, and human verification._

  * **Problem addressed**: The interactive input modes of different world models (the form of action conditioning, such as text instructions, trajectory coordinates, keyboard keys, etc.) are not unified with each other, making it difficult to use a single benchmark for fair comparison; at the same time, the industry lacks large-scale interaction-capability evaluation data covering diverse scenarios (different viewpoints/weather/scenes).
  * **Main method**:
    * Constructs a 330k video clip dataset, filters it down to 2.1k high-quality samples covering variations in viewpoint, weather, and scene.
    * Proposes an "Action Generation Framework" that converts/unifies the different action input forms of various world models into a comparable evaluation interface.
    * Based on this framework, designs 6 task types (covering visual generation quality, trajectory-following accuracy, and long-term memory retention ability), together generating 4.9k test samples.
    * Evaluates 14 representative world models.
  * **Difference from previous approaches**: Previous evaluations of world models were often tied to a specific model's action interface, making cross-model comparison difficult; iWorld-Bench uses a unified action generation framework so that models with different action modalities can be fairly evaluated under the same set of tasks, and additionally emphasizes the two interaction-capability dimensions of "distance perception" and "memory" that have previously been less systematically tested.
  * **Key design description**: The overall pipeline is: data collection (330k clips) → quality filtering (2.1k samples, covering diversity in viewpoint/weather/scene) → generating unified-format action-conditioned input via the Action Generation Framework → batch-generating 4.9k test samples according to six task types → feeding into 14 world models for scoring across the three dimensions of visual generation, trajectory following, and memory → building the leaderboard.



### Result

  * After evaluating 14 representative world models, "key limitations" were identified, but the abstract does not list specific numerical scores; the full text or the iWorld-Bench.com leaderboard needs to be checked to obtain detailed comparison data.
  * Whether it is fair: since this paper has been accepted by ICML 2026 and has undergone peer review, the methodology is relatively credible; but the abstract does not reveal whether the same computational resources/sampling settings were used for all models during evaluation, which needs to be checked in the full text to confirm fairness.
  * It needs to be verified whether the evaluation results of other papers (such as WorldOlympiad) on overlapping models are consistent with this one; the abstract does not provide enough information for direct comparison.



### Limitation

  * The abstract mentions "identifying key limitations," but does not specifically elaborate on what these limitations are, which needs to be checked in the experimental analysis section of the full text.
  * Inferred from the method design, potential weaknesses may include: the Action Generation Framework may introduce approximation error when converting different action modalities, and the unification process itself may disadvantage or favor models with certain native action modalities; the 2.1k high-quality sample scale is still relatively limited and may not fully represent the diversity of real-world interactions.



### Related work

  * The contemporaneous WorldOlympiad (arXiv:2606.11129) is also a world model benchmark paper, but focuses on three tracks of physical/geometric/interaction evaluation, forming a complementary perspective to iWorld-Bench's distance perception/memory/unified action framework, worth reading alongside.
  * No clearly updated follow-up research (such as a paper doing secondary analysis or extension of iWorld-Bench) has been found so far.
  * Degree worth surveying: medium-high, especially for researchers who need to choose an evaluation tool — this paper's unified action framework design approach has practical reference value.



### Conclusion

  * Overall assessment: This is a methodologically rigorous world model benchmark paper that has been accepted by ICML 2026. Its "unified action generation framework" solves the practical pain point of cross-model comparison, providing reference value for researchers who wish to fairly compare different interactive world models.
  * Relationship with other important articles: Belongs to the same 2026 wave of world model evaluation benchmarks as WorldOlympiad, and the two are complementary (the former focuses on distance perception/memory/unified action interfaces, the latter focuses on physical/geometric consistency); it may also be cited as an evaluation method by subsequent VLA / world-model-as-simulator papers (such as WoVR, Interactive World Simulator).
  * Areas for ROCm/AMD improvement: The paper itself focuses on evaluation benchmark design and does not involve underlying hardware or training frameworks, so no direct connection to ROCm can be found; if AMD wants to verify the interactive capabilities of world models trained/inferred on its own hardware, this benchmark can serve as a ready-made evaluation tool for reference.
