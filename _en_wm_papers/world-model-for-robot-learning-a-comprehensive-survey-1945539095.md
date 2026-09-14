---
layout: paper
title: "World Model for Robot Learning: A Comprehensive Survey"
section: wm
page_id: "1945539095"
permalink: /en/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/
---

**Paper** : [World Model for Robot Learning: A Comprehensive Survey](https://arxiv.org/abs/2605.00080)  
**Source** : arXiv (no specific conference publication indicated yet)  
**arXiv ID** : 2605.00080

### Abstract

A world model is a predictive representation of how the environment evolves conditioned on actions, and it has become a core component of robot learning, supporting policy learning, planning, simulation, evaluation, and data generation, evolving rapidly alongside the rise of foundation models and large-scale video generation techniques. However, existing literature is quite fragmented in terms of architecture, functional role, and embodied application domain. This survey systematically examines, from a robot learning perspective, how world models couple with robot policies, how they serve as learned simulators for reinforcement learning and evaluation, and how robot video world models have evolved from "imagination-based generation" to "controllable, structured, foundation-model-scale" forms; it further connects these concepts to navigation and autonomous driving, and summarizes representative datasets, benchmarks, and evaluation protocols. The authors commit to continuously maintaining an accompanying GitHub repository.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539095_survey_wm2_fig1.png) 

_Figure 1: Overview of the organization of this survey - architectural coupling of world models with robot policies, world models as simulators, and related evaluation/benchmarks._

  * **Problem being addressed**: literature on world models is scattered across different architectures (latent dynamics, video diffusion, etc.), different functional roles (policy coupling, simulator, data generator), and different application domains (manipulation, navigation, autonomous driving), lacking systematic organization.
  * **Main method**: this is a survey rather than a new model proposal; it establishes a taxonomy that organizes the literature from three angles: (1) how world models couple with robot policies (e.g., as an internal representation of the policy or as an external simulator); (2) the role of world models as "learned simulators" for reinforcement learning training and evaluation; (3) the technical evolution of robot video world models from pure "imagination-based generation" to "controllable, structured, foundation-model-scale" forms.
  * **Difference from prior approaches**: compared to existing surveys that may focus on only a single sub-area (e.g., only manipulation or only navigation), this paper attempts to span robotic manipulation, navigation, and autonomous driving—three major application scenarios—providing a more comprehensive unified perspective, with particular emphasis on the functional relationship between world models and policy learning/reinforcement learning/evaluation, rather than merely architectural classification.
  * **Description of key method design**: the article's structure is expected to unfold along three axes: the policy-coupled world model dimension, the learned-simulator-for-RL/evaluation dimension, and the video-generation dimension (from imagination-based to foundation-scale video world models); on this basis it supplements coverage of datasets, benchmarks, and evaluation protocols, and finally connects to corresponding applications in navigation and autonomous driving.



### Result

  * As a survey paper, its "result" is manifested in systematically organizing and classifying the rapidly growing literature on world models for robot learning, clarifying key paradigms and applications, and pointing out major challenges and future directions.
  * Fairness: since this is a broad literature review, whether its coverage and classification are comprehensive or have omissions needs to be verified against other contemporaneous surveys (such as the other two in the list, 2606.00113 and 2511.02097) to check whether their classification approaches are consistent or complementary, in order to cross-validate its completeness and objectivity.



### Limitation

  * The limitation of survey-type papers lies in the fact that their classification framework reflects the authors' subjective way of organizing material, which may differ from other surveys (e.g., the contemporaneous 2606.00113 and 2511.02097) that adopt different ways of dividing the field, requiring readers to cross-reference in order to gain a more complete understanding.
  * The abstract does not provide specific quantitative evaluations or performance comparison data; its "result" leans toward qualitative organization rather than quantitative evidence, which is a general limitation of survey-type articles.
  * The paper mentions that it will continuously maintain a GitHub repository to supplement new work, showing that the authors are also aware that this field is evolving rapidly and that the current version may quickly become outdated.



### Related work

  * This paper overlaps significantly in topic with two other contemporaneous world model surveys (arXiv:2606.00113 "World Models for Robotic Manipulation: A Survey" and arXiv:2511.02097 "A Step Toward World Models: A Survey on Robotic Manipulation"), and is worth cross-reading to compare the similarities and differences in their classification frameworks.
  * Assessment of how worth surveying the related work is: high. As a survey itself, its reference list and taxonomy serve as an important index for further tracking specific technical papers in the world model field (such as Aether, MimicGen, Dreamitate).



### Conclusion

  * As a relatively recent (2026) world model survey, this paper provides a unified framework spanning policy, simulator, and video generation perspectives, suitable as an entry point for research and for quickly grasping the overall landscape of the field—worth reading first.
  * Relationship to other important papers: this paper can serve as a "map" for understanding where other specific technical papers in this list (Aether, MimicGen, Dreamitate) sit within the overall world model taxonomy, and should also be cross-referenced with the other two contemporaneous surveys to avoid a one-sided understanding arising from a single survey's classification preferences.
  * ROCm/AMD relevance: as a literature survey, this paper does not touch on specific hardware implementation details, so no direct connection to ROCm/AMD is apparent; however, the "foundation-model-scale video world models" it mentions imply a high demand for large-scale GPU computing resources for training and deployment, and the maturity of ROCm ecosystem support for such large-scale training/inference (compared to the CUDA ecosystem) is an area AMD needs to continuously monitor and strengthen when positioning itself in this field.
