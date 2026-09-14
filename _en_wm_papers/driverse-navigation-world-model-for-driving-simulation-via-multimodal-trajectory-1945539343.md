---
layout: paper
title: "DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment"
section: wm
page_id: "1945539343"
permalink: /en/wm/driverse-navigation-world-model-for-driving-simulation-via-multimodal-trajectory-1945539343/
---

**Paper** : [DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment](https://arxiv.org/abs/2504.18576)  
**Source** : arXiv / ACM Multimedia (ACM MM) 2025 (accepted)  
**arXiv ID** : 2504.18576

### Abstract

This paper introduces DriVerse, a generative model that simulates "navigation-driven" driving scenes starting from a single image and a future trajectory. Previous autonomous-driving world models either fed trajectories or discrete control signals directly into the generation pipeline (leading to poor alignment between the control input and the implicit features of the 2D generative model, and low output quality), or used coarse text instructions or discrete vehicle control signals (which lack the precision needed to guide fine-grained, trajectory-specific video generation, making them unsuitable for evaluating real autonomous-driving algorithms). DriVerse introduces explicit trajectory guidance in two complementary forms: first, tokenizing the trajectory into text prompts (using a predefined trend vocabulary that integrates seamlessly with language conditioning); second, converting the 3D trajectory into a 2D spatial motion prior to strengthen control over the static content of the driving scene. To handle dynamic objects, the authors further introduce a lightweight motion alignment module that focuses on inter-frame consistency of dynamic pixels, significantly improving the temporal coherence of moving elements across long sequences. With almost no additional training or extra data, DriVerse outperforms specialized models on future video generation tasks on both the nuScenes and Waymo datasets.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539343_driverse_fig1.png) 

_Figure 1: DriVerse navigation world model overview - generating high-quality video aligned with real driving scenes from a single image and a navigation trajectory._

![Figure]({{ site.baseurl }}/assets/images/1945539343_driverse_fig2.png) 

_Figure 2: DriVerse framework overview - the two main modules of static alignment (Multimodal Trajectory Prompting) and dynamic alignment (Motion Alignment)._

  * Problem addressed: Previous autonomous-driving navigation world models did a poor job of aligning "control signals" with "generated frames" — feeding raw trajectories/discrete control signals directly in leads to low-fidelity output, while using coarse text instructions or discrete control signals lacks the precision needed to support fine-grained, trajectory-specific video generation, making them unsuitable for evaluating real autonomous-driving algorithm performance.
  * Main method: Proposes a "Multimodal Trajectory Prompting" (MTP) strategy that jointly leverages semantic and spatial cues to guide video generation: (1) defining a "trend vocabulary" that converts trajectory motion patterns into a series of discrete tokens, which are added to conventional text prompts for semantic conditioning; (2) converting the 3D trajectory into a 2D spatial motion prior to strengthen control over the static content of the scene. In addition, a lightweight motion alignment module is introduced that focuses on inter-frame consistency of dynamic pixels. To handle artifacts caused by changes in vehicle heading angle during long-sequence generation, a Dynamic Window Generation (DWG) strategy is also designed, which adaptively updates the conditioning reference frame at appropriate intermediate frames according to heading-angle changes during autoregressive extended generation.
  * Difference from previous approaches: Compared with methods that directly force raw trajectory values or discrete control signals into the generative model, DriVerse's dual explicit trajectory guidance — "textualized trend vocabulary + 2D spatial motion prior" — better matches the language/spatial conditioning input forms that 2D generative models (such as diffusion models) are accustomed to, resulting in better alignment. Meanwhile, the motion alignment module and dynamic window generation strategy specifically address the "temporal consistency of dynamic objects" and "steering artifacts in long-sequence autoregressive generation" issues that other methods tend to overlook.
  * Key design description: The overall pipeline can be understood as follows: given a starting frame and a future 3D trajectory, the trajectory is first converted into two representations that are fed into the generative model simultaneously — one is "trend vocabulary" text tokens (e.g., discrete words describing trends such as acceleration or turning), concatenated with the original text prompt; the other projects the 3D trajectory into a motion prior in 2D image space (e.g., the expected position of the future path within the frame), used to constrain how static scene content (roads, buildings, etc.) changes as the camera moves. During generation, the motion alignment module focuses on "things that move" in the frame (such as other vehicles and pedestrians), ensuring their appearance and position changes are coherent across consecutive frames rather than jumping randomly at the pixel level. When autoregressive generation extends to longer videos, the dynamic window generation strategy detects the magnitude of vehicle heading-angle change and updates the reference frame used to condition the next generation segment at the appropriate time, avoiding image distortion caused by accumulated error over long durations.



