---
layout: paper
title: "World Models for Robotic Manipulation: A Survey"
section: wm
page_id: "1945391939"
permalink: /wm/world-models-for-robotic-manipulation-a-survey-1945391939/
---

**Paper** : [World Models for Robotic Manipulation: A Survey](https://arxiv.org/abs/2606.00113)  
**Source** : arXiv (no specific conference publication indicated yet)  
**arXiv ID** : 2606.00113

### Abstract

Robotic manipulation requires the ability to anticipate how an action will change objects, contact, and scene geometry before execution. Learned world models provide this capability by predicting task-relevant future evolution conditioned on robot intervention, but the term "world model" now encompasses latent dynamics models, action-conditioned video generators, 3D/4D scene predictors, physics-informed simulators, and prediction modules embedded within vision-language-action (VLA) systems—this diffusion of scope has fragmented the literature and blurred the design choices that truly matter for manipulation tasks. This survey organizes the literature around three questions: what future representation is predicted, how prediction is linked to action, and when prediction is used within the robot learning pipeline. The authors give world models an operational definition as "action-conditioned predictive systems," distinguishing them from perception modules, inverse models, policies, and reward/value functions, and organize existing work into five representation families. They develop a functional taxonomy distinguishing "integrated prediction-action models" from "explicit predictive planners," and categorize infrastructure roles (synthetic experience generation, candidate filtering, search-based evaluation, learned environments, outcome verification) spanning pretraining, post-training, and inference-time adaptation stages. They review 34 manipulation datasets and organize evaluation protocols for prediction fidelity, task performance, and simulator reliability.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391939_wmsurvey_fig1.png) 

_Fig. 1: World models predict task-relevant future world evolution (typically conditioned on observations and robot actions). This paper organizes the literature along three complementary axes: predicted representation, predictive core, and the role of prediction in the action interface, learning infrastructure, and learning lifecycle._

![Figure]({{ site.baseurl }}/assets/images/1945391939_wmsurvey_fig2.png) 

_Fig. 3: Functional taxonomy of direct prediction-action interfaces. (a-b) Integrated prediction-action models embed prediction within the action generation model itself; (c-e) explicit predictive planners expose prediction as an intermediate target (subgoal, trajectory, or structured plan) to be realized by a downstream controller._

  * **Problem being addressed**: the term "world model" in robotic manipulation is defined too broadly, encompassing many different technical approaches, making it difficult to clarify the design choices that are truly critical for manipulation tasks.
  * **Main method**: using three core questions (what future representation is predicted, how it is linked to action, and when it is used within the learning pipeline) as classification axes, the paper gives an actionable definition—"a world model = an action-conditioned predictive system"—clearly distinguishing it from perception modules, inverse models, policies, and reward/value functions. Building on this, it establishes a taxonomy of five representation families, along with a functional taxonomy distinguishing "integrated prediction-action models" (where prediction and action are fused within the same model) from "explicit predictive planners" (predict first, then plan, with the two stages separated).
  * **Difference from prior approaches**: compared to approaches that simply classify by architecture (e.g., RNN-based, diffusion-based), this paper places greater emphasis on the dimensions of "functional role" and "usage timing," particularly proposing five infrastructure roles (synthetic experience generation, candidate filtering, search-based evaluation, learned environments, outcome verification) and situating world models within the context of the entire robot learning pipeline (pretraining/post-training/inference-time adaptation)—a relatively distinctive way of organizing the material.
  * **Description of key method design**: the article first gives an operational definition to delineate scope, then organizes the literature using a three-dimensional classification matrix of "representation family × functional role × usage stage," additionally systematically reviewing 34 manipulation datasets and their corresponding three types of evaluation protocols (prediction fidelity, task performance, simulator reliability), and finally identifies open challenges (contact modeling, hallucination control, action alignment, and benchmarking under closed-loop usage).



### Result

  * The "result" of this survey is providing a more precise, actionable definition and functional taxonomy of world models, and systematically reviewing 34 robotic manipulation datasets along with corresponding evaluation protocols, helping to clarify the current state of this rapidly growing but chaotic field.
  * The paper explicitly points out open challenges that remain in the field: contact modeling, hallucination control (i.e., generative models may produce predictions that do not conform to physical laws), action alignment, and insufficient benchmarking under closed-loop usage scenarios.
  * Fairness: as a survey, whether its classification framework and definitions are broadly adopted by the community needs to be verified against other papers (especially the other two world model surveys in this list) to see whether they adopt similar or conflicting definitions, in order to judge the generalizability of its taxonomy.



### Limitation

  * The limitations self-acknowledged by the paper (open challenges) include contact modeling, hallucination control, action alignment, and insufficient closed-loop benchmarking—these are both limitations of the field and open problems pointed out by this survey.
  * Since this is a survey, its "operational definition" itself carries a degree of subjectivity; different researchers may hold different views on "what counts as a world model," and whether this paper's definition can become a widely accepted standard remains to be seen.



### Related work

  * This paper is highly related to two other contemporaneous world model surveys (arXiv:2605.00080 and arXiv:2511.02097). The three can be viewed as part of a wave of surveys on world models for robotics that emerged concentrated in 2025-2026, and it is worth cross-comparing the differences in their classification angles (this paper emphasizes functional role and pipeline stage more; 2605.00080 emphasizes the three axes of policy coupling/simulator/video generation more; 2511.02097 does not restrict itself to methods "explicitly labeled as world models," adopting instead a capability-oriented perspective).
  * Assessment of how worth surveying the related work is: high, especially its proposed "action-conditioned predictive system" definition and five infrastructure role classifications, which have practical value for clarifying the relationship between world models and the prediction modules within VLA (vision-language-action) systems.



### Conclusion

  * This paper provides what appears to be the most precise, actionable definition of world models currently available, and offers a detailed functional classification and dataset/evaluation protocol organization specific to robotic manipulation scenarios, making it very valuable for researchers who want to systematically understand the technical choices in this field.
  * Relationship to other important papers: this paper's "action-conditioned predictive system" definition helps clarify the positioning of specific works such as Aether, MimicGen, and Dreamitate within the overall taxonomy (for example, Aether falls under integrated prediction-planning models, while Dreamitate is closer to the "video-generation-driven explicit prediction" route); it also forms a complementary perspective with the other two contemporaneous surveys.
  * ROCm/AMD relevance: this survey focuses on methodology and classification and does not touch on specific hardware implementation, so no direct connection to ROCm/AMD is apparent; however, for open challenges mentioned in the text such as "hallucination control" and "closed-loop benchmarking," developing corresponding evaluation benchmarks and simulators on AMD hardware would still require separately confirming the completeness of ROCm support for related open-source toolchains (such as physics simulation engines and VLA training frameworks).
