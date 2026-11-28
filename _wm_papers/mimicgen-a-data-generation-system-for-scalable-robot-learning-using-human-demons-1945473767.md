---
layout: paper
title: "MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations"
section: wm
page_id: "1945473767"
permalink: /wm/mimicgen-a-data-generation-system-for-scalable-robot-learning-using-human-demons-1945473767/
---

**Paper** : [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations](https://arxiv.org/abs/2310.17596)  
**Source** : arXiv / CoRL 2023 (7th Conference on Robot Learning) / NVIDIA  
**arXiv ID** : 2310.17596

### Abstract

Imitation learning requires large amounts of human demonstration data, but collecting such data is extremely costly. MimicGen proposes a data generation system that can automatically synthesize large-scale, diverse robot demonstration datasets from a small number (about 200) of human demonstrations, by adapting the original demonstrations to new scene configurations, object instances, and robot arm combinations, producing over 50,000 demonstrations across 18 tasks. The paper shows that imitation learning policies trained on this generated data achieve strong performance on long-horizon and high-precision tasks (such as multi-part assembly and coffee making), with results comparable to collecting additional real human demonstrations, making it an economical way to scale up robot learning data.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473767_mimicgen_fig1.png) 

_Figure 1: MimicGen Overview - generating large diverse datasets from a small number of human demonstrations by re-purposing them for new settings._

![Figure]({{ site.baseurl }}/assets/images/1945473767_mimicgen_fig2.png) 

_Figure 2: MimicGen System Pipeline - parsing source demos into object-centric subtask segments and adapting them to generate new demonstrations._

  * **Problem addressed**: Collecting human demonstration data is costly and time-consuming, which limits the scalability of imitation learning.
  * **Main method**: Starting from a small set of human demonstrations, MimicGen geometrically transforms the object-centric interaction subsegments of the demonstrations according to object poses in new scenes, re-stitching them together to generate complete demonstration trajectories suitable for the new scene configuration, and then converts these into robot-executable action sequences using an inverse kinematics (IK) solver.
  * **Difference from prior approaches**: Unlike traditional methods that require extensive human teleoperation to collect demonstrations, MimicGen can scale up data without additional human labor, and can generate new data across object instances, scene layouts, and even different robot arm embodiments.
  * **Key design details**: The system decomposes demonstrations into object-centric action segments (e.g., "grasp," "place" subtasks). For a new initial scene, it computes coordinate transformations based on the positions and poses of objects in the new scene, remapping the object-relative trajectories within each segment to the new scene, and then stitches the different segments together to form a complete task demonstration. This process can be repeated to generate large amounts of diverse data, and a filtering mechanism (e.g., keeping only generated demonstrations where the task succeeds) can be used to ensure data quality.

### Result

  * Using MimicGen, over 50,000 demonstrations were generated from about 200 human demonstrations, covering 18 tasks, multiple scene configurations, and various robot arms. Imitation learning policies trained with this data perform well on long-horizon, high-precision tasks (multi-part assembly, coffee making, etc.), and can handle a wider distribution of initial states.
  * The paper compares two approaches — "generating an equal amount of data with MimicGen" versus "collecting an equal amount of additional human demonstrations" — showing that the benefit of generated data is comparable to collecting more human demonstrations, proving it to be an economically viable way to augment data.
  * **Fairness of the paper**: This paper provides a public dataset, simulation environment, and code (NVlabs/mimicgen) that the community can use for verification. Whether other papers' comparison data conflict with these results needs to be verified (for example, whether subsequent work has pointed out that the generated data is of insufficient quality for certain task types).

### Limitation

  * The method described in the paper relies on object-centric segmentation of human demonstrations and precise object pose estimation. If scene object detection/pose estimation is inaccurate, the quality of generated trajectories may degrade.
  * The method is mainly validated in simulation environments; sensing noise and physical contact modeling factors present in the real world may not be fully captured by this data generation approach. The abstract and available information do not clearly mention results from large-scale real robot deployment, which requires further verification against the full paper.
  * The generated data is still constrained by the range of skills and object interaction patterns covered by the original human demonstrations, and may not be able to directly generate entirely new skill types not covered by the original demonstrations.

### Related work

  * MimicGen is a representative early work in the data generation/augmentation approach, sharing similar goals with many subsequent data synthesis methods that combine generative models (video diffusion, world models), such as Dreamitate, but takes a different methodological route: MimicGen performs geometric/kinematic-level trajectory recombination rather than image generation.
  * No newer related research has been found so far (no further search of subsequent citing works was conducted within the scope of this survey).
  * **Assessment of how worth surveying this related work is**: Medium-high. As an important baseline in the robot data generation field, it is frequently cited and compared against in subsequent world model / video generation data synthesis papers.

### Conclusion

  * This paper is an important baseline work in the field of robot learning data generation. Its method is concise, open-source, and reproducible, making it a valuable reference point for understanding data augmentation through the "non-generative model route."
  * **Relationship to other important papers**: It is commonly used as a baseline for comparison against generative world-model-driven data synthesis methods (e.g., Dreamitate, which uses video diffusion to generate demonstrations, as well as more recent world model data generation methods). The two represent different data augmentation philosophies — "geometric recombination" versus "generative synthesis."
  * **ROCm/AMD relevance**: This paper primarily uses NVIDIA simulation environments (robosuite/MuJoCo family) and IK solvers, belonging to general-purpose robot learning infrastructure, and does not involve specific accelerator optimization. When reproducing this on ROCm, it should be noted that simulation environments (Isaac/robosuite, etc.) currently mostly rely on the NVIDIA ecosystem. For deployment on AMD platforms, the compatibility of these simulation environments with ROCm/non-CUDA environments needs to be evaluated — this is an area where ROCm still needs strengthening in the embodied AI simulation pipeline.
