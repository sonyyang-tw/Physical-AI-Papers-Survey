---
layout: paper
title: "In-Context World Modeling for Robotic Control"
section: vla
page_id: "1945474654"
permalink: /vla/in-context-world-modeling-for-robotic-control-1945474654/
---

**Paper** : [In-Context World Modeling for Robotic Control](https://arxiv.org/abs/2606.26025)  
**Source** : arXiv (cs.RO / cs.CV)  
**arXiv ID** : 2606.26025

### Abstract

This paper proposes In-Context World Modeling (ICWM), treating "system identification" as an in-context adaptation problem. Modern VLA models typically condition only on "the current observation + language instruction," and thus generalize poorly to changes in setup such as new camera viewpoints or robot morphologies—because they implicitly assume the fixed execution context encountered during training, and any new environment requires extensive fine-tuning data. ICWM enables a robot policy to autonomously infer key system variables from a short history of "self-generated, task-agnostic" interactions. Unlike traditional in-context learning, which uses demonstrations to specify "what task to do," ICWM uses the context window to understand "how the system works." By processing these interactions before executing a task, the model can implicitly capture the current system's world dynamics, allowing it to adapt to new setups without any parameter updates. Extensive experiments on simulation and real robot platforms show that ICWM significantly outperforms standard VLA baselines under novel camera viewpoints.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474654_icwm_fig1.png) 

_Figure 1: Conceptual illustration of In-Context World Modeling (ICWM). Standard VLA models, due to their fixed observation-action assumptions, often fail under new system configurations; just as humans explore an unfamiliar control interface to build a mental world model, ICWM enables a robot to autonomously infer system dynamics through self-probing interaction context._

![Figure]({{ site.baseurl }}/assets/images/1945474654_icwm_fig2.png) 

_Figure 2: Overview of the ICWM training and inference pipeline. (1) Training phase: the model is trained on data collected across multiple system configurations, where task-agnostic interaction segments are prepended to each training sample as context; (2) Inference phase: at test time, the robot first performs random exploration to gather system context, and then uses in-context inference based on this context to guide the policy in generating precise actions._

  * **Problem addressed**: VLA models condition only on the current observation and language instruction, without treating the underlying system configuration (such as camera viewpoint or robot morphology) as a variable, causing any new execution environment to require data-intensive fine-tuning to adapt.
  * **Main method**: ICWM redefines "system identification" as an in-context adaptation problem —
    * Before executing a task, the robot first performs a short segment of "self-generated, task-agnostic" exploratory interaction.
    * The model processes this interaction history within its context window, from which it implicitly infers the dynamic characteristics of the current system (e.g., how the camera viewpoint maps to the action space, the physical constraints of the robot morphology, etc.).
    * Only after inferring the system variables does the model begin executing the specific task, and the entire adaptation process requires no parameter updates.
  * **Differences from prior approaches**: Traditional in-context learning uses demonstration data to tell the model "what task to do," whereas ICWM does the opposite, using contextual interaction to let the model understand "how the system works" — that is, it shifts the goal of in-context learning from task specification to system identification itself, a conceptual pivot.
  * **Key design**: This can be understood as a two-stage process — first an "exploration/calibration" stage (the model gathers system information through task-agnostic self-interaction and implicitly models system dynamics within its context), followed by a "task execution" stage (the same model uses its newly inferred understanding of the system to execute the specific task instruction), with the entire process requiring no gradient updates or fine-tuning.



### Result

  * Extensive experiments on simulation and real robot platforms show that ICWM significantly outperforms standard VLA baselines under "novel camera viewpoints."
  * Fairness: the abstract only mentions the advantage under "novel camera viewpoints" without providing specific numbers (success rate percentages, or which specific baselines were compared), nor does it mention whether results under "robot morphology variation" (the other generalization target mentioned at the start of the abstract) are equally significant; the full text needs to be checked to obtain complete quantitative comparison data and the list of compared baselines.



### Limitation

  * Limitations stated by the paper: the abstract does not explicitly list a limitations section; the full text needs to be checked.
  * Weaknesses inferred from the method design: ICWM relies on "a short segment of self-generated, task-agnostic interaction" to accomplish system identification; if the target environment changes too drastically, or if the exploratory interaction itself fails to reveal sufficient system information (e.g., certain robot morphology differences may not manifest in task-agnostic interaction), the adaptation performance of this method may be limited. In addition, the extra exploration phase may introduce additional runtime overhead; the abstract does not mention the magnitude of this overhead, and the full text needs to be checked.



### Related work

  * No newer related research directly building on this work was found (within the scope of this search, no follow-up papers directly citing or extending ICWM were found).
  * Worth surveying: medium-high. "In-context system identification" is a generalization dimension complementary to other WAM/VLA generalization studies on the list (e.g., "Do World Action Models Generalize Better than VLAs?" which focuses on robustness to visual/language perturbations) — namely, "new hardware/new viewpoint configurations" rather than "perturbations within the same configuration" — worth including as part of understanding the full picture of VLA generalization problems.



### Conclusion

  * Overall assessment: worth referencing, especially for engineers concerned with "cross-platform/cross-viewpoint deployment" problems. Its core concept (using contextual interaction for system identification rather than demonstrations for task specification) offers an approach to adapting to new execution environments without fine-tuning, which is meaningful in practical settings where robot hardware/camera configurations frequently change.
  * Relationship to other papers: ICWM and "Do World Action Models Generalize Better than VLAs?" on the list both focus on VLA generalization limitations, but from different angles — the latter tests "robustness to perturbations," the former tests "adaptation to new hardware/viewpoint configurations"; the two papers can be viewed as complementary generalization research directions rather than a direct extension or challenge relationship.
  * ROCm/AMD relevance: no clear connection to ROCm/AMD can be discerned from the abstract's content; the paper does not mention the hardware platform used for training or inference.
