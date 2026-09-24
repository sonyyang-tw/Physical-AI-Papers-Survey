---
layout: paper
title: "LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks"
section: vla
page_id: "1945538792"
permalink: /vla/lohovla-a-unified-vision-language-action-model-for-long-horizon-embodied-tasks-1945538792/
---

**Paper** : [LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks](https://arxiv.org/abs/2506.00411)  
**Source** : arXiv  
**arXiv ID** : 2506.00411

### Abstract

Real-world embodied agents often face long-horizon tasks—high-level goals that require multiple steps to accomplish rather than a single action. Successfully handling such tasks requires both high-level task planning (decomposing the goal into subtasks) and low-level action control (generating precise robot actions). Existing VLA models often perform poorly at planning, while hierarchical architectures are prone to coordination problems. This paper proposes LoHoVLA, a unified VLA framework that leverages a large pretrained vision-language model (VLM) as its backbone, simultaneously generating language tokens (for subtask generation) and action tokens (for robot action prediction), paired with a hierarchical closed-loop control mechanism to reduce errors arising from both high-level planning and low-level control. The authors also constructed the LoHoSet dataset (based on the Ravens simulator, 20 long-horizon tasks, 1000 expert demonstrations per task) for training and validation.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945538792_lohovla_fig1.png) 

_Figure 1: LoHoVLA overview and method architecture diagram — the top compares the vanilla VLA with a hierarchical architecture, and the bottom shows the overall architecture of the LoHoVLA unified model, which simultaneously generates language subtask tokens and action tokens._

  * **Problem addressed**: Long-horizon embodied tasks require both "task planning" and "action control" simultaneously; standard VLA models often fail at the planning stage, while hierarchical architectures (with separate planner and controller) are prone to coordination inconsistency between the two layers.
  * **Main method**: LoHoVLA uses a single large pretrained VLM as a shared backbone, simultaneously outputting language tokens (subtask descriptions) and action tokens (robot actions), so both share the same representation, improving generalization across tasks; it also incorporates a "hierarchical closed-loop control" mechanism, allowing feedback and error correction between the high-level planning results and low-level execution results.
  * **Differences from prior approaches**: Standard monolithic VLA models typically map language instructions directly to actions, lacking an explicit subtask planning step; traditional hierarchical architectures separately train/deploy a planner and a controller, which are prone to inter-module inconsistency. LoHoVLA merges the two using a "unified model, shared representation" approach, while retaining a closed-loop correction mechanism.
  * **Architecture/pipeline description**: After receiving visual observations and a language goal, the VLM backbone first generates a subtask in the form of language tokens, then the same model continues to generate the corresponding robot action tokens; during execution, closed-loop feedback (observing execution results and feeding them back to the planning/control modules) continuously corrects subtasks and actions, reducing failures caused by planning errors or accumulated control error.



### Result

  * Experiments show that LoHoVLA significantly surpasses both hierarchical methods and standard VLA methods on long-horizon embodied tasks in the Ravens simulator.
  * The abstract does not provide specific numbers (such as success rate percentages), only describing its advantage as "significantly surpasses"; the full text needs to be checked to obtain quantitative comparison data.
  * Fairness: current evaluation is limited to the authors' self-built LoHoSet dataset (based on the Ravens simulator), rather than a general public benchmark (such as LIBERO), so its generalizability and cross-benchmark comparison require checking comparison data from other papers.



### Limitation

  * At the abstract level, the paper does not explicitly state a limitations section.
  * From the method design, the evaluation dataset is self-built (LoHoSet), and the task variety (20 tasks) and simulator (Ravens) scope are relatively limited, which may risk a "tailor-made for the self-built dataset" bias toward optimistic results.
  * The abstract does not mention whether there is real-robot validation, being limited to simulator experiments only; actual deployment feasibility requires checking the full text.



### Related work

  * The abstract mentions comparisons with "existing VLA models" and "hierarchical architectures," but does not list specific comparison paper names.
  * No newer directly comparable follow-up research was found (this paper was published in May 2025; whether there is direct follow-up work needs further verification).
  * Worth surveying related work: medium. The "unified language + action token generation" approach proposed here is relevant to the core issue explored by papers like DeepThinkVLA and LaRA-VLA ("CoT/reasoning injection")—how to incorporate high-level semantic planning into action generation—worth comparing within the same context.



### Conclusion

  * This paper is one of the earlier (May 2025) representative works proposing the idea of "a unified model simultaneously handling long-horizon planning and action control," of reference value for understanding the design lineage of "planning-control integration" in the VLA field. However, since it is validated only on a self-built simulation dataset, before engineering adoption it is recommended to first check the full text for real-robot results and broader benchmark comparisons.
  * Relationship to other important papers: this paper is one of the pioneering works in the "unified VLA framework for long-horizon tasks" route; subsequent papers such as DeepThinkVLA and LaRA-VLA can be seen as extensions of the same broader direction on the question of "how to make the model perform multi-step reasoning before acting" (though via different specific technical paths: LoHoVLA takes the subtask language token generation route, while DeepThinkVLA/LaRA-VLA take the explicit or latent CoT reasoning route).
  * Relevance to ROCm/AMD: the abstract does not mention training/inference hardware or framework details, so no clear connection to ROCm/AMD can be discerned; the full text's implementation environment needs to be checked.
