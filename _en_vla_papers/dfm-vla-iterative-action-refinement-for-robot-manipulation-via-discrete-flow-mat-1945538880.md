---
layout: paper
title: "DFM-VLA: Iterative Action Refinement for Robot Manipulation via Discrete Flow Matching"
section: vla
page_id: "1945538880"
permalink: /en/vla/dfm-vla-iterative-action-refinement-for-robot-manipulation-via-discrete-flow-mat-1945538880/
---

**Paper** : [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)](https://arxiv.org/abs/2503.09215)  
**Source** : arXiv (cs.CV / cs.AI)  
**arXiv ID** : 2503.09215

### Abstract

EOT-WM is a world model for autonomous driving that focuses on controlling the trajectories of both the "ego vehicle" and "other vehicles" simultaneously, in order to generate more realistic driving simulation videos. The authors point out that advanced end-to-end autonomous-driving systems predict the motion of other vehicles and plan the ego vehicle's trajectory, whereas existing world models mostly emphasize controllability of only the ego vehicle's trajectory, leaving other vehicles' motion uncontrolled, which makes it difficult to realistically simulate the interaction between the ego vehicle and its surrounding environment. EOT-WM first projects the trajectories of the ego vehicle and other vehicles from BEV (bird's-eye-view) space into image coordinates, matching trajectories with the corresponding vehicles in the video via pixel position; it then uses a Spatial-Temporal VAE to encode the trajectory video, aligning it spatiotemporally with the latent representation of the driving video; and it designs a trajectory-injected diffusion Transformer to denoise the noisy latent video to generate the final video. The authors also propose a new metric based on control-latent similarity to evaluate trajectory controllability. Experiments on the nuScenes dataset show that this method improves FID by 30% and FVD by 55% compared to SOTA methods, and can use its own generated trajectories to predict unseen driving scenarios.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945538880_dfmvla_fig1.png) 

_Figure 1: Comparison of decoding paradigms — (1) autoregressive (AR) models require as many steps as the length of the action sequence; (2) discrete diffusion/flow-matching methods can iteratively refine actions with fewer steps._

![Figure]({{ site.baseurl }}/assets/images/1945538880_dfmvla_fig2.png) 