### Result

  * With almost no additional training or extra data, DriVerse outperforms specialized models on future video generation tasks on both the nuScenes and Waymo datasets.
  * The abstract and available information do not provide specific quantitative metrics (such as specific FID, FVD, or other video generation quality scores); the full text needs to be consulted for precise comparison data.
  * The abstract does not mention direct comparison data with other autonomous-driving world models (such as GeoDrive or WoTE); comparison data from other papers needs to be checked to confirm DriVerse's relative ranking within this sub-field.



### Limitation

  * The paper's abstract does not contain an explicit self-stated Limitation section; the full text needs to be checked to confirm the limitations the authors state themselves.
  * Potential weaknesses inferred from the method design: DriVerse relies on a predefined discretized trajectory representation via the "trend vocabulary," which may have limited expressive capacity for extreme or rare driving behaviors beyond the vocabulary's coverage (such as complex trajectories for emergency obstacle avoidance). In addition, the method is mainly validated on video generation quality (visual fidelity and temporal coherence) rather than directly validating its effectiveness as a downstream autonomous-driving planning/decision evaluation tool; whether it can be directly used for trajectory evaluation like WoTE remains to be verified.



### Related work

  * GeoDrive (arXiv:2505.22421, an autonomous-driving world model driven by 3D geometric information with precise action control) is a contemporaneous related autonomous-driving world model paper, suitable for comparing similarities and differences with DriVerse in geometry/trajectory conditioning approaches.
  * Similar survey resources (such as Awesome-World-Model and World-Models-Autonomous-Driving-Survey on GitHub) continue to collect this type of paper, showing that this sub-field is still evolving rapidly.
  * Degree worth surveying: medium-high. DriVerse represents a landmark work in the "explicit trajectory conditioning" design school of autonomous-driving world models, worth comparing alongside WoTE (BEV-space trajectory evaluation) and GeoDrive (3D geometric conditioning) and other papers with different technical routes, to understand the current technical divergences and convergence points in this field.



### Conclusion

  * Overall assessment: Worth reference, especially for readers concerned with the question of "how to make a generative world model respond precisely to trajectory/control input." Its dual explicit trajectory guidance design of "textualized trend vocabulary + 2D spatial motion prior" has a certain degree of engineering innovation, and it has been formally accepted at ACM MM 2025, indicating a degree of peer-review scrutiny.
  * Relationship with other important articles: DriVerse and WoTE (arXiv:2504.01941) both belong to the autonomous-driving world model field, but take different technical routes — DriVerse focuses on "generating high-fidelity future driving scene video" for training/evaluation use, while WoTE focuses on "using a BEV-space world model to directly perform online trajectory evaluation" to support end-to-end driving decisions. The two can be seen as representatives of two different application orientations: "generative simulation" and "decision evaluation." It can also be compared with contemporaneous papers such as GeoDrive on different trajectory/geometry conditioning technical details.
  * ROCm/AMD relevance: The paper focuses on the trajectory conditioning design of the generative model and video generation quality evaluation, and does not mention the computing hardware platform used or any ROCm-related content. No clear connection to ROCm/AMD can be found from the available information.
