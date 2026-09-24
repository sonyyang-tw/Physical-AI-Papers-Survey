---
layout: paper
title: "Dreamitate: Real-World Visuomotor Policy Learning via Video Generation"
section: wm
page_id: "1945364542"
permalink: /wm/dreamitate-real-world-visuomotor-policy-learning-via-video-generation-1945364542/
---

**Paper** : [Dreamitate: Real-World Visuomotor Policy Learning via Video Generation](https://arxiv.org/abs/2406.16862)  
**Source** : arXiv / CoRL 2024 (Conference on Robot Learning) / Columbia University, Toyota Research Institute, Stanford University  
**arXiv ID** : 2406.16862

### Abstract

The ability of robot manipulation policies to generalize across diverse visual environments is a key challenge. Dreamitate proposes a visuomotor policy learning framework that leverages a video diffusion model pretrained on large-scale web video, fine-tuned on task-specific human demonstrations. At test time, the model generates a "task execution video" conditioned on an image of the new scene, and this synthesized video is then used directly to control the robot. A key insight is that using common tools naturally bridges the embodiment gap between human hands and robot grippers. The authors validate the approach on four tasks of increasing complexity, showing that leveraging web-scale generative models allows the policy to achieve generalization significantly better than existing behavior cloning methods.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945364542_dreamitate_fig1.png) 

_Figure 1: Real-World Visuomotor Policy Learning via Video Generation - Dreamitate fine-tunes a video generative model to synthesize videos of tool-use demonstrations, which are tracked to extract robot actions._

![Figure]({{ site.baseurl }}/assets/images/1945364542_dreamitate_fig2.png) 

_Figure 2: Method Overview - stereo camera recordings of human demonstrations, video model fine-tuning, and 3D trajectory extraction for closed-loop execution._

  * **Problem addressed**: Behavior-cloning-type policies generalize poorly when facing visual scenes outside the training distribution (new backgrounds, new lighting, new object appearances).
  * **Main method**: A pretrained video diffusion model is first fine-tuned on human demonstration videos, so that it can generate a synthesized video of "performing the task" conditioned on a starting image of a new scene; then, tool trajectories are extracted from the generated video via visual tracking (3D tracking) and converted into an explicit action sequence to control the robotic arm.
  * **Difference from prior approaches**: Unlike behavior-cloning policies that directly regress actions from images, Dreamitate splits the process into two stages — "predicting the future" and "generating actions" — first using a generative model to "imagine" the video of the task-execution process, then translating the video into actions, thereby transferring the visual generalization ability embedded in web-scale video data to the robot policy.
  * **Key methodological design**: The policy pipeline is: (1) input an observation image of the new scene; (2) the fine-tuned video diffusion model generates a future video of a tool (such as tongs, a shovel, or other common tools) manipulating the object; (3) 3D tracking is performed on the tool in the generated video to obtain its motion trajectory in space; (4) the trajectory is converted into commands for the robot's end effector and executed directly. Using "tools" as the shared medium between human demonstration and robot execution is the core design for bridging the embodiment gap.



### Result

  * On four manipulation tasks of increasing complexity, Dreamitate demonstrates significantly higher visual generalization ability (able to handle scene-appearance changes not seen during training) compared to existing behavior cloning baselines.
  * Fairness of the paper: The Columbia/TRI/Stanford team provides a project website and code (cvlab-columbia/dreamitate), giving it a degree of reproducibility; however, the abstract does not detail specific quantitative metrics or baseline comparison details, and verification against the full text and other papers (such as later works on video-generation-as-policy, e.g., 2508.00795 "Video Generators are Robot Policies") is needed to confirm consistency of results.



### Limitation

  * The method relies on "common tools" as the medium between human and robot; the abstract does not clearly address its applicability to tasks that do not involve tool use, i.e., purely bare-handed/direct gripper manipulation of objects, and further verification of the full text is needed.
  * Relying on video generation model inference plus subsequent 3D tracking may introduce relatively high inference latency; the abstract does not mention real-time performance, which is a potential weakness for practical deployment.
  * The quality of the generated video and the accuracy of 3D tracking directly affect final action accuracy, a typical error-accumulation risk shared by "generative world-model-driven policies" in general, but the abstract does not specifically discuss failure modes.



### Related work

  * This belongs to the "video-generation-driven robot policy" track as one of its early representative works, with a clear continuation in later, more recent work along the same research direction (such as 2508.00795, "Video Generators are Robot Policies"), showing that this track continues to receive attention and expansion.
  * Assessment of how worthwhile the related work is to survey: high. Dreamitate is often cited by recent world model / video-based policy surveys as a representative work of the paradigm of "using generated video as a proxy for action prediction."



### Conclusion

  * This paper is an important early demonstration connecting "large-scale video generation models" with "robot manipulation policies." Its "tools as a bridge" approach to solving the embodiment gap is somewhat inspiring, and it is worth citing as a reference for world model / video-based policy research.
  * Relationship to other important papers: It can be seen as an alternative data/policy generation paradigm distinct from the MimicGen (geometric data generation) track — the two respectively represent "geometric recomposition" and "generative video imitation" — and it also echoes the "video world model-driven policy" category discussed in world model surveys (such as the multiple surveys in this collection).
  * ROCm/AMD relevance: This method fundamentally relies on training and inference of a video diffusion model, and the degree of support for training/inference of this kind of large generative model on ROCm (such as the PyTorch ROCm equivalent of the diffusers ecosystem, and GPU compatibility of the 3D tracking toolchain) needs to be separately verified; the abstract does not mention specific hardware or framework details, so no clear connection can be determined, and honestly, no clear connection can be identified.