_Figure 2: Overall DFM-VLA architecture — given language-vision context and noisy action tokens, the model predicts clean actions and iteratively refines them via discrete flow matching._

  * Problem addressed: Existing driving world models can only controllably generate the ego vehicle's trajectory, while the motion of other vehicles is uncontrolled (random or dependent on data distribution), making it impossible to realistically simulate interaction scenarios between the ego vehicle and other traffic participants, which limits the credibility of world models as simulators for evaluating autonomous-driving systems.
  * Main method: EOT-WM (Ego-Other vehicle Trajectories World Model) unifies control of ego and other vehicle trajectories within the same video latent space, with three core components:
    * Video-based Trajectory Representation (VTR): projects the trajectory of each vehicle (ego and others) from BEV space into the image coordinate system, matching trajectories with the corresponding vehicles in the video frames via pixel position.
    * Aligned Motion Guidance Generation (AMGG): uses a spatiotemporal VAE to encode these "trajectory videos" so that they align spatially and temporally with the latent representation of the driving video itself.
    * Trajectory-injected Diffusion Transformer (TiDiT): uses a diffusion Transformer to denoise the noisy video latent, injecting trajectory guidance signals during denoising to generate controlled driving videos.
  * Difference from prior approaches: Previous methods (e.g., conditioning only on the ego vehicle's trajectory or waypoints) neglect the controllability of other vehicles, causing the behavior of other vehicles in simulation to be disconnected from real interactions; EOT-WM converts the trajectories of multiple vehicles into a unified visual latent space, allowing the generative model to simultaneously "understand" the motion intentions of both the ego vehicle and other vehicles.
  * Description of the key methodological design: The model is built on top of CogVideoX (a text/image-to-video diffusion model); besides the original driving video, the input also includes a set of trajectory videos (each vehicle's future trajectory drawn as a visualized trajectory layer, with positions corresponding to the image coordinate system); these trajectory videos are aligned to vehicle identities via VTR, then encoded via AMGG into a latent tensor with the same dimensionality as the driving video; at each step of diffusion denoising, TiDiT feeds the trajectory latent and video latent jointly into the Transformer, progressively denoising to generate the final driving video, so trajectory conditioning can simultaneously influence the motion trajectory of the ego vehicle and every other vehicle in the frame.

### Result

  * Main results: on the nuScenes dataset, compared to the SOTA methods at the time, FID improves by 30% and FVD by 55%; a new metric (based on control-latent similarity) is proposed to evaluate trajectory controllability, showing higher fidelity of trajectory control. In addition, the model can use its own generated trajectories to predict unseen driving scenarios, showing a degree of generalization ability.
  * Enhancements: mainly improves "video generation quality" (large FID/FVD gains) and "multi-vehicle trajectory controllability," which is the core differentiating advantage over previous methods that only controlled the ego vehicle's trajectory.
  * Fairness: the FID/FVD improvement percentages given in the abstract are results of the authors' own comparisons; it is not stated which specific SOTA baseline(s) were compared against, and no independent third-party or follow-up-paper verification of these numbers has been found. It would be necessary to check other papers (e.g., subsequent driving world model benchmark papers) to see whether they have cross-validated EOT-WM's results or reached different conclusions.

### Limitation

  * Self-stated limitations in the paper: only the arXiv abstract page was read; the abstract itself does not list an explicit limitation section.
  * Weaknesses inferred from the results:
    * The method relies on projection from BEV to image coordinates and pixel-position matching; in scenes with heavy occlusion or densely overlapping vehicles, the matching between trajectories and vehicles may be unstable, but the abstract does not discuss this case.
    * It is only validated on nuScenes (a single dataset with a specific sensor configuration and region); generalization across datasets or sensor configurations is unknown.
    * The paper has undergone multiple revisions (v1 to v4, spanning March to November 2025), which may reflect adjustments to the method or evaluation during the review process, but the specific changes cannot be determined from the abstract.

### Related work

  * Based on web searches, this research direction already has follow-up work, such as the 2026 papers "EgoExo-WM: Unlocking Exo Video for Ego World Models" and "Ego-Dynamics-Augmented World Model for Autonomous Driving with Zero-Shot Cross-Chassis Adaptation," showing that the driving world model field continues to move toward richer viewpoint fusion and cross-vehicle generalization. In addition, a survey from October 2025, "A Comprehensive Survey on World Models for Embodied AI" (arXiv:2510.16732), cites this paper and can serve as a quick entry point for grasping the overall landscape of the field.
  * Degree to which the related work merits surveying: high. This area (controllability and multi-agent interaction simulation in driving world models) continues to see new work published; it is recommended to use the above survey to quickly locate other related methods for comparison.

### Conclusion

  * Overall assessment: EOT-WM proposes a clear architectural solution (VTR + AMGG + TiDiT) to the concrete and practical problem of "uncontrollable other-vehicle trajectories," with substantial FID/FVD improvements. It is a worthwhile reference in driving-world-model controllability research, particularly because its trajectory-to-image-coordinate projection technique is engineering-reproducible.
  * Relationship to other important papers: This work extends the line of driving-world-model research built on video diffusion models such as CogVideoX, challenging the limitation of prior methods that "only control the ego vehicle's trajectory"; it continues to evolve alongside subsequent works such as EgoExo-WM and Ego-Dynamics-Augmented World Model within the same lineage.
  * Gaps regarding ROCm/AMD: the abstract does not mention the hardware platform or framework details used for training/inference, so no clear connection to ROCm/AMD is apparent, and none should be speculated. If a team wants to reproduce this kind of CogVideoX-based diffusion Transformer training pipeline on AMD hardware, they would need to separately verify the support status of the CogVideoX family of models on ROCm.
